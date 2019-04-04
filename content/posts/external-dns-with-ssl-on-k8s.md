Title: Setting Up a Domain with SSL on DigitalOcean Kubernetes using ExternalDNS and Helm
Date: 2019-04-04
Author: andrewsomething
Category: digitalocean
Tags: k8s, digitalocean, external-dns, lets-encrypt
Slug: external-dns-with-ssl-on-k8s

A little while back I [added support](https://github.com/helm/charts/pull/11257) for DigitalOcean to the ExternalDNS Helm chart, and I wanted to share my notes on how to use it. [ExternalDNS](https://github.com/kubernetes-incubator/external-dns) is an extremely convenient tool that allows you to dynamically control DNS records for your Kubernetes resources just by adding an annotation. In this post, I'll walk through how to install it with Helm and use it to point a domain at a Kubernetes service. I'll also cover setting up SSL using a DigitalOcean managed SSL certificate on the load balancer.

First, a few assumptions:

* You have access to a Kubernetes cluster with kubectl
* You have the [Helm client installed locally](https://helm.sh/docs/using_helm/#installing-the-helm-client)
* Helm has been configured in the cluster using [a service account with the correct permissions](https://helm.sh/docs/using_helm/#tiller-and-role-based-access-control)
* You have `doctl`, the DigitalOcean CLI, [installed locally](https://github.com/digitalocean/doctl#installing-doctl)
* You have a [domain hosted on DigitalOcean](https://www.digitalocean.com/docs/networking/dns/how-to/add-domains/)

## Installing ExternalDNS with Helm

With all of that in place, the first thing to do is install ExternalDNS into the cluster. You will need to [generate a DigitalOcean API token](https://www.digitalocean.com/docs/api/create-personal-access-token/) for it to use. It's best to create a token specifically for this service rather than using one you may have in your local environment. Then run the following command replacing `$DO_API_TOKEN` with the token you generated:

    helm install --name external-dns \
      --set digitalocean.apiToken=$DO_API_TOKEN,provider=digitalocean,rbac.create=true \
      stable/external-dns

You can verify that it has been successfully installed by running:

    $ kubectl get pods -l "app=external-dns"

When ready, the output should look something like this:

    NAME                           READY     STATUS    RESTARTS   AGE
    external-dns-68bfc948b-jhhrq   1/1       Running   0          34s

## Generating a DigitalOcean Managed SSL Certificate

Next, use `doctl` to generate an SSL certificate managed by DigitalOcean making use of their Let's Encrypt integration. Giving it a name and replacing `example.com` with your domain, run:

    doctl compute certificate create  --name k8s-cert \
      --type lets_encrypt --dns-names example.com

The output will include an ID that looks something like `9r3e053d-da5e-4390-b7b8-0fs23486e41q`. You'll need that in the next step.

## Deploying the Kubernetes Service

Now you are ready to deploy your service to the Kubernetes cluster. For this example we are using an NGINX container for the deployment, but that could be any application running in your cluster. The important part for this exercise is the LoadBalancer Service. Here is the full example:

    kind: Service
    apiVersion: v1
    metadata:
      name: https-with-cert
      annotations:
        external-dns.alpha.kubernetes.io/hostname: "example.com"
        service.beta.kubernetes.io/do-loadbalancer-redirect-http-to-https: "true"
        service.beta.kubernetes.io/do-loadbalancer-certificate-id: "9r3e053d-da5e-4390-b7b8-0fs23486e41q"
    spec:
      type: LoadBalancer
      selector:
        app: nginx-example
      ports:
        - name: https
          protocol: TCP
          port: 443
          targetPort: 80
    
    ---
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: nginx-example
    spec:
      replicas: 1
      template:
        metadata:
          labels:
            app: nginx-example
        spec:
          containers:
          - name: nginx
            image: nginx
            ports:
            - containerPort: 80
              protocol: TCP

Let's look a little closer at the `annotations` section:

      annotations:
        external-dns.alpha.kubernetes.io/hostname: "example.com"
        service.beta.kubernetes.io/do-loadbalancer-redirect-http-to-https: "true"
        service.beta.kubernetes.io/do-loadbalancer-certificate-id: "9r3e053d-da5e-4390-b7b8-0fs23486e41q"

[Kubernetes annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) are just metadata attached to a Kubernetes object. They can be used for anything from specifying a maintainer for the service to a git commit hash or other release information. They can also be used to pass on information to controllers. In our case, both the [DigitalOcean Cloud Controller Manager](https://github.com/digitalocean/digitalocean-cloud-controller-manager) and the ExternalDNS controller are watching for services created with these annotations. Breaking down each one:

* `external-dns.alpha.kubernetes.io/hostname` - Specifies the domain name to be assigned to the service
* `service.beta.kubernetes.io/do-loadbalancer-certificate-id` - Specifies the ID of the DigitalOcean managed SSL cert
* `service.beta.kubernetes.io/do-loadbalancer-redirect-http-to-https` - Configures the load balancer to automatically redirect clients from HTTP to HTTPS

After replacing the domain and certificate ID in the full example and saving it to a file, apply the configuration with:

    kubectl apply -f path/to/https-with-domain.yaml

Now let's take a quick look at the logs for ExternalDNS by running:

    kubectl logs \
      `kubectl get pod -l app=external-dns -o jsonpath="{.items[0].metadata.name}"`

When the record has been successfully configured, you will see two lines like:

    time="2019-04-04T01:19:11Z" level=info msg="Changing record." action=CREATE record=example.com ttl=300 type=A zone=example.com
    time="2019-04-04T01:19:12Z" level=info msg="Changing record." action=CREATE record=example.com ttl=300 type=TXT zone=example.com

You might be wondering why it created two records. ExternalDNS uses `TXT` records to mark records that it manages. It will not modify any records without a corresponding `TXT` record.

## Wrapping It Up

With our service successfully deployed, it will now be available at the configured domain with SSL. If we redeploy the service latter, the DNS record will persist even if the underlying IP address were to change. If you're looking for more detail, here's some further reading for you:

* [Examples with additional configuration details for DigitalOcean load balancers using Kubernetes annotations](https://github.com/digitalocean/digitalocean-cloud-controller-manager/tree/master/docs/controllers/services/examples)
* [The full list of configuration details for the ExternalDNS Helm chart](https://github.com/helm/charts/tree/master/stable/external-dns#configuration)


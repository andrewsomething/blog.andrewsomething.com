Title: A Few Recent DigitalOcean Tools
Date: 2017-04-04
Author: andrewsomething
Category: digitalocean
Tags: Fabric, DigitalOcean, GitHub, Ansible
Slug: recent-digitalocean-tools

Obligatory comment about how it's been quite awhile since the last time I've blogged...

With that out of the way, I wanted to share a few things that I've done recently that might be useful for others. In particular, there are a couple [DigitalOcean][] related tools that might come in handy.

## fabric-digitalocean

As I've written before, [Fabric][] is a great tool for automating some basic systems administration tasks. Recently, I wrote `fabric-digitalocean` in order to make it easier to use Fabric with DigitalOcean Droplets. It provides an `@droplets` decorator for use in your Fabfiles. It can take a list of Droplet IDs, a tag, or a region as an argument. Then, using the DigitalOcean API, these arguments are expanded to provide Fabric with a list of hosts.

More and more, [tagging](https://www.digitalocean.com/company/blog/droplet-tagging-organize-your-infrastructure/) is becoming an important way to interact with DigitalOcean resources. For example, DO Load Balancers use tags for service discovery, and the [newly released Monitoring](https://www.digitalocean.com/company/blog/introducing-monitoring/) functionality allows you to create alert policies based on tags. If you're already using tags across your fleet, the ability to run tasks on instances based on how they are tagged is extremely convenient.

As a quick example, this Fabfile could be used to run the `uptime` on all Droplets tagged "production":

    from fabric.api import task, run
    from fabric_digitalocean.decorators import droplets
    
    @task
    @droplets(tag='production')
    def example():
        run('uptime')

It can be installed via `pip` with:

    pip install fabric-digitalocean

The source is [available on GitHub](https://github.com/andrewsomething/fabric-digitalocean). I'd love to hear any ideas you might have for other integration points between Fabric and the DO API.

## DigitalOcean monitoring agent Ansible role

While Fabric obviously still has a place in my toolkit, [Ansible][] has taken on a growing role in how I manage my infrastructure. It is flexible enough for both running one-off tasks and standing up services fully under configuration management.

[In Janurary](https://www.digitalocean.com/company/blog/improved-graphs/), DigitalOcean released an [open-source monitoring agent](https://github.com/digitalocean/do-agent). It's used to power both the graphs displaying Droplet metrics as well the new Monitoring and alerting features. You can optionally install the agent when creating new Droplets. Though if you have an existing fleet, it can be a bit tedious to install it on all of your currently running instances.

When I was backfilling the agent onto my existing Droplets, I wanted a single Ansible role that I could use regardless of the underlaying distribution. I was also eager to see what it takes to get something up on Ansible Galaxy, their hub for sharing and distributing roles. So I put together a role to install the agent on all supported distros and made it [available there](https://galaxy.ansible.com/andrewsomething/do-agent/).

You can install it with:

    ansible-galaxy install andrewsomething.do-agent

Once installed, an example playbook simply looks like:

    - hosts: all
      become: true
      roles:
         - andrewsomething.do-agent

The source is also [available on GitHub](https://github.com/andrewsomething/ansible-role-do-agent).

[DigitalOcean]: https://www.digitalocean.com
[Fabric]: http://www.fabfile.org/
[Ansible]: https://www.ansible.com/
[Prometheus]: https://prometheus.io/
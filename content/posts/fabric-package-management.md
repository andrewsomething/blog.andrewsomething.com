Title: Package Management with Fabric
Date: 2015-08-03 22:45
Author: andrewsomething
Category: fabric-package-management
Tags: Fabric, DigitalOcean, GitHub
Slug: fabric-package-management

Recently, I've been using [Fabric][] quite a bit. It is simple, Pythonic, and I've grown to enjoy using it for automating basic systems administration tasks when a full-fledged configuration management system is more than you need for the job.

For the most part, Fabric keeps to the basics, e.g. executing remote shell commands and uploading files. There are [quite a few sets of tools][] that have popped up to extend it, but unfortunately there no is "official" contrib library. Many of these project serve very specific use cases like deploying a Django application and duplicate certain functionality.

One thing that I've become a bit frustrated with is copying around convenience functions into multiple Fabfiles. In particular, I end up cargo culting functions related to package management. So to finally rid myself of these, I've created `fabric-package-management`.

The source is on [GitHub], and you can install it [from PyPI][] with:

    sudo pip install fabric-package-management

The aim is to provide basic primitives for package management with Fabric. Its focus is intentionally narrow. The 0.1 release only offers support for Apt, but I hope to see it grow support for more distributions. It could potentially add an abstraction layer for cross distro support.

Here's a quick example of using it to update all your DigitalOcean servers:

    import os
    import digitalocean
    from fabric.api import task, prompt, env, settings
    from fabric.operations import reboot

    from fabric_package_management import apt

    USER = 'username'

    def get_hosts():
        token = os.getenv('DO_TOKEN')
        manager = digitalocean.Manager(token=token)
        droplets = manager.get_all_droplets()
        hosts = []
        for d in droplets:
            hosts.append(d.ip_address)

        return hosts

    @task()
    def run():
        hosts = get_hosts()
        for h in hosts:
            with settings(host_string=h, user=USER):
                apt.update()
                apt.upgrade()
                if apt.reboot_required():
                    prompt("Reboot required. Initiate now?\nYes/No?",
                           "response",
                           default="No",
                           validate=r'yes|Yes|YES|no|No|NO')
                    if env.response.lower() == "yes":
                        reboot()

Hope you find this useful!

[Fabric]: http://www.fabfile.org/
[quite a few sets of tools]: https://github.com/fabric/fabric/issues/461
[GitHub]: https://github.com/andrewsomething/fabric-package-management
[from PyPI]: https://pypi.python.org/pypi/fabric-package-management/0.1
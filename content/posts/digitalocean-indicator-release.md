Title: DigitalOcean Indicator
Date: 2014-04-25 18:45
Author: andrewsomething
Category: DigitalOcean
Tags: Ubuntu, DigitalOcean, GitHub
Slug: digitalocean-indicator-release

![DigitalOcean Indicator screenhot](//i.imgur.com/ssV10vC.png)

The other weekend I took some time to play around with the [DigitalOcean API,][]
and this is what resulted. The [DigitalOcean indicator][] allows you to monitor and
manage your droplets directly from your panel. You can:

  - Quickly see which droplets are active.
  - Reboot, power on, and/or power down you droplets.
  - Copy your droplet's IP address with a click for easy access.

You can install it on Ubuntu from my PPA:

    sudo add-apt-repository ppa:andrewsomething/digitalocean
    sudo apt-get update
    sudo apt-get install digitalocean-indicator

It leverages [python-digitalocean], an API wrapper by [Lorenzo Setale][]. It's
also package for Ubuntu in my PPA.

[DigitalOcean API,]: https://developers.digitalocean.com/
[DigitalOcean indicator]: https://github.com/andrewsomething/digitalocean-indicator
[python-digitalocean]: https://github.com/koalalorenzo/python-digitalocean
[Lorenzo Setale]: https://github.com/koalalorenzo

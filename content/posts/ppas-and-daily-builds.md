Title: PPAs and Daily Builds
Date: 2009-06-10 05:46
Author: andrewsomething
Category: Ubuntu
Tags: bzr, daily builds, ppa, Ubuntu
Slug: ppas-and-daily-builds

So earlier today I was throwing together a script to publish bzr
snapshots to a PPA. My use case was pretty simple. It's a debian native
package. So the packaging and upstream are one and the same, so no need
to merge branches or make sure patches apply cleanly. Basically just
pull, build, and publish with a little bit of magic to set the versions
correctly.

But as I know there are a number of PPAs publishing snapshots of
upstream sources, I wanted to take a look around and see what others are
using. Unfortunetely, there doesn't really seem to be a location
pointing to a list of projects or with general information on how to go
about doing this. So here are some of the things I came across, just to
put it one place. Maybe it's time for a wiki page?

First of all, [James Westby][] is up to something really exciting with
bzr-builder (a plugin for bzr written in python) and Daily Debs. The
basic idea is to make doing nightly builds of upstream projects almost
trivial by using simple recipe files while bzr-builder does all the
heavy lifting. A recipie file could look as simple as this:

>     branch lp:foo
>     merge lp:foo/debian-pkg

I can't wait to see where this is going and to hear more about the
discussions around it at UDS.

You can find the spec here:
https://wiki.ubuntu.com/DailyUpstreamBuildsPOCSpec

The code for bzr-builder is here:
https://code.edge.launchpad.net/~james-w/bzr-builder/trunk

And a PPA of bzr-builder made with bzr-builder is here:
https://edge.launchpad.net/~dailydebs-team/+archive/bzr-builder

Some of the most used daily build PPAs are probably the [Mozilla Daily
Builds][] and  [Chromium Daily Builds][]. Along with the
[gwibber-daily][] PPA, these are run by [Fabien Tassin][]. The bash
scripts he uses to produce them can be found here:
https://code.edge.launchpad.net/~fta/+junk/ppa-scripts

[Project Neon][] has a [PPA][]delivering nighly builds of Amarok and
other KDE goodies. The build scripts are written in Ruby and hosted on
KDE's svn:
http://websvn.kde.org/trunk/extragear/multimedia/amarok/supplementary\_scripts/neon/

Anyone else doing something cool? Know where to find some more examples?


  [James Westby]: https://edge.launchpad.net/~james-w
  [Mozilla Daily Builds]: https://edge.launchpad.net/%7Eubuntu-mozilla-daily/+archive/ppa
  [Chromium Daily Builds]: https://edge.launchpad.net/%7Echromium-daily/+archive/ppa
  [gwibber-daily]: https://edge.launchpad.net/%7Egwibber-daily/+archive/ppa
  [Fabien Tassin]: https://code.edge.launchpad.net/%7Efta
  [Project Neon]: http://amarok.kde.org/wiki/User:Apachelogger/Project_Neon
  [PPA]: https://edge.launchpad.net/~project-neon/+archive/ppa
  [Just because everyone else is doing it...]: http://www.speedtest.net/result/492469146.png
    "Just because everyone else is doing it..."

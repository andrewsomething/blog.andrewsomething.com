Title: Bazaar Explorer 0.9.0 Now in PPA 
Date: 2009-11-04 04:26
Author: andrewsomething
Category: Uncategorized
Tags: bzr, explorer, ppa
Slug: bazaar-explorer-0-9-0-now-in-ppa

[![bzr icon][1]][2]

One of the things that I've always loved about bzr is that it is a
powerful yet intuitive solution for version control. Now [Bazaar
Explorer][2], a wonderful cross-platform Qt-based GUI front-end to
the Bazaar VCS, is making it even easier. Whether you're just getting
started with DVCS or you just prefer a graphical environment, you should
really check it out. (You can take a tour [here][].)

[![bzr-exploer screenshot][3]]

There's been a Windows installer for Bazaar Explorer for awhile, and of
course the source code is over there on [Launchpad][]. Even though
Bazaar's plugin system makes it simple to install it on Linux from
source, it just doesn't feel like it's keeping with the theme of making
things easy. So I went and packaged it for Ubuntu!

You can now grab it from the [Bazaar Explorer PPA][]. It should be
entering Debian Unstable and Ubuntu Lucid in the near future, but we
want to give you PPA users the chance to kick the tires first. Just add
**ppa:bzr-explorer-dev/ppa** to your system's Software Sources.

There are packages for Karmic, Jaunty, Intrepid, and Hardy in the PPA,
but please note that as bzr-explorer depends on bzr (\>= 1.14) and qbzr
(\>= 0.11), users of Ubuntu releases before Karmic will also need to add
the [PPA for Bazaar Developers][].  Also be aware that Hardy users might
have some issues as parts of Explorer (e.g. the Preferences dialog)
depend on Qt/PyQt 4.4.  (See:[Bug #429549][]). That said, every thing
should be working smoothly in Karmic.

  [1]: http://doc.bazaar-vcs.org/explorer/en/_static/bazaar-explorer-64.png
  [2]: http://doc.bazaar-vcs.org/explorer/en/
  [here]: http://doc.bazaar-vcs.org/explorer/en/visual-tour-gnome.html
  [3]: http://doc.bazaar-vcs.org/explorer/en/_static/home-page-screenshot.png
  [Launchpad]: https://edge.launchpad.net/bzr-explorer
  [Bazaar Explorer PPA]: https://edge.launchpad.net/~bzr-explorer-dev/+archive/ppa
  [PPA for Bazaar Developers]: https://edge.launchpad.net/~bzr/+archive/ppa
  [Bug #429549]: https://bugs.launchpad.net/bzr-explorer/+bug/429549

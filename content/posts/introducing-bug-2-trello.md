Title: Introducing Bug 2 Trello
Date: 2013-06-13 19:35
Author: andrewsomething
Category: Bug 2 Trello
Tags: app-development, bugs, chrome, trello
Slug: introducing-bug-2-trello

For some time now, I've been using [Trello][] to organize my free
software contributions. My main use is to give me a cross-project view
of what I'm working on. As most of my contributions stem from packaging
software for Debian and Ubuntu, I end up working on and following bugs
across many different hosting projects (e.g. Launchpad, Debian's BTS,
GitHub). Each does a decent job (some better than others) of displaying
and prioritizing issues within a certain project. Though a bug that is
critical in a project that I'm only tangentially interested in might be
a lower priority from me personally than a wishlist issue in a different
project. So Trello has been extremely helpful in giving me a global view
of how I should be spending my limited time across projects. Though
putting information from all of these different places into Trello can
be tedious...

So that's why I created [Bug 2 Trello,][] a Chrome extension to add
bugs/issues to a Trello board.

 

<iframe width="560" height="315" src="//www.youtube.com/embed/MMgeP0DH9c4" frameborder="0" allowfullscreen></iframe>

 

It currently supports Launchpad, GitHub, SourceForge, Google Code,
BitBucket, and Debian's BTS. There is also support for some Bugzilla
instances. This support currently requires that the JSON-RPC interface
is available. It is known to work with with Wikimedia, Mozilla, KDE,
Apache, and Redhat. It is known *not* to work with GNOME, Kernel.org,
and Novell.

-   Install it from the Chrome
    Store: <https://chrome.google.com/webstore/detail/bug2trello/aomnoofmdnaccffobkddehcmdihggcke>
-   Report bugs: <https://github.com/andrewsomething/bug2trello/issues>
-   Grab the
    code: `git clone git://github.com/andrewsomething/bug2trello.git`

Bug 2 Trello is licensed under the MIT License.

  [Trello]: https://trello.com/
  [Bug 2 Trello,]: https://chrome.google.com/webstore/detail/bug-2-trello/aomnoofmdnaccffobkddehcmdihggcke

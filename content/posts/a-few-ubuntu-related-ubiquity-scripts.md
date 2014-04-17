Title: A Few Ubuntu-related Ubiquity Scripts
Date: 2009-06-10 19:04
Author: andrewsomething
Category: Ubuntu
Tags: firefox, Ubuntu
Slug: a-few-ubuntu-related-ubiquity-scripts

Awhile back I hacked up a few Ubuntu releated scripts for Ubiquity. No,
not the Ubuntu installer. The Firefox add-on.  Now that I have one of
these fancy blog thing-a-majigs, I figured I'd share them with all of
you. Hopefully some one else will find them useful.

To make a long story short, [Ubiquity][] is GNOME-Do for your browser.

I've got a number of simple scripts that you can use with it to do
Ubuntu related tasks in Firefox:

-   AptURL - Install a package using AptURL. If you're reading a post
    about a package, just highlight the package name and call Ubiquity.
    No need to open a terminal or package manager. Usage: `apturl
    [package]`
-   Debian Package Search - One of the sites I end up using the most in
    my MOTU work is http://packages.debian.org/ This brings it just a
    keystroke away. Usage: `debian-packages [package]`
-   Launchpad Ubuntu Package Search - You guessed it. Search Ubuntu
    packages on LP. Usage: `lp-packages [package]`
-   Launchpad Team and People Search - What do you think it does? Usage:
    `lp-team-and-people [team or person]`
-   Launchpad Ubuntu Bug Search - Simular to the two above... 
    `lp-ubuntu-bug [bug \# or description]`
-   Ubuntu Man Page Search - Read the man page! Usage: `ubuntu-man
    [package]`
-   Ubuntu Package database searcher- This one searches
    packages.ubuntu.com It was written by David Futcher ([bobbo][]), and
    it was what inspired me to make all the others. Usage:
    `ubuntu-packages [package]`
-   Report Ubuntu Bug - Report a bug in a Ubuntu package on Launchpad.
    (Although, chances are you should really be using Apport.) Usage:
    `ubuntu-report-bug [package]`

You can grab them with:

    bzr branch lp:~andrewsomething/+junk/ubiquity-commands

  [Ubiquity]: http://labs.mozilla.com/projects/ubiquity/
  [bobbo]: https://edge.launchpad.net/~bobbo

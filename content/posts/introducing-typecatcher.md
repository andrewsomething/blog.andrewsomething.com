Title: Introducing TypeCatcher
Date: 2012-11-11 23:00
Author: andrewsomething
Category: TypeCatcher
Tags: app-development, quickly, typecatcher
Slug: introducing-typecatcher

![][1]

After helping to review applications for the Ubuntu App Showdown, I had
the urge to take another look at the state of quickly, Ubuntu's quick
starter for app development. So here we have [TypeCatcher][]. It allows
you to search, browse, and download Google webfonts for off-line use.
You can preview fonts with adjustable size and text.

It was mostly written in one Sunday afternoon a few months back. Though
I put it aside for awhile, mostly out of my inability to come up with a
name for it. The delay did allow me to flesh it out a bit. For the most
part I was quite happy with quickly. The templates really do get you up
and running fast. Though as I'm extremely comfortable with both bzr and
Debian packaging, I didn't really employ its ability to hide those parts
from users.

(As a side note, on place where quickly fell a bit short for me was
renaming the project. Sometimes you just want to start hacking and then
think about naming later, but quickly uses your project name in file
names and classes all over the place. It would be nice to bake project
renaming into its UI. There is already a [bug report about this on
Launchpad][]including a renaming script in the comments.)

After dogfooding the app writing tools, I think I'll probably test
the [submission process][] for the Ubuntu Extras repository as well. For
now though, you can install it for Ubuntu 12.10 from my PPA:

    sudo add-apt-repository ppa:andrewsomething/typecatcher
    sudo apt-get update && sudo apt-get install typecatcher

You can also grab the source from bzr on Launchpad:

    bzr branch lp:typecatcher

 

[Bugs and feature requests][] welcome there as well.

And of course, who doesn't love screenshots:

  ![][2]
  ![][3]
  ![][4]
  ![][5]
  ![][6]

 

  [1]: {filename}/images/2012/11/typecatcher_0012.png
  [TypeCatcher]: https://launchpad.net/typecatcher
  [bug report about this on Launchpad]: https://bugs.launchpad.net/quickly/+bug/667492
  [submission process]: http://developer.ubuntu.com/publish/
  [Bugs and feature requests]: https://bugs.launchpad.net/typecatcher
  [2]: {filename}/images/2012/11/selection_005.png
  [3]: {filename}/images/2012/11/typecatcher_003.png
  [4]: {filename}/images/2012/11/typecatcher_004.png
  [5]: {filename}/images/2012/11/typecatcher_006.png
  [6]: {filename}/images/2012/11/typecatcher_002.png


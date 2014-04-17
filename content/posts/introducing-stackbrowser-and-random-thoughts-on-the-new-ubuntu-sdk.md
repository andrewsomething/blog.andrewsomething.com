Title: Introducing StackBrowser (and random thoughts on the new Ubuntu SDK)
Date: 2013-09-12 21:57
Author: andrewsomething
Category: StackBrowser
Tags: app-development, askubuntu, qml, stackexchange, Ubuntu, ubuntu sdk
Slug: introducing-stackbrowser-and-random-thoughts-on-the-new-ubuntu-sdk


  ![][1]

If you follow me on Google+, you already know about this, but it seems
like it's time to introduce this to a larger audience. Mostly an excuse
to play with the new [Ubuntu SDK][], I've created StackBrowser. It
allows you to explore the StackExchange network natively on Ubuntu
Touch. It's written in pure QML/ JavaScript.

  ![][2]

Currently you can:

-   Browse and view recent questions
-   Search questions by tag
-   Browse, search, and view users

The roadmap for future releases includes a "convergence" layout (i.e
tablet/desktop view) and accessing your global inbox.

StackBrowser is available in the Ubuntu Touch Software Center. It can be
tested on a 13.10 Ubuntu desktop system, or on earlier releases if you
have the SDK installed, by grabbing its source from [Launchpad][]:

        bzr branch lp:stackbrowser
        cd stackbrowser
        qmlscene stackbrowser.qml

You can of course [report bugs there][] as well.

  ![][3]

Some random thoughts on the SDK and Ubuntu Touch apps
-----------------------------------------------------

-   I've enjoyed working with Qml for the most part. It's really quick
    and painless to build a nice UI. StackBrowser, admittedly not a very
    complex app, was built in a hour here and an hour there over the
    course of just a few days.
-   Though I think that I've still got a lot of learning to do about the
    "Qml way," if such a thing exists. I guess maybe the term I'm
    looking for is  "declarative nature."
-   I'd much rather write code in Python than JavaScript. [Hopefully that will be possible.][]
-   Relatedly, it feels like once an app becomes sufficiently ambitious,
    you need to use C++.
-   There are some very simple things you can't do in Qml/JS like write
    a file to disk.
-   There are places where there are strange holes in what you can do
    with Qml. For instance, you can [take pictures][], [record video][],
    and [play media][] all using pure QML.[Yet, I can't find any way to record audio with just QML.][] Maybe I'm missing something?
-   I've got an idea for a location aware app, but[I've found the docs to be very wanting.][]
-   There's a lot of great work going on in [the core apps project][],
    and it is very much a community effort.
-   The focus right now seems to be on the velocity of the development,
    but I'd like to see the core apps project become a more cohesive
    project (i.e. run more like say GNOME or KDE) and more integrated
    into Ubuntu governance.
-   I miss the larger collection of standard widgets available in Gtk.
-   Relate to the two above points,[I've noticed][] a couple place where
    some core apps  have different implementations of the same thing
    (e.g. location selection) with different visual styles and different
    behaviors.
-   Maybe it's just because most of my contributions to free software
    have been packaging things for Debian and Ubuntu, but the fact that
    people are being encouraged to bundle dependencies in click packages
    make me feel dirty.
-   That said, just clicking a button in QtCreator and attaching the
    result to a webform was extremely simple.
-   My app was available to install just a few hours after submission.
    Wonder how that will scale?

Wow, that was a bit stream of conscience like...

  [Ubuntu SDK]: http://developer.ubuntu.com/get-started/
  [Launchpad]: https://launchpad.net/stackbrowser
  [report bugs there]: https://bugs.launchpad.net/stackbrowser
  [Hopefully that will be possible.]: https://plus.google.com/102795169786046713434/posts/imZAq7pcdR8
  [take pictures]: http://qt-project.org/doc/qt-5.1/qtmultimedia/qml-qtmultimedia5-cameracapture.html
  [record video]: http://qt-project.org/doc/qt-5.1/qtmultimedia/qml-qtmultimedia5-camerarecorder.html
  [play media]: http://qt-project.org/doc/qt-5.1/qtmultimedia/qml-qtmultimedia5-mediaplayer.html
  [Yet, I can't find any way to record audio with just QML.]: http://askubuntu.com/questions/338610/access-microphone-record-sound-from-qml
  [I've found the docs to be very wanting.]: http://askubuntu.com/questions/344831/how-to-access-geolocation-information-on-ubuntu-touch
  [the core apps project]: https://launchpad.net/ubuntu-phone-coreapps
  [I've noticed]: https://lists.launchpad.net/ubuntu-phone/msg03972.html
  [1]: {filename}/images/2013/09/kazam_screenshot_00000.png
  [2]: {filename}/images/2013/09/kazam_screenshot_00001.png
  [3]: {filename}/images/2013/09/kazam_screenshot_00002.png

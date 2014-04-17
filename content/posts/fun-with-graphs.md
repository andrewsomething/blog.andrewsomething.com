Title: Fun with graphs
Date: 2011-10-09 20:01
Author: andrewsomething
Category: Ubuntu
Tags: community, mailinglists, stats, Ubuntu
Slug: fun-with-graphs

For awhile now, I've felt like the ubuntu-motu mailing list has been a
shadow of its former self. It turns out that empirical data backs up
this feeling. I produced a histogram of mailinglist volume over time:

![motu][1]

I also figured I should take a look at ubuntu-devel:

![devel][2]

That graph raises the question what happened at the end of 2006. Of
course, that was when ubuntu-devel-discuss was started:

![devel-discuss][3]

I'm not sure what this all means, but I do find it interesting in the
context of some recent discussion on the direction of the Ubuntu
community.

----

You can find the python code I used in a [GitHub gist][]. It takes an
mbox file and produces a histogram using [matplotlib][]. It is
shamelessly based off of [code by Takafumi Arakaki][] that was
designed to plot a histogram of the commit frequency of a Mercurial or
Git repository by reading newline separated unix time via STDIN. I just
rewrote the `read_dates()` function. If someone has a simpler way of
doing the date conversion, I'd love to see it. What I did was a
bit convoluted.

  [1]: {filename}/images/2011/10/motu.png
  [2]: {filename}/images/2011/10/devel.png
  [3]: {filename}/images/2011/10/devel-discuss.png
  [GitHub gist]: https://gist.github.com/1273952
  [matplotlib]: http://matplotlib.sourceforge.net/
  [code by Takafumi Arakaki]: https://gist.github.com/913543

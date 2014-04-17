Title: GPG key transition
Date: 2010-09-24 22:21
Author: andrewsomething
Category: Ubuntu
Tags: gpg, me
Slug: gpg-key-transition

I’ve recently set up a stronger (4096R) OpenPGP key, and will be
transitioning away from my old (1024D) one. The old key will continue to
be valid for some time, but i prefer all future correspondence to come
to the new one. I would also like this new key to be re-integrated into
the web of trust. Please find here [a statement signed with both
keys][], certifying the transition.

The old key was:

    pub 1024D/6286FB6D 2007-11-03 Key fingerprint = 62EE D4F4 6D46 BE9E FF02 220A 2F89 3E7C 6286 FB6D

And the new key is:

    pub 4096R/D53FDCB1 2010-09-24 Key fingerprint = 6EB2 23D7 D71E 67A5 3C93 A7DA 3B56 E2BB D53F DCB1

To fetch my new key from a public key server, you can simply do:

    gpg --keyserver pgp.mit.edu --recv-key D53FDCB1

If you already know my old key, you can now verify that the new key is
signed by the old one:

    gpg --check-sigs D53FDCB1

If you don't already know my old key, or you just want to be double
extra paranoid, you can check the fingerprint against the one above:

    gpg --fingerprint D53FDCB1

If you are satisfied that you've got the right key, and the UIDs match
what you expect, I'd appreciate it if you would sign my key:

    gpg --sign-key D53FDCB1

Lastly, if you could upload these signatures, i would appreciate it. You
can just upload the signatures to a public keyserver directly:

    gpg --keyserver pgp.mit.edu --send-key D53FDCB1

Thanks!

  [a statement signed with both keys]: http://people.ubuntu.com/~andrewsomething/key-transition-2010-09-24.txt

---
layout: post
title:  "Cloudflare Crypto Meetup"
date:   2014-07-24 18:24:52
categories: cryptography
---

I attended the [second cryptography meetup](http://www.meetup.com/CloudFlare-Meetups/events/191252182/)
at Cloudflare last Wednesday and was once again impressed by the turnout.
It was only the second talk and they've already had prominent members of
the crypto community speaking including [Adam Langley](https://imperialviolet.org)
from Google, Trevor Perrin who worked on TextSecure and Brian Warner from Mozilla.

The talks were all fantastic but Trevor's talk about application level encryption
and the challenges of group encryption the most interesting.  The challenge is
that there's no known protocol or algorithm for generating a shared secret key
among more than two individuals, although there has been [recent research](http://crypto.stanford.edu/~dabo/pubs/abstracts/obfuscationDH.html)
on the subject.  Additionally, TextSecure had some requirements specific to
the asynchronous nature of messaging and didn't introduce any new primitives to
accomplish their goal.  They instead use [racheting](https://whispersystems.org/blog/advanced-ratcheting/)
for key exchange and forward security which allows them to avoid establishing
a session between users.

All the talks from the first round can be found on [Cloudflare's YouTube channel](https://www.youtube.com/channel/UCgv3xMy6kECn0boYP9d2o-g),
and I expect the second round will be added before too long.

I'm looking forward to the next set of talks as I'll surely be attending them.

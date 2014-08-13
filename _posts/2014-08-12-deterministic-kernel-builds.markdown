---
layout: post
title:  "Deterministic Linux Kernel Builds"
date:   2014-08-11 23:59:59
categories: kernel linux
---

As an experiment I wanted to see if I could deterministically build the Linux
kernel twice in a row.  My goal was to have two kernels where the bzImage result
hashes to the same sha256 hash.

I saw that a patchset had been merged a while back[1], but the script provided
didn't work out of the box for me.  (And why should it!? It was written in 2011!)
It got me going in the right direction, which is all I needed to get it to work.


    #!/usr/bin/bash
    export INSTALL_MOD_STRIP=-s
    export KBUILD_BUILD_TIMESTAMP=0
    export KBUILD_BUILD_USER=root
    export KBUILD_BUILD_HOST=localhost
    make mrproper
    make allnoconfig
    make -j4

It's even much simpler than the original script, although the original did more
than just build the kernel.  Running this script twice in a row compiling for
x86\_64 with the same libraries (and versions) installed should result in the
same sha256 hashes.  I tried it on two different machines and a virtual machine
after updating my packages to the most recent versions.  Next I'll try some
configs other than allnoconfig, but it was just convenient and fastest to
compile.

[1] http://lwn.net/Articles/437864/

Some additional links on deterministic builds I found interesting:

https://blog.torproject.org/category/tags/deterministic-builds
https://archive.fosdem.org/2014/schedule/event/reproducibledebian/

---
layout: post
title:  "New Home Network Layout"
date:   2014-08-29 23:59:59
categories: networking pfsense openwrt
---

For a while now, I've wanted better insight into network behavior on my home network.
While I've been a long time advocate of OpenWRT as an alternative to proprietary
embedded management systems, it's frustrating to work with such limited hardware.
Things like logging and packet capture become cumbersome because you have to forward
those to other machines to consume, store or analyze.

So this lead me to begin looking at other options for a home router.  I thought about
implementing one myself, but I'm a sucker for nice web management interfaces and those
take time to do well.  So as a result, I settled on pfSense.  I already had an old i5
desktop which was collecting dust and shouldn't be, so I put it to work.

After downloading, verifying, and installing pfSense, I was happy to see that most of
the default configuration options were set to sane, secure values.  I already had a
new simple network architecture in mind: 2 subnets completely isolated from each other
but both having access to the WAN.  The HTPC and guest wifi network would reside on the
one subnet/vlan and my desktop, NAS and regular wifi would be on the other subnet/vlan.

So I set about figuring out how to configure OpenWRT to accomplish this.  Although
OpenWRT is generally very easy to configure since all files are using the same syntax
and reside in the same directory, I found it slightly difficult to understand what I
needed to do.  The main reason it was a bit challenging to me was because OpenWRT
abstracts away some of the details about what it does in the configuration files.  For
example, I wanted to bridge the guest access point with the guest vlan, but the area
where you configure the vlan and tagging isn't the same place where you bridge it with
the wireless network.

After getting the configuration down I wired it up and tested it offline, verifying
that a wireless client on the guest network couldn't communicate with my desktop and
that the trunk port was tagging vids correctly.  Finally, after backing up my configs,
I was ready to try it out and make the swap.

Despite double checking everything, when I brought up pfSense and OpenWRT after moving
them near the modem, it was clear something had gone horribly wrong.  Although pfSense
seemed to come up alright, I couldn't access OpenWRT through any physical ports.  Wifi
still worked though, which turns out kept me from having to factory reset and restore
from that backup I just made.  After some debugging, I found the issue was that I had
somehow left out tagging on the switch config for the CPU.  This resulted in OpenWRT
dropping the packets since it didn't have anywhere to send them.

Below you can find a diagram of my new configuration.  I'm fairly happy with it so far
and am extremely impressed with how easy it was to install and configure pfsense.

![Home Network]({{ site.url }}/images/homelab.png)

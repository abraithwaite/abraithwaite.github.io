---
layout: post
title:  "dhclient, resolvconf and Expected Behavior"
date:   2014-10-23 23:48:59
categories: linux networking
---

I came across an interesting problem recently which was made more complicated
by the lack of good documentation and the inability to narrow search results
due to broad search terms.  Additionally, it was made worse by the apparent
lack of understanding surrounding how these programs interact.

The problem had to do with the way that DNS resolution is handled on linux
systems: `/etc/resolv.conf` This file contains the nameservers glibc uses when
calling `getaddrinfo` in socket programming.  It's an interesting file not
because of its purpose though, but because of how many programs would like to
modify it: dnsmasq, bind, dhclient, vpns, proxies, etc.  This is the reason
`/sbin/resolvconf` (the script) was written.

From the resolvconf man page:

    resolvconf manages resolv.conf(5) files from multiple sources, such as DHCP
    and VPN clients.  Traditionally, the host runs just one client and that
    updates /etc/resolv.conf.  More modern systems frequently have wired and
    wireless interfaces and there is no guarantee both are on the same network.
    With the advent of VPN and other types of networking daemons, many things
    now contend for the contents of /etc/resolv.conf.

Now, the primary program using resolvconf, at least for Ubuntu, is generally
going to be dhclient.  dhclient doesn't use it directly though.  In fact,
dhclient has "dhclient-script" which calls hooks to update system
configuration.  dhclient-script was (probably?) written before resolvconf
though so dhclient-script implements it's own function to update
`/etc/resolv.conf`.

To get around dhclient-script's built-in update function (`make_resolv_conf`),
the resolvconf package provides a dhclient hook
(`/etc/dhcp/dhclient-enter-hooks.d/resolvconf`) which overrides the default
dhclient-script implementation and calls resolvconf instead.  So far, so good.
(Note: I didn't know this up front).

Now, onto my specific issue. It's common to run a private DNS server in cloud
deployments so you have complete flexibility when it comes to DNS.  However,
now you have to concern oneself with maintaining each instances nameservers.
'Not a problem!' you say.  You do a quick [google
search](https://encrypted.google.com/search?q=set+nameserver+ubuntu) on how to
add nameservers to an Ubuntu server.  Among the results:

- [Write them directly to resolv.conf](http://ubuntuforums.org/showthread.php?t=1972424)
- [Add the servers to /etc/resolv.conf.d/{base,head,tail}](http://ubuntuforums.org/showthread.php?t=2078398)
- [Modify /etc/network/interfaces](http://askubuntu.com/questions/346838/how-do-i-configure-my-dns-settings-in-ubuntu-server)
- [Add them to dhclient.conf](https://developers.google.com/speed/public-dns/docs/using)

Knowing about resolvconf, I read the manual and figured out that it suggests to
use either dhclient.conf or `/etc/network/interfaces` to make the changes to
the file.  Since this is a cloud deployment, I didn't want to make the changes
to `/etc/network/interfaces` because that requires running ifup / ifdown.  Not
good when you're doing everything remotely through either configuration
management or ssh.  So I go with dhclient.conf.

So I make the changes and run `dhclient -x -pf /var/run/dhclient.eth0.pid` to
stop dhclient without releasing the lease and then restart it with the same
arguments it was invoked with before.  Finally the nameservers changes are
reflected in `/etc/resolv.conf`.  I implement this in config management and I'm
on my way.  Sometime later on when a change had to be made to the nameservers,
it was time to update them again.  So I update it in configuration management
and apply the changes.  It's not long before a few servers go offline.  Turns
out, and I still haven't figured this out, but sometimes when running `dhclient
-x` it releases the current lease.  I'm not sure how or why this happens, it's
just what was observed.

So after spending a while trying to figure that out without making any
progress, I decide to go with the hacky way of doing things: without
resolvconf.  resolvconf shouldn't touch /etc/resolv.conf if it's not a symlink,
so I think I'm okay.  There is a `--disable-updates` option for resolvconf, but
I didn't notice it at this time.

Hours later, private names stop resolving and `/etc/resolv.conf` is back in the
state it was before I made the changes.  Not discouraged, I begin
investigating. I notice that the file was modified at the same time a lease was
renewed.  Knowing that dhclient calls resolvconf to update /etc/resolv.conf and
knowing that resolvconf should ignore the file if it's not a symlink, I'm
thoroughly confused.  I try reverting back to the previous method
(dhclient.conf), but I forgot to change the files back to symlinks.

That's when things got wild.  Not wanting `dhclient -x` to cause issues again,
I begin looking for alternative ways to update nameservers on a live dhcp-based
instance.  I found reading the dhclient manual that the leases are kept in a
plaintext file and I made the assumption that the last entry gets read when
renewing a current lease.  This kindof works, but kindof doesn't.  dhclient
holds on to the file descriptor of the first lease file it opened when it
started execution.  So if the file gets renamed or deleted, changes to the
leases file won't get recognized even if it's at the correct location.  Okay.
That was too fragile anyways.

Finally I look into why resolvconf is getting called when the file wasn't a
symlink.  This is when I noticed that the files weren't, in fact, symlinks (the
mistake I made above).  Further investigation revealed both how resolvconf
keeps dhclient-script from updating `/etc/resolv.conf` and the root cause.  The
root cause was that, even though `/sbin/resolvconf` checks to see if
`/etc/resolv.conf` is a symlink, so does
`/etc/dhcp/dhclient-enter-hooks.d/resolvconf`.  This is why the file could
still be updated even though it wasn't a symbolic link.  The hook checks to see
if the symlink exists _before_ it disables dhclient-script's built-in hook.

The end result is this: we disable updates by using `resolvconf
--disable-updates` and keep the file as a symlink.  The contents of
`/etc/resolv.conf` (really `/run/resolvconf/resolv.conf`) are under
configuration management.  I'm still not sure this is the best solution.  The
requirement that we be able to update nameservers without a restart and that
the file comes back in the correct state in the case of an unexpected restart
is something I would have expected others to have encountered.  Yet after
spending too much time looking for how others manage this, I found nothing.

What's more surprising is that `resolvconf --disable-updates` wasn't suggested
anywhere I looked.  I definitely read the man pages, but it wasn't clear that
this was the best way to accomplish what I was looking for.  I'm still unsure
about why `dhclient -x` caused a release, but I didn't see any unusual hooks
installed on the server (or perhaps I'm not looking in the right place).

[resolvconf](https://alioth.debian.org/projects/resolvconf/)

[Ubuntu bug report](https://bugs.launchpad.net/ubuntu/+source/resolvconf/+bug/1385010)

[dhclient](https://www.isc.org/downloads/DHCP/)

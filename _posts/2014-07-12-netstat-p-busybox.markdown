---
layout: post
title:  "`netstat -p` on busybox"
date:   2014-07-12 11:42:00
categories: networking linux
---

`netstat` is one of my favorite linux utilities and is always one of the first
tools I use when starting to debug any network related issues.  One of my
favorite options that netstat provides is the `-p` flag.  This flag is used
to see which programs are talking on which sockets.

On to the real problem.  I was investigating an issue with a OpenWrt router I
was having which was that it was listening on a port which I wasn't expecting.
I wanted to find the program which was holding this socket, but was disappointed
to find that the netstat packaged with busybox does not have the `-p` option!
Quelle Horreur!

To solve this, I decided to look into the proc filesystem to see if there was
anything of value.  The first thing I found was `/proc/net/tcp` which had some
useful information but not the program holding it.

```
root@OpenWrt:~# cat /proc/net/udp
  sl  local_address rem_address   st tx_queue rx_queue tr tm->when retrnsmt   uid  timeout inode
  34: 00000000:6922 00000000:0000 07 00000000:00000000 00:00000000 00000000 65534        0 2572701 2 80edd820
  53: 00000000:0035 00000000:0000 07 00000000:00000000 00:00000000 00000000     0        0 1126 2 8099c820
  67: 00000000:0043 00000000:0000 07 00000000:00000000 00:00000000 00000000     0        0 1123 2 8099cc00
```

The port in question that I was investigating was `67` which is the DHCP port which
I thought I had disabled, hence the investigation.

This file shows a number of things including the address/port combos for active
sockets and metadata about those sockets.  However, the most useful thing found
in this file was that it lists the inode of the socket.  Using the inode for
the socket, I can find which process has a reference to it by walking the
`/proc/{pid}/` tree and looking for that inode in the `/fd/` sub-tree for all
running processes.

```
root@OpenWrt:~# find /proc/ -type l | grep /fd/ | xargs ls -la 2>/dev/null | grep 1123
lrwx------    1 root     root           64 Dec 12 19:28 /proc/707/fd/5 -> socket:[1123]
```

Ahah!  Pid `707` is the culprit.  Now just who is this pid?

```
root@OpenWrt:~# ps w
  PID USER       VSZ STAT COMMAND
    1 root      1432 S    init
    2 root         0 SW   [keventd]
    3 root         0 RWN  [ksoftirqd_CPU0]
    4 root         0 SW   [kswapd]
    5 root         0 SW   [bdflush]
    6 root         0 SW   [kupdated]
    8 root         0 SW   [mtdblockd]
   94 root         0 SWN  [jffs2_gcd_mtd4]
  118 root      1432 S    init
  154 root      1440 S    syslogd -C16
  156 root      1424 S    klogd
  676 root      1108 S    /usr/sbin/dropbear -P /var/run/dropbear.1.pid -p 192.
  684 root       976 S    /usr/sbin/uhttpd -f -h /www -r OpenWrt -x /cgi-bin -t
  707 nobody     884 S    /usr/sbin/dnsmasq -K -D -y -Z -b -E -s lan -S /lan/ -
28001 root      1436 S    udhcpc -t 0 -i eth0.1 -b -p /var/run/dhcp-eth0.1.pid
 1573 root      1184 S    /usr/sbin/dropbear -P /var/run/dropbear.1.pid -p 192.
 1574 root      1440 S    -ash
 1873 root      1428 R    ps w
```

Of course, it is dnsmasq.  Now I have to find out why the configuration isn't
taking hold.  Anyways, it took longer to write this post than figure it out
but I'm forcing myself to write more and I thought it was cool, so there it is.

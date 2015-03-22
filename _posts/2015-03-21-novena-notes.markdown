---
layout: post
title:  "Novena first thoughts"
date:   2015-03-21 23:59:59
categories: novena linux hardware
---

I recently received my
[Novena](https://www.crowdsupply.com/kosagi/novena-open-laptop) desktop edition which I ordered during the crowdsupply campaign.  I've been anxiously awaiting
it since the beginning of February.

The box arrived in good condition with no obvious signs of being dropped or
damaged.  Opening it, I was greeted immediately with the schematics booklet
which I proceeded to show off to my coworkers.  I loved that the novena logo is
everywhere on the hardware too, it looks great.

[Assembly was
straightforward](http://www.kosagi.com/w/index.php?title=Desktop_User_Guide),
all that was necessary to boot was install the monitor.  After reading the
desktop assembly guide, I was sufficiently frightened of permanently damaging
the monitor but it wasn't really all that bad.  I did cause a bit of blanching
due to over-tightening but it was easily corrected by loosening up the screws.

The first boot went smoothly.  The setup required was minimal and fairly
typical (locale, keymap, etc).  I didn't have a whole lot of time to play with
it that night so I got it running then put it down till the weekend.The
Randomized name was a nice touch.  I ended up with 'novena-salsa-vision' which
I decided to keep for the novelty.

I booted it again this morning and had some circular artifacts and screen
tearing on the LCD.  My immediate first thought was that I had touched
something I shouldn't have, but that wasn't the case.  After running it for a
while, it just stopped occurring (perhaps it was the software update, but I
didn't have to reboot so I kind of doubt it).  I wish I had taken a quick video
of it; if it happens again I will.

This computer will be my go-to project board from now on.  I knew it would be
from the instant I saw it. Because the novena came with a
[myriad RF](https://myriadrf.org/projects/novena-rf/)
[breakout board](http://www.bunniestudios.com/blog/?p=3727) as part of the
stretch goals, the first thing I'm going to try doing with it is setup the SDR
module and start scanning the airwaves.  I'm new to SDR, so I'm really excited
to try it out!

Overall, I'm extremely satisfied so far with my new toy.  So much so that it
prompted me to actually write another post which should be a testament to my
excitement.  Perhaps one day writing these will become easier, for now I'm just
excited to get this up and running.

Thanks [Bunnie](https://twitter.com/bunniestudios) and
[Xobs](https://twitter.com/xobs) for organizing this awesome project!

![Novena Case]({{ site.url }}/images/novena1.jpg)
![Novena Closeup]({{ site.url }}/images/novena2.jpg)

dmesg:

    
    [    0.000000] Booting Linux on physical CPU 0x0
    [    0.000000] Initializing cgroup subsys cpuset
    [    0.000000] Initializing cgroup subsys cpu
    [    0.000000] Initializing cgroup subsys cpuacct
    [    0.000000] Linux version 3.17.0-rc5-00238-gfb115dd (xobs@xobs-novena-laptop) (gcc version 4.9.1 (Debian 4.9.1-19) ) #350 SMP PREEMPT Fri Dec 12 18:08:43 SGT 2014
    [    0.000000] CPU: ARMv7 Processor [412fc09a] revision 10 (ARMv7), cr=10c5387d
    [    0.000000] CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
    [    0.000000] Machine model: Kosagi Novena Dual/Quad
    [    0.000000] Ignoring memory range 0xffffffff - 0x100000000
    [    0.000000] cma: Reserved 256 MiB at 2f800000
    [    0.000000] Memory policy: Data cache writealloc
    [    0.000000] On node 0 totalpages: 983039
    [    0.000000] free_area_init_node: node 0, pgdat c0ad8d00, node_mem_map dd978000
    [    0.000000]   Normal zone: 1520 pages used for memmap
    [    0.000000]   Normal zone: 0 pages reserved
    [    0.000000]   Normal zone: 194560 pages, LIFO batch:31
    [    0.000000]   HighMem zone: 6160 pages used for memmap
    [    0.000000]   HighMem zone: 788479 pages, LIFO batch:31
    [    0.000000] PERCPU: Embedded 9 pages/cpu @dd926000 s12736 r8192 d15936 u36864
    [    0.000000] pcpu-alloc: s12736 r8192 d15936 u36864 alloc=9*4096
    [    0.000000] pcpu-alloc: [0] 0 [0] 1 [0] 2 [0] 3 
    [    0.000000] Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 981519
    [    0.000000] Kernel command line: console=ttymxc1,115200 init=/lib/systemd/systemd rootwait rw root=PARTUUID=4e6f764d-03 console=tty0
    [    0.000000] log_buf_len individual max cpu contribution: 65536 bytes
    [    0.000000] log_buf_len total cpu_extra contributions: 196608 bytes
    [    0.000000] log_buf_len min size: 131072 bytes
    [    0.000000] log_buf_len: 524288 bytes
    [    0.000000] early log buf free: 129264(98%)
    [    0.000000] PID hash table entries: 4096 (order: 2, 16384 bytes)
    [    0.000000] Dentry cache hash table entries: 131072 (order: 7, 524288 bytes)
    [    0.000000] Inode-cache hash table entries: 65536 (order: 6, 262144 bytes)
    [    0.000000] allocated 7864312 bytes of page_cgroup
    [    0.000000] please try 'cgroup_disable=memory' option if you don't want memory cgroups
    [    0.000000] Memory: 3617932K/3932156K available (7928K kernel code, 365K rwdata, 2300K rodata, 524K init, 338K bss, 314224K reserved, 3153916K highmem)
    [    0.000000] Virtual kernel memory layout:
        vector  : 0xffff0000 - 0xffff1000   (   4 kB)
        fixmap  : 0xffc00000 - 0xffe00000   (2048 kB)
        vmalloc : 0xf0000000 - 0xff000000   ( 240 MB)
        lowmem  : 0xc0000000 - 0xef800000   ( 760 MB)
        pkmap   : 0xbfe00000 - 0xc0000000   (   2 MB)
        modules : 0xbf000000 - 0xbfe00000   (  14 MB)
          .text : 0xc0008000 - 0xc0a05394   (10229 kB)
          .init : 0xc0a06000 - 0xc0a891c0   ( 525 kB)
          .data : 0xc0a8a000 - 0xc0ae54ec   ( 366 kB)
           .bss : 0xc0ae54ec - 0xc0b39e64   ( 339 kB)
    [    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1
    [    0.000000] Preemptible hierarchical RCU implementation.
    [    0.000000] NR_IRQS:16 nr_irqs:16 16
    [    0.000000] L2C-310 erratum 769419 enabled
    [    0.000000] L2C-310 enabling early BRESP for Cortex-A9
    [    0.000000] L2C-310 full line of zeros enabled for Cortex-A9
    [    0.000000] L2C-310 ID prefetch enabled, offset 1 lines
    [    0.000000] L2C-310 dynamic clock gating enabled, standby mode enabled
    [    0.000000] L2C-310 cache controller enabled, 16 ways, 1024 kB
    [    0.000000] L2C-310: CACHE_ID 0x410000c7, AUX_CTRL 0x76070001
    [    0.000000] Switching to timer-based delay loop, resolution 15ns
    [    0.000008] sched_clock: 32 bits at 66MHz, resolution 15ns, wraps every 65075262448ns
    [    0.001490] Console: colour dummy device 80x30
    [    0.002638] console [tty0] enabled
    [    0.002672] Calibrating delay loop (skipped), value calculated using timer frequency.. 132.00 BogoMIPS (lpj=660000)
    [    0.002728] pid_max: default: 32768 minimum: 301
    [    0.002882] Mount-cache hash table entries: 2048 (order: 1, 8192 bytes)
    [    0.002920] Mountpoint-cache hash table entries: 2048 (order: 1, 8192 bytes)
    [    0.003628] Initializing cgroup subsys memory
    [    0.003677] Initializing cgroup subsys devices
    [    0.003711] Initializing cgroup subsys freezer
    [    0.003743] Initializing cgroup subsys blkio
    [    0.003773] Initializing cgroup subsys perf_event
    [    0.003841] CPU: Testing write buffer coherency: ok
    [    0.003892] ftrace: allocating 25965 entries in 77 pages
    [    0.048106] CPU0: thread -1, cpu 0, socket 0, mpidr 80000000
    [    0.048247] Setting up static identity map for 0x1072d958 - 0x1072d9b0
    [    0.120483] CPU1: Booted secondary processor
    [    0.120517] CPU1: thread -1, cpu 1, socket 0, mpidr 80000001
    [    0.140476] CPU2: Booted secondary processor
    [    0.140502] CPU2: thread -1, cpu 2, socket 0, mpidr 80000002
    [    0.160493] CPU3: Booted secondary processor
    [    0.160518] CPU3: thread -1, cpu 3, socket 0, mpidr 80000003
    [    0.160606] Brought up 4 CPUs
    [    0.160708] SMP: Total of 4 processors activated.
    [    0.160727] CPU: All CPU(s) started in SVC mode.
    [    0.161458] devtmpfs: initialized
    [    0.165132] VFP support v0.3: implementor 41 architecture 3 part 30 variant 9 rev 4
    [    0.179207] pinctrl core: initialized pinctrl subsystem
    [    0.179634] regulator-dummy: no parameters
    [    0.189436] NET: Registered protocol family 16
    [    0.191927] DMA: preallocated 256 KiB pool for atomic coherent allocations
    [    0.193018] cpuidle: using governor ladder
    [    0.193051] cpuidle: using governor menu
    [    0.193198] CPU identified as i.MX6Q, silicon rev 1.2
    [    0.201361] vdd1p1: 800 <--> 1375 mV at 1100 mV 
    [    0.201805] vdd3p0: 2800 <--> 3150 mV at 3000 mV 
    [    0.202248] vdd2p5: 2000 <--> 2750 mV at 2400 mV 
    [    0.202686] vddarm: 725 <--> 1450 mV at 1150 mV 
    [    0.203134] vddpu: 725 <--> 1450 mV at 1150 mV 
    [    0.203577] vddsoc: 725 <--> 1450 mV at 1175 mV 
    [    0.213222] No ATAGs?
    [    0.213272] hw-breakpoint: found 5 (+1 reserved) breakpoint and 1 watchpoint registers.
    [    0.213306] hw-breakpoint: maximum watchpoint size is 4 bytes.
    [    0.213897] imx6q-pinctrl 20e0000.iomuxc: initialized IMX pinctrl driver
    [    0.251726] 2P5V: 2500 mV 
    [    0.251818] reg-fixed-voltage regulators:2p5v: 2P5V supplying 2500000uV
    [    0.252010] 3P3V: 3300 mV 
    [    0.252084] reg-fixed-voltage regulators:3p3v: 3P3V supplying 3300000uV
    [    0.252275] usb_otg_vbus: 5000 mV 
    [    0.252349] reg-fixed-voltage regulators:usb_otg_vbus: usb_otg_vbus supplying 5000000uV
    [    0.660521] es8328-power: 5000 mV 
    [    0.660618] reg-fixed-voltage regulators:es8328-regulator: es8328-power supplying 5000000uV
    [    0.660820] lcd-lvds-power: 3300 mV 
    [    0.660898] reg-fixed-voltage regulators:lcd-regulator: lcd-lvds-power supplying 3300000uV
    [    0.661104] lcd-display-power: 3300 mV 
    [    0.661203] reg-fixed-voltage regulators:display-regulator: lcd-display-power supplying 3300000uV
    [    0.680519] sata-power: 3300 mV 
    [    0.680601] reg-fixed-voltage regulators:sata-regulator: sata-power supplying 3300000uV
    [    0.681085] vgaarb: loaded
    [    0.681462] SCSI subsystem initialized
    [    0.681547] libata version 3.00 loaded.
    [    0.681848] usbcore: registered new interface driver usbfs
    [    0.681943] usbcore: registered new interface driver hub
    [    0.682094] usbcore: registered new device driver usb
    [    0.683955] stmpe-i2c 0-0044: Looking up vcc-supply from device tree
    [    0.684047] stmpe-i2c 0-0044: Looking up vio-supply from device tree
    [    0.684945] stmpe-i2c 0-0044: stmpe811 detected, chip id: 0x811
    [    0.687717] i2c i2c-0: IMX I2C adapter registered
    [    0.688396] i2c i2c-1: IMX I2C adapter registered
    [    0.689695] i2c i2c-2: IMX I2C adapter registered
    [    0.689879] pps_core: LinuxPPS API ver. 1 registered
    [    0.689901] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
    [    0.689955] PTP clock support registered
    [    0.690369] Advanced Linux Sound Architecture Driver Initialized.
    [    0.691511] Bluetooth: Core ver 2.19
    [    0.691572] NET: Registered protocol family 31
    [    0.691591] Bluetooth: HCI device and connection manager initialized
    [    0.691626] Bluetooth: HCI socket layer initialized
    [    0.691652] Bluetooth: L2CAP socket layer initialized
    [    0.691699] Bluetooth: SCO socket layer initialized
    [    0.692267] cfg80211: Calling CRDA to update world regulatory domain
    [    0.692617] Switched to clocksource mxc_timer1
    [    0.724489] FS-Cache: Loaded
    [    0.724909] imx6q-pcie 1ffc000.pcie: missing *config* reg space
    [    0.846229] imx6q-pcie 1ffc000.pcie: PCI host bridge to bus 0000:00
    [    0.846266] pci_bus 0000:00: root bus resource [io  0x1000-0x10000]
    [    0.846292] pci_bus 0000:00: root bus resource [mem 0x01000000-0x01efffff]
    [    0.846320] pci_bus 0000:00: No busn resource found for root bus, will use [bus 00-ff]
    [    0.846381] pci 0000:00:00.0: [16c3:abcd] type 01 class 0x060400
    [    0.846415] pci 0000:00:00.0: reg 0x10: [mem 0x00000000-0x000fffff]
    [    0.846437] pci 0000:00:00.0: reg 0x38: [mem 0x00000000-0x0000ffff pref]
    [    0.846501] pci 0000:00:00.0: supports D1
    [    0.846513] pci 0000:00:00.0: PME# supported from D0 D1 D3hot D3cold
    [    0.846822] PCI: bus0: Fast back to back transfers disabled
    [    0.847087] pci 0000:01:00.0: [168c:0034] type 00 class 0x028000
    [    0.847201] pci 0000:01:00.0: reg 0x10: [mem 0x00000000-0x0007ffff 64bit]
    [    0.847377] pci 0000:01:00.0: reg 0x30: [mem 0x00000000-0x0000ffff pref]
    [    0.847614] pci 0000:01:00.0: supports D1
    [    0.847627] pci 0000:01:00.0: PME# supported from D0 D1 D3hot
    [    0.862725] PCI: bus1: Fast back to back transfers disabled
    [    0.862760] pci_bus 0000:01: busn_res: [bus 01-ff] end is updated to 01
    [    0.862779] pci_bus 0000:00: busn_res: [bus 00-ff] end is updated to 01
    [    0.862900] pci 0000:00:00.0: BAR 0: assigned [mem 0x01000000-0x010fffff]
    [    0.862937] pci 0000:00:00.0: BAR 14: assigned [mem 0x01100000-0x011fffff]
    [    0.862966] pci 0000:00:00.0: BAR 15: assigned [mem 0x01200000-0x012fffff pref]
    [    0.862997] pci 0000:00:00.0: BAR 6: assigned [mem 0x01300000-0x0130ffff pref]
    [    0.863031] pci 0000:01:00.0: BAR 0: assigned [mem 0x01100000-0x0117ffff 64bit]
    [    0.863111] pci 0000:01:00.0: BAR 6: assigned [mem 0x01200000-0x0120ffff pref]
    [    0.863142] pci 0000:00:00.0: PCI bridge to [bus 01]
    [    0.863169] pci 0000:00:00.0:   bridge window [mem 0x01100000-0x011fffff]
    [    0.863196] pci 0000:00:00.0:   bridge window [mem 0x01200000-0x012fffff pref]
    [    0.863247] pci 0000:00:00.0: PCI bridge to [bus 01]
    [    0.863274] pci 0000:00:00.0:   bridge window [mem 0x01100000-0x011fffff]
    [    0.863300] pci 0000:00:00.0:   bridge window [mem 0x01200000-0x012fffff pref]
    [    0.863333] pci_bus 0000:00: resource 4 [io  0x1000-0x10000]
    [    0.863344] pci_bus 0000:00: resource 5 [mem 0x01000000-0x01efffff]
    [    0.863356] pci_bus 0000:01: resource 1 [mem 0x01100000-0x011fffff]
    [    0.863367] pci_bus 0000:01: resource 2 [mem 0x01200000-0x012fffff pref]
    [    0.876512] NET: Registered protocol family 2
    [    0.877266] TCP established hash table entries: 8192 (order: 3, 32768 bytes)
    [    0.877370] TCP bind hash table entries: 8192 (order: 4, 65536 bytes)
    [    0.877513] TCP: Hash tables configured (established 8192 bind 8192)
    [    0.877603] TCP: reno registered
    [    0.877631] UDP hash table entries: 512 (order: 2, 16384 bytes)
    [    0.877700] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes)
    [    0.877961] NET: Registered protocol family 1
    [    0.878056] PCI: CLS 64 bytes, default 64
    [    0.878639] hw perfevents: enabled with armv7_cortex_a9 PMU driver, 7 counters available
    [    0.881905] futex hash table entries: 1024 (order: 4, 65536 bytes)
    [    0.882122] audit: initializing netlink subsys (disabled)
    [    0.882187] audit: type=2000 audit(0.859:1): initialized
    [    0.891302] zpool: loaded
    [    0.891339] zbud: loaded
    [    0.893460] squashfs: version 4.0 (2009/01/31) Phillip Lougher
    [    0.894910] fuse init (API version 7.23)
    [    0.896478] pstore: Registered eepromoops as persistent store backend
    [    0.896576] msgmni has been set to 1418
    [    0.898344] NET: Registered protocol family 38
    [    0.898476] bounce: pool size: 64 pages
    [    0.898718] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 249)
    [    0.898763] io scheduler noop registered (default)
    [    0.898794] io scheduler deadline registered
    [    0.899016] io scheduler cfq registered
    [    0.901088] pcieport 0000:00:00.0: Signaling PME through PCIe PME interrupt
    [    0.901124] pci 0000:01:00.0: Signaling PME through PCIe PME interrupt
    [    0.901155] pcie_pme 0000:00:00.0:pcie01: service driver pcie_pme loaded
    [    0.901605] pwm-backlight backlight: Looking up power-supply from device tree
    [    0.902963] imx-sdma 20ec000.sdma: Direct firmware load for imx/sdma/sdma-imx6q.bin failed with error -2
    [    0.903008] imx-sdma 20ec000.sdma: firmware not found
    [    0.906209] imx-sdma 20ec000.sdma: initialized
    [    0.908051] pfuze100-regulator 1-0008: Full layer: 2, Metal layer: 1
    [    0.908672] pfuze100-regulator 1-0008: FAB: 0, FIN: 0
    [    0.908697] pfuze100-regulator 1-0008: identify took 1 tries
    [    0.908720] pfuze100-regulator 1-0008: pfuze100 found.
    [    0.910262] SW1AB: 300 <--> 1875 mV at 1375 mV 
    [    0.911085] SW1C: 300 <--> 1875 mV at 1375 mV 
    [    0.911928] SW2: 800 <--> 3300 mV at 3000 mV 
    [    0.912792] SW3A: 400 <--> 1975 mV at 1500 mV 
    [    0.913619] SW3B: 400 <--> 1975 mV at 1500 mV 
    [    0.914429] SW4: override max_uV, 3300000 -> 1975000
    [    0.914445] SW4: 800 <--> 1975 mV at 1800 mV 
    [    0.915686] SWBST: 5000 <--> 5150 mV at 5000 mV 
    [    0.916927] VSNVS: 1000 <--> 3000 mV at 3000 mV 
    [    0.917163] VREFDDR: override min_uV, 1 -> 750000
    [    0.917176] VREFDDR: override max_uV, 2147483647 -> 750000
    [    0.917781] VREFDDR: 750 mV 
    [    0.918571] VGEN1: 800 <--> 1550 mV at 800 mV 
    [    0.919377] VGEN2: 800 <--> 1550 mV at 1500 mV 
    [    0.920175] VGEN3: 1800 <--> 3300 mV at 1800 mV 
    [    0.920976] VGEN4: 1800 <--> 3300 mV at 1800 mV 
    [    0.921815] VGEN5: 1800 <--> 3300 mV at 2500 mV 
    [    0.922646] VGEN6: 1800 <--> 3300 mV at 2800 mV 
    [    0.999142] Serial: IMX driver
    [    0.999734] 21e8000.serial: ttymxc1 at MMIO 0x21e8000 (irq = 59, base_baud = 5000000) is a IMX
    [    2.025661] console [ttymxc1] enabled
    [    2.029878] 21ec000.serial: ttymxc2 at MMIO 0x21ec000 (irq = 60, base_baud = 5000000) is a IMX
    [    2.039110] 21f0000.serial: ttymxc3 at MMIO 0x21f0000 (irq = 61, base_baud = 5000000) is a IMX
    [    2.048255] [drm] Initialized drm 1.1.0 20060810
    [    2.053073] it6251 2-005c: Looking up power-supply from device tree
    [    2.315564] dummy 2-005e: error -5 writing to lvds addr 0x5
    [    2.565043] Galcore version 4.6.9.9754
    [    2.568833] galcore 130000.gpu: Looking up pu-supply from device tree
    [    2.595825] ipu_smfc_init: ioremap 0x02650000 -> f00ce000
    [    2.596375] imx-ipuv3 2400000.ipu: IPUv3H probed
    [    2.601345] ipu_smfc_init: ioremap 0x02a50000 -> f011e000
    [    2.601854] imx-ipuv3 2800000.ipu: IPUv3H probed
    [    2.614307] brd: module loaded
    [    2.621350] loop: module loaded
    [    2.627536] senoko 0-0020: Senoko 'S' version 2.0 (features: 0x02)
    [    2.633781] senoko 0-0020: GPIO IRQ: 20
    [    2.637641] senoko 0-0020: GPIO IRQ trigger: 0
    [    2.643311] ahci-imx 2200000.sata: fsl,transmit-level-mV value 1025, using 00000024
    [    2.651008] ahci-imx 2200000.sata: fsl,transmit-boost-mdB value 0, using 00000000
    [    2.658545] ahci-imx 2200000.sata: fsl,transmit-atten-16ths value 8, using 00002800
    [    2.666249] ahci-imx 2200000.sata: fsl,receive-eq-mdB not specified, using 05000000
    [    2.673968] ahci-imx 2200000.sata: Looking up target-supply from device tree
    [    2.676867] ahci-imx 2200000.sata: SSS flag set, parallel bus scan disabled
    [    2.681550] it6251 2-005c: RPCLKCnt: 1025
    [    2.682257] it6251 2-005c: System status: 0x3a
    [    2.683685] it6251 2-005c: Clock: 0x193
    [    2.684395] it6251 2-005c: Ref Link State: 0x00
    [    2.684403] it6251 2-005c: Display didn't stabilize.  This may be because the LVDS port is still in powersave mode.
    [    2.684410] it6251 2-005c: Will try again in 100 msecs
    [    2.716428] ahci-imx 2200000.sata: AHCI 0001.0300 32 slots 1 ports 3 Gbps 0x1 impl platform mode
    [    2.725267] ahci-imx 2200000.sata: flags: ncq sntf stag pm led clo only pmp pio slum part ccc apst 
    [    2.735869] scsi host0: ahci_platform
    [    2.739949] ata1: SATA max UDMA/133 mmio [mem 0x02200000-0x02203fff] port 0x100 irq 71
    [    2.749745] spi_imx 2010000.ecspi: probed
    [    2.755195] libphy: Fixed MDIO Bus: probed
    [    2.760528] fec 2188000.ethernet: Looking up phy-supply from device tree
    [    2.760547] fec 2188000.ethernet: Looking up phy-supply property in node /soc/aips-bus@02100000/ethernet@02188000 failed
    [    2.760570] 2188000.ethernet supply phy not found, using dummy regulator
    [    2.785613] dummy 2-005e: error -5 writing to lvds addr 0x5
    [    2.793657] libphy: fec_enet_mii_bus: probed
    [    2.798544] fec 2188000.ethernet eth0: registered PHC device 0
    [    2.804733] ath9k 0000:01:00.0: enabling device (0140 -> 0142)
    [    2.820531] ath: EEPROM regdomain: 0x60
    [    2.820541] ath: EEPROM indicates we should expect a direct regpair map
    [    2.820556] ath: Country alpha2 being used: 00
    [    2.820562] ath: Regpair used: 0x60
    [    2.832071] ieee80211 phy0: Selected rate control algorithm 'minstrel_ht'
    [    2.833622] ieee80211 phy0: Atheros AR9462 Rev:2 mem=0xf0300000, irq=155
    [    2.840477] pegasus: v0.9.3 (2013/04/25), Pegasus/Pegasus II USB Ethernet driver
    [    2.847990] usbcore: registered new interface driver pegasus
    [    2.853801] usbcore: registered new interface driver asix
    [    2.859284] usbcore: registered new interface driver ax88179_178a
    [    2.865480] usbcore: registered new interface driver cdc_ether
    [    2.871391] usbcore: registered new interface driver cdc_eem
    [    2.877179] usbcore: registered new interface driver smsc75xx
    [    2.883045] usbcore: registered new interface driver smsc95xx
    [    2.888870] usbcore: registered new interface driver net1080
    [    2.894627] usbcore: registered new interface driver cdc_subset
    [    2.900677] usbcore: registered new interface driver cdc_ncm
    [    2.906434] ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
    [    2.913014] ehci-pci: EHCI PCI platform driver
    [    2.917548] ehci-platform: EHCI generic platform driver
    [    2.923219] usbcore: registered new interface driver usb-storage
    [    2.929404] usbcore: registered new interface driver usbserial
    [    2.935329] usbcore: registered new interface driver usbserial_generic
    [    2.941925] usbserial: USB Serial support registered for generic
    [    2.948033] usbcore: registered new interface driver usb_serial_simple
    [    2.954644] usbserial: USB Serial support registered for zio
    [    2.960364] usbserial: USB Serial support registered for funsoft
    [    2.966447] usbserial: USB Serial support registered for flashloader
    [    2.972882] usbserial: USB Serial support registered for vivopay
    [    2.978951] usbserial: USB Serial support registered for moto_modem
    [    2.985297] usbserial: USB Serial support registered for hp4x
    [    2.991104] usbserial: USB Serial support registered for suunto
    [    2.997102] usbserial: USB Serial support registered for siemens_mpi
    [    3.004886] imx_usb 2184000.usb: Looking up vbus-supply from device tree
    [    3.005188] ci_hdrc ci_hdrc.0: ChipIdea HDRC found, lpm: 0; cap: f012e100 op: f012e140
    [    3.008172] ci_hdrc ci_hdrc.0: It is OTG capable controller
    [    3.009117] imx_usb 2184200.usb: Looking up vbus-supply from device tree
    [    3.009397] ci_hdrc ci_hdrc.1: ChipIdea HDRC found, lpm: 0; cap: f0136300 op: f0136340
    [    3.012911] ci_hdrc ci_hdrc.1: doesn't support gadget
    [    3.018003] ci_hdrc ci_hdrc.1: EHCI Host Controller
    [    3.022951] ci_hdrc ci_hdrc.1: new USB bus registered, assigned bus number 1
    [    3.042657] ci_hdrc ci_hdrc.1: USB 2.0 started, EHCI 1.00
    [    3.048291] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002
    [    3.055135] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
    [    3.062388] usb usb1: Product: EHCI Host Controller
    [    3.067302] usb usb1: Manufacturer: Linux 3.17.0-rc5-00238-gfb115dd ehci_hcd
    [    3.074389] usb usb1: SerialNumber: ci_hdrc.1
    [    3.079553] hub 1-0:1.0: USB hub found
    [    3.083389] hub 1-0:1.0: 1 port detected
    [    3.088269] mousedev: PS/2 mouse device common for all mice
    [    3.094461] input: 20b8000.kpp as /devices/soc0/soc/2000000.aips-bus/20b8000.kpp/input/input0
    [    3.102657] ata1: SATA link down (SStatus 0 SControl 300)
    [    3.102704] ahci-imx 2200000.sata: no device found, disabling link.
    [    3.102710] ahci-imx 2200000.sata: pass ahci_imx..hotplug=1 to enable hotplug
    [    3.123357] input: Senoko keypad as /devices/soc0/soc/2100000.aips-bus/21a0000.i2c/i2c-0/0-0020/senoko-keypad.1/input/input1
    [    3.135047] usbcore: registered new interface driver appletouch
    [    3.141094] usbcore: registered new interface driver bcm5974
    [    3.150236] it6251 2-005c: RPCLKCnt: 1025
    [    3.155039] it6251 2-005c: System status: 0x3a
    [    3.155141] rtc-pcf8523 0-0068: rtc core: registered rtc-pcf8523 as rtc0
    [    3.155735] snvs_rtc 20cc034.snvs-rtc-lp: rtc core: registered 20cc034.snvs-rtc-lp as rtc1
    [    3.155868] i2c /dev entries driver
    [    3.179580] it6251 2-005c: Clock: 0x193
    [    3.184187] it6251 2-005c: Ref Link State: 0x00
    [    3.188758] it6251 2-005c: Display didn't stabilize.  This may be because the LVDS port is still in powersave mode.
    [    3.199260] it6251 2-005c: Will try again in 150 msecs
    [    3.212434] sbs-battery 0-000b: sbs_probe: Failed to get device status
    [    3.219027] sbs-battery: probe of 0-000b failed with error -5
    [    3.226982] imx2-wdt 20bc000.wdog: timeout 60 sec (nowayout=0)
    [    3.233105] usbcore: registered new interface driver bcm203x
    [    3.238868] usbcore: registered new interface driver btusb
    [    3.244496] usbcore: registered new interface driver ath3k
    [    3.250190] sdhci: Secure Digital Host Controller Interface driver
    [    3.256416] sdhci: Copyright(c) Pierre Ossman
    [    3.260801] sdhci-pltfm: SDHCI platform and OF driver helper
    [    3.267305] sdhci-esdhc-imx 2194000.usdhc: could not get ultra high speed state, work on normal mode
    [    3.277754] sdhci-esdhc-imx 2194000.usdhc: Looking up vmmc-supply from device tree
    [    3.277774] sdhci-esdhc-imx 2194000.usdhc: Looking up vmmc-supply property in node /soc/aips-bus@02100000/usdhc@02194000 failed
    [    3.277803] sdhci-esdhc-imx 2194000.usdhc: Looking up vqmmc-supply from device tree
    [    3.277818] sdhci-esdhc-imx 2194000.usdhc: Looking up vqmmc-supply property in node /soc/aips-bus@02100000/usdhc@02194000 failed
    [    3.277832] sdhci-esdhc-imx 2194000.usdhc: No vmmc regulator found
    [    3.284080] sdhci-esdhc-imx 2194000.usdhc: No vqmmc regulator found
    [    3.291640] sdhci-esdhc-imx 2194000.usdhc: Looking up card-external-vcc-supply from device tree
    [    3.291659] sdhci-esdhc-imx 2194000.usdhc: Looking up card-external-vcc-supply property in node /soc/aips-bus@02100000/usdhc@02194000 failed
    [    3.291674] 2194000.usdhc supply card-external-vcc not found, using dummy regulator
    [    3.355603] dummy 2-005e: error -5 writing to lvds addr 0x5
    [    3.392657] mmc0: SDHCI controller on 2194000.usdhc [2194000.usdhc] using ADMA
    [    3.400301] sdhci-esdhc-imx 2198000.usdhc: could not get ultra high speed state, work on normal mode
    [    3.402712] usb 1-1: new high-speed USB device number 2 using ci_hdrc
    [    3.416133] sdhci-esdhc-imx 2198000.usdhc: Looking up vmmc-supply from device tree
    [    3.416153] sdhci-esdhc-imx 2198000.usdhc: Looking up vmmc-supply property in node /soc/aips-bus@02100000/usdhc@02198000 failed
    [    3.416176] sdhci-esdhc-imx 2198000.usdhc: Looking up vqmmc-supply from device tree
    [    3.416190] sdhci-esdhc-imx 2198000.usdhc: Looking up vqmmc-supply property in node /soc/aips-bus@02100000/usdhc@02198000 failed
    [    3.416204] sdhci-esdhc-imx 2198000.usdhc: No vmmc regulator found
    [    3.422411] sdhci-esdhc-imx 2198000.usdhc: No vqmmc regulator found
    [    3.429002] sdhci-esdhc-imx 2198000.usdhc: Looking up card-external-vcc-supply from device tree
    [    3.429025] sdhci-esdhc-imx 2198000.usdhc: Looking up card-external-vcc-supply property in node /soc/aips-bus@02100000/usdhc@02198000 failed
    [    3.429040] 2198000.usdhc supply card-external-vcc not found, using dummy regulator
    [    3.532660] mmc1: SDHCI controller on 2198000.usdhc [2198000.usdhc] using ADMA
    [    3.540651] ledtrig-cpu: registered to indicate activity on CPUs
    [    3.546840] hidraw: raw HID events driver (C) Jiri Kosina
    [    3.552538] usbcore: registered new interface driver usbhid
    [    3.558156] usbhid: USB HID core driver
    [    3.558751] usb 1-1: New USB device found, idVendor=05e3, idProduct=0614
    [    3.558761] usb 1-1: New USB device strings: Mfr=0, Product=1, SerialNumber=0
    [    3.558768] usb 1-1: Product: USB2.0 Hub Charger
    [    3.561365] hub 1-1:1.0: USB hub found
    [    3.561788] hub 1-1:1.0: 4 ports detected
    [    3.590222] [drm] Supports vblank timestamp caching Rev 2 (21.10.2013).
    [    3.591687] mmc1: host does not support reading read-only switch. assuming write-enable.
    [    3.599333] mmc1: new high speed SDHC card at address e624
    [    3.599757] mmcblk0: mmc1:e624 SS16G 14.8 GiB 
    [    3.601177]  mmcblk0: p1 p2 p3
    [    3.618070] [drm] No driver support for vblank timestamp query.
    [    3.624145] imx-drm display-subsystem: bound imx-ipuv3-crtc.0 (ops ipu_crtc_ops)
    [    3.631657] imx-drm display-subsystem: bound imx-ipuv3-crtc.4 (ops ipu_crtc_ops)
    [    3.639194] imx-drm display-subsystem: bound imx-ipuv3-crtc.5 (ops ipu_crtc_ops)
    [    3.646732] imx-drm display-subsystem: bound imx-ipuv3-crtc.1 (ops ipu_crtc_ops)
    [    3.654421] imx-hdmi 120000.hdmi: Detected HDMI controller 0x13:0xa:0xa0:0xc1
    [    3.662053] imx-drm display-subsystem: bound 120000.hdmi (ops hdmi_ops)
    [    3.668946] imx-ldb 2000000.aips-bus:ldb@020e0008: dual-channel mode, ignoring second output
    [    3.677459] imx-drm display-subsystem: bound 2000000.aips-bus:ldb@020e0008 (ops imx_ldb_ops)
    [    3.723459] Console: switching to colour frame buffer device 240x67
    [    3.729024] it6251 2-005c: RPCLKCnt: 1025
    [    3.729732] it6251 2-005c: System status: 0x3a
    [    3.731135] it6251 2-005c: Clock: 0x193
    [    3.731844] it6251 2-005c: Ref Link State: 0x00
    [    3.731851] it6251 2-005c: Display didn't stabilize.  This may be because the LVDS port is still in powersave mode.
    [    3.731857] it6251 2-005c: Will try again in 200 msecs
    [    3.776073] imx-drm display-subsystem: fb0:  frame buffer device
    [    3.782174] imx-drm display-subsystem: registered panic notifier
    [    3.812655] [drm] Initialized imx-drm 1.0.0 20120507 on minor 0
    [    3.821595] es8328 2-0011: Looking up DVDD-supply from device tree
    [    3.821686] es8328 2-0011: Looking up AVDD-supply from device tree
    [    3.821749] es8328 2-0011: Looking up PVDD-supply from device tree
    [    3.821824] es8328 2-0011: Looking up HPVDD-supply from device tree
    [    3.823212] imx-es8328 sound: Looking up audio-amp-supply from device tree
    [    3.830764] imx-es8328 sound: es8328-hifi-analog <-> 2028000.ssi mapping ok
    [    3.843043] usb 1-1.1: new full-speed USB device number 3 using ci_hdrc
    [    3.925571] dummy 2-005e: error -5 writing to lvds addr 0x5
    [    3.955794] usb 1-1.1: New USB device found, idVendor=04fe, idProduct=0008
    [    3.956227] input: imx-audio-es8328 Headphone Jack as /devices/soc0/sound/sound/card1/input2
    [    3.956817] TCP: cubic registered
    [    3.956849] NET: Registered protocol family 17
    [    3.957027] Bluetooth: RFCOMM socket layer initialized
    [    3.957045] Bluetooth: RFCOMM ver 1.11
    [    3.957067] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
    [    3.957078] Bluetooth: BNEP socket layer initialized
    [    3.957089] Bluetooth: HIDP (Human Interface Emulation) ver 1.2
    [    3.957098] Bluetooth: HIDP socket layer initialized
    [    3.963640] cpu cpu0: Looking up arm-supply from device tree
    [    3.963706] cpu cpu0: Looking up pu-supply from device tree
    [    3.963756] cpu cpu0: Looking up soc-supply from device tree
    [    3.974818] ThumbEE CPU extension supported.
    [    3.974838] Registering SWP/SWPB emulation handler
    [    3.975282] registered taskstats version 1
    [    3.976252] input: gpio-keys as /devices/soc0/gpio-keys/input/input3
    [    3.979286] rtc-pcf8523 0-0068: setting system clock to 2015-03-21 22:30:01 UTC (1426977001)
    [    3.985546] PM: Checking hibernation image partition /dev/sda2
    [    3.985612] PM: Hibernation image not present or could not be loaded.
    [    3.985634] VGEN2: disabling
    [    3.986103] SW4: disabling
    [    3.986112] sata-power: disabling
    [    3.986120] usb_otg_vbus: disabling
    [    3.986287] ALSA device list:
    [    3.986292]   #0: DW-HDMI rev 0x0a, irq 147
    [    3.986294]   #1: imx-audio-es8328
    [    4.018624] it6251 2-005c: RPCLKCnt: 1025
    [    4.019297] it6251 2-005c: System status: 0x3e
    [    4.020631] it6251 2-005c: Clock: 0x193
    [    4.021300] it6251 2-005c: Ref Link State: 0x00
    [    4.095226] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=0
    [    4.095233] usb 1-1.1: Product: Generic USB Hub
    [    4.095237] usb 1-1.1: Manufacturer: Chicony
    [    4.105449] hub 1-1.1:1.0: USB hub found
    [    4.112388] hub 1-1.1:1.0: 3 ports detected
    [    4.144785] EXT4-fs (mmcblk0p3): couldn't mount as ext3 due to feature incompatibilities
    [    4.155998] EXT4-fs (mmcblk0p3): couldn't mount as ext2 due to feature incompatibilities
    [    4.181874] EXT4-fs (mmcblk0p3): mounted filesystem with ordered data mode. Opts: (null)
    [    4.193840] VFS: Mounted root (ext4 filesystem) on device 179:3.
    [    4.204267] devtmpfs: mounted
    [    4.211338] Freeing unused kernel memory: 524K (c0a06000 - c0a89000)
    [    4.213064] usb 1-1.2: new high-speed USB device number 4 using ci_hdrc
    [    4.324547] usb 1-1.2: New USB device found, idVendor=0b95, idProduct=772b
    [    4.335418] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
    [    4.346763] usb 1-1.2: Product: AX88772B
    [    4.354185] usb 1-1.2: Manufacturer: ASIX Elec. Corp.
    [    4.363002] usb 1-1.2: SerialNumber: 000001
    [    4.515768] random: systemd urandom read with 84 bits of entropy available
    [    4.528872] systemd[1]: systemd 215 running in system mode. (+PAM +AUDIT +SELINUX +IMA +SYSVINIT +LIBCRYPTSETUP +GCRYPT +ACL +XZ -SECCOMP -APPARMOR)
    [    4.546300] systemd[1]: Detected architecture 'arm'.
    [    4.670453] NET: Registered protocol family 10
    [    4.679937] systemd[1]: Inserted module 'ipv6'
    [    4.697407] systemd[1]: Set hostname to <novena-salsa-vision>.
    [    4.709091] asix 1-1.2:1.0 eth1: register 'asix' at usb-ci_hdrc.1-1.2, ASIX AX88772B USB 2.0 Ethernet, 00:0e:c6:87:72:01
    [    4.803107] usb 1-1.3: new full-speed USB device number 5 using ci_hdrc
    [    4.925163] usb 1-1.3: string descriptor 0 read error: -22
    [    4.934594] usb 1-1.3: New USB device found, idVendor=13d3, idProduct=3393
    [    4.945432] usb 1-1.3: New USB device strings: Mfr=1, Product=2, SerialNumber=3
    [    4.958869] usb 1-1.3: Direct firmware load for ar3k/AthrBT_0x11020000.dfu failed with error -2
    [    4.971950] Bluetooth: Patch file not found ar3k/AthrBT_0x11020000.dfu
    [    4.982486] Bluetooth: Loading patch file failed
    [    4.991186] ath3k: probe of 1-1.3:1.0 failed with error -2
    [    5.083045] usb 1-1.4: new high-speed USB device number 6 using ci_hdrc
    [    5.204733] usb 1-1.4: New USB device found, idVendor=05e3, idProduct=0614
    [    5.218999] usb 1-1.4: New USB device strings: Mfr=0, Product=1, SerialNumber=0
    [    5.233524] usb 1-1.4: Product: USB2.0 Hub Charger
    [    5.247365] hub 1-1.4:1.0: USB hub found
    [    5.258553] hub 1-1.4:1.0: 4 ports detected
    [    5.342927] usb 1-1.1.1: new full-speed USB device number 7 using ci_hdrc
    [    5.433732] systemd[1]: Starting Forward Password Requests to Wall Directory Watch.
    [    5.445453] systemd[1]: Started Forward Password Requests to Wall Directory Watch.
    [    5.456877] systemd[1]: Expecting device dev-ttymxc1.device...
    [    5.466680] usb 1-1.1.1: New USB device found, idVendor=04fe, idProduct=0006
    [    5.466689] usb 1-1.1.1: New USB device strings: Mfr=3, Product=4, SerialNumber=0
    [    5.466695] usb 1-1.1.1: Product: PFU-65 USB Keyboard
    [    5.466701] usb 1-1.1.1: Manufacturer: Chicony
    [    5.493760] input: Chicony PFU-65 USB Keyboard as /devices/soc0/soc/2100000.aips-bus/2184200.usb/ci_hdrc.1/usb1/1-1/1-1.1/1-1.1.1/1-1.1.1:1.0/0003:04FE:0006.0001/input/input4
    [    5.494191] hid-generic 0003:04FE:0006.0001: input,hidraw0: USB HID v1.00 Keyboard [Chicony PFU-65 USB Keyboard] on usb-ci_hdrc.1-1.1.1/input0
    [    5.543584] systemd[1]: Starting Remote File Systems (Pre).
    [    5.555983] systemd[1]: Reached target Remote File Systems (Pre).
    [    5.565444] systemd[1]: Starting Encrypted Volumes.
    [    5.573040] usb 1-1.4.1: new low-speed USB device number 8 using ci_hdrc
    [    5.587273] systemd[1]: Reached target Encrypted Volumes.
    [    5.596101] systemd[1]: Starting Arbitrary Executable File Formats File System Automount Point.
    [    5.612494] systemd[1]: Set up automount Arbitrary Executable File Formats File System Automount Point.
    [    5.630404] systemd[1]: Starting Dispatch Password Requests to Console Directory Watch.
    [    5.641625] systemd[1]: Started Dispatch Password Requests to Console Directory Watch.
    [    5.652468] systemd[1]: Starting Paths.
    [    5.662530] systemd[1]: Reached target Paths.
    [    5.669829] systemd[1]: Expecting device dev-disk-by\x2dpath-platform\x2d2198000.usdhc\x2dpart2.device...
    [    5.685822] systemd[1]: Expecting device dev-disk-by\x2dpath-platform\x2d2198000.usdhc\x2dpart1.device...
    [    5.701949] systemd[1]: Starting Root Slice.
    [    5.706531] usb 1-1.4.1: New USB device found, idVendor=0461, idProduct=4d22
    [    5.706537] usb 1-1.4.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
    [    5.706541] usb 1-1.4.1: Product: USB Optical Mouse
    [    5.709903] input: USB Optical Mouse as /devices/soc0/soc/2100000.aips-bus/2184200.usb/ci_hdrc.1/usb1/1-1/1-1.4/1-1.4.1/1-1.4.1:1.0/0003:0461:4D22.0002/input/input5
    [    5.710338] hid-generic 0003:0461:4D22.0002: input,hidraw1: USB HID v1.11 Mouse [USB Optical Mouse] on usb-ci_hdrc.1-1.4.1/input0
    [    5.804185] systemd[1]: Created slice Root Slice.
    [    5.812100] systemd[1]: Starting User and Session Slice.
    [    5.825134] systemd[1]: Created slice User and Session Slice.
    [    5.834012] systemd[1]: Starting /dev/initctl Compatibility Named Pipe.
    [    5.847428] systemd[1]: Listening on /dev/initctl Compatibility Named Pipe.
    [    5.857585] systemd[1]: Starting Delayed Shutdown Socket.
    [    5.869821] systemd[1]: Listening on Delayed Shutdown Socket.
    [    5.878729] systemd[1]: Starting Journal Socket (/dev/log).
    [    5.891028] systemd[1]: Listening on Journal Socket (/dev/log).
    [    5.900107] systemd[1]: Starting Syslog Socket.
    [    5.911294] systemd[1]: Listening on Syslog Socket.
    [    5.919280] systemd[1]: Starting udev Control Socket.
    [    5.930971] systemd[1]: Listening on udev Control Socket.
    [    5.939453] systemd[1]: Starting udev Kernel Socket.
    [    5.950995] systemd[1]: Listening on udev Kernel Socket.
    [    5.959425] systemd[1]: Starting Journal Socket.
    [    5.970618] systemd[1]: Listening on Journal Socket.
    [    5.978739] systemd[1]: Starting System Slice.
    [    5.990166] systemd[1]: Created slice System Slice.
    [    5.998140] systemd[1]: Started File System Check on Root Device.
    [    6.007261] systemd[1]: Starting system-systemd\x2dfsck.slice.
    [    6.020045] systemd[1]: Created slice system-systemd\x2dfsck.slice.
    [    6.029365] systemd[1]: Starting system-serial\x2dgetty.slice.
    [    6.042174] systemd[1]: Created slice system-serial\x2dgetty.slice.
    [    6.051370] systemd[1]: Starting system-getty.slice.
    [    6.062951] systemd[1]: Created slice system-getty.slice.
    [    6.071197] systemd[1]: Starting Nameserver information manager...
    [    6.098358] systemd[1]: Started Set Up Additional Binary Formats.
    [    6.135602] systemd[1]: Starting Load Kernel Modules...
    [    6.149593] systemd[1]: Starting Create list of required static device nodes for the current kernel...
    [    6.168381] systemd[1]: Mounting Debug File System...
    [    6.182777] systemd[1]: Mounted Huge Pages File System.
    [    6.191698] systemd[1]: Starting udev Coldplug all Devices...
    [    6.206370] systemd[1]: Mounted POSIX Message Queue File System.
    [    6.217140] systemd[1]: Starting LSB: Set keymap...
    [    6.231822] systemd[1]: Starting Journal Service...
    [    6.253382] systemd[1]: Started Journal Service.
    [    6.269504] random: nonblocking pool is initialized
    [    6.538362] systemd-udevd[174]: starting version 215
    [    6.997200] EXT4-fs (mmcblk0p3): re-mounted. Opts: barrier=1,errors=remount-ro
    [    7.368336] Adding 32764k swap on /dev/mmcblk0p2.  Priority:-1 extents:1 across:32764k SSFS
    [    7.974582] systemd-journald[144]: Received request to flush runtime journal from PID 1
    [   13.413119] vgaarb: this pci device is not a vga device
    [   13.523499] vgaarb: this pci device is not a vga device
    [   13.923219] fec 2188000.ethernet eth0: Freescale FEC PHY driver [Micrel KSZ9021 Gigabit PHY] (mii_bus:phy_addr=2188000.ethernet:07, irq=-1)
    [   13.936001] IPv6: ADDRCONF(NETDEV_UP): eth0: link is not ready
    [   14.007551] IPv6: ADDRCONF(NETDEV_UP): wlan0: link is not ready
    [   15.106672] IPv6: ADDRCONF(NETDEV_UP): eth1: link is not ready
    [   16.307764] cfg80211: Calling CRDA to update world regulatory domain
    [   16.446817] cfg80211: World regulatory domain updated:
    [   16.451993] cfg80211:  DFS Master region: unset
    [   16.456490] cfg80211:   (start_freq - end_freq @ bandwidth), (max_antenna_gain, max_eirp), (dfs_cac_time)
    [   16.466360] cfg80211:   (2402000 KHz - 2472000 KHz @ 40000 KHz), (N/A, 2000 mBm), (N/A)
    [   16.474532] cfg80211:   (2457000 KHz - 2482000 KHz @ 40000 KHz), (N/A, 2000 mBm), (N/A)
    [   16.482731] cfg80211:   (2474000 KHz - 2494000 KHz @ 20000 KHz), (N/A, 2000 mBm), (N/A)
    [   16.490800] cfg80211:   (5170000 KHz - 5250000 KHz @ 80000 KHz, 160000 KHz AUTO), (N/A, 2000 mBm), (N/A)
    [   16.500445] cfg80211:   (5250000 KHz - 5330000 KHz @ 80000 KHz, 160000 KHz AUTO), (N/A, 2000 mBm), (0 s)
    [   16.510099] cfg80211:   (5490000 KHz - 5730000 KHz @ 160000 KHz), (N/A, 2000 mBm), (0 s)
    [   16.518318] cfg80211:   (5735000 KHz - 5835000 KHz @ 80000 KHz), (N/A, 2000 mBm), (N/A)
    [   16.526449] cfg80211:   (57240000 KHz - 63720000 KHz @ 2160000 KHz), (N/A, 0 mBm), (N/A)
    [   18.971419] wlan0: authenticate with c4:6e:1f:4f:ca:64
    [   18.988881] wlan0: direct probe to c4:6e:1f:4f:ca:64 (try 1/3)
    [   19.202116] wlan0: send auth to c4:6e:1f:4f:ca:64 (try 2/3)
    [   19.209230] wlan0: authenticated
    [   19.222126] wlan0: associate with c4:6e:1f:4f:ca:64 (try 1/3)
    [   19.229534] wlan0: RX AssocResp from c4:6e:1f:4f:ca:64 (capab=0x11 status=0 aid=4)
    [   19.237386] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
    [   19.243820] wlan0: associated
    [  297.489311] vgaarb: this pci device is not a vga device

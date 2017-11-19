---
title: "Linux Kernel Supported Versions"
table_of_contents: False
---

# Linux Kernel Supported Versions

The Ubuntu Core officially supports Linux kernel version 4.4 therefore any new
IoT device that is Ubuntu Core based should consider using it if possible.
Moreover this is a long term supported kernel by the Linux kernel community.

Also, you could use an older version of the Linux kernel. Keep in mind however
that some features might not be available. For example you need at least Linux
kernel v3.13 to have the Bluetooth Low Energy functioning. 

Using an older kernel yet having good interoperability will most probably
require you to backport the Bluetooth part of the kernel from the newer release.
This can be easily done using
[Kernel Backports
Project](https://backports.wiki.kernel.org/index.php/Main_Page)

In short:

| Kernel version | Support Status                                            |
|:--------------:|-----------------------------------------------------------|
| >= 4.4         | Will work out of the box                                  |
| >= 3.13        | Ok for Bluetooth Classic and LE however consider backporting |
| >= 3.10        | Ok for Bluetooth Classic however consider backporting |

The heart of Ubuntu Core is *snapd* which has some constraints on the kernel
version used. In particular it requires the newest AppArmor patches. Therefore,
when choosing a kernel please take a look at [sample
kernels](https://github.com/snapcore/sample-kernels) that have all the bits
necessary for *snapd* to run included. Also make sure to read the [Board
enablement
overview](https://docs.ubuntu.com/core/en/guides/build-device/board-enablement).

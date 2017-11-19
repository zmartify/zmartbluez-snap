---
title: "Introduction"
table_of_contents: False
---

# Introduction

This section gives a short overview of what is possible with the bluez snap
at the moment. It is not, however, Ubuntu Core specific and the steps described
here will work on any other Linux system with BlueZ installed on it regardless
if it is snap or classic (that is .deb, .rpm, .ebuild, or etc... based)

To easily interact with the BlueZ service the snap provides a small
utility called bluetoothctl which can be started from the command
line. The use in different scenarios will be explained in the
following sections.

**NOTE:** The bluetoothctl utility used on the examples below just uses
the DBus APIs provided by the BlueZ service.

There are also various small python script examples to play with the
DBus API at

[Test scripts](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/test)

In particular this section will discuss:

* [Prerequisites](using-prerequisites.html)
* [Available commands](available-commands.md)
* [How to pair with remote devices](pairing/introduction.md)
* [How to send files using OPP](sending-files.md)
* [Accessing the GATT services](gatt-services.md)
* [Device Enablement with Bluetooth](enablement/introduction.md)

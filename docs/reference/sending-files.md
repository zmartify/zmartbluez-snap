---
title: "Sending Files Using OPP"
table_of_contents: True
---

# Using Bluetooth to Send Files on Ubuntu Core

This section describes the required steps to be able to send files over
Bluetooth using an Ubuntu Core device. It will focus on the [OBEX Object
Push](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=309007&amp;vId=346844)
profile which is a standard Bluetooth profile for such a use case.

## Prerequisites

Make sure that:

* The bluez snap is installed.
* Service is up and running.
* Both devices are paired.

Refer to the previous sections in order to learn how to do it.

The files will be sent to the server which is a Bluetooth-enabled device with
the Object Push profile enabled. If this is not fulfilled then Ubuntu Core will
fail to connect.

The minimal set of the Bluetooth profiles that must be available on the server
device is:

|   Profile        |  UUID  |
|------------------|:------:|
| GAP Service      | 0x1800 |
| GATT Server      | 0x1801 |
| OBEX Object Push | 0x1105 |

If you are unsure about which profiles are enabled, then check this using the
*sdptool* utility:

```
% sdptool browse 00:1A:7D:DA:71:0F
Browsing 00:1A:7D:DA:71:0F ...
Service Name: GAP Service
Service RecHandle: 0x10001
Service Class ID List:
  "Generic Access" (0x1800)
Protocol Descriptor List:
  "L2CAP" (0x0100)
    PSM: 31
  "ATT" (0x0007)
    uint16: 0x0001
    uint16: 0x0007
Language Base Attr List:
  code_ISO639: 0x656e
  encoding:    0x6a
  base_offset: 0x100

Service Name: GATT Server
Service RecHandle: 0x10002
Service Class ID List:
  "Generic Attribute" (0x1801)
Protocol Descriptor List:
  "L2CAP" (0x0100)
    PSM: 31
  "ATT" (0x0007)
    uint16: 0x000c
    uint16: 0x000f
Language Base Attr List:
  code_ISO639: 0x656e
  encoding:    0x6a
  base_offset: 0x100

Failed to connect to SDP server on 00:1A:7D:DA:71:0F: Connection refused
Service Name: OBEX Object Push
Service RecHandle: 0x10004
Service Class ID List:
  "OBEX Object Push" (0x1105)
Protocol Descriptor List:
  "L2CAP" (0x0100)
  "RFCOMM" (0x0003)
    Channel: 1
  "OBEX" (0x0008)
Language Base Attr List:
  code_ISO639: 0x656e
  encoding:    0x6a
  base_offset: 0x100
Profile Descriptor List:
  "OBEX Object Push" (0x1105)
    Version: 0x0102
```

## Connect OPP Profile

Make sure that the pairing is successfully completed. You can learn how to do it
on the [Pairing page](pairing/introduction.html)

Once the pairing is successfully completed, it is time to connect the OBEX
Object Push profile. To interact with OBEX, the obexctl tool is used. Open
another terminal and type

```
$ sudo bluez.obexctl
```

You will see output like this:

```
$ sudo obexctl
[NEW] Client /org/bluez/obex 
[obex]#
```

This indicates that the OBEX client has been properly initialized and is
awaiting interactive commands. The first thing to do is to get it connected to
the remote server which is the device that has been paired in the previous
step. Type:

```
[obex]# connect 00:25:56:D1:36:6B
```

You will see output like:

```
Attempting to connect to 00:25:56:D1:36:6B
[NEW] Session /org/bluez/obex/client/session4 [default]
[NEW] ObjectPush /org/bluez/obex/client/session4 
Connection successful
[00:25:56:D1:36:6B]#
```

The above indicates that the connection has been established. Check the address
of the remote device in the prompt. It is now possible to send files.

## Sending Files

In order to send files use the *send* command while connected to the OBEX Object
Push profile. For sending a file type:

```
[00:25:56:D1:36:6B]# send <path to file>
```

Note that the file you are about to send should be accessible to the snap,
therefore it must be placed in a readable location. For example:
/var/snap/bluez/current.

Also keep in mind that the regular use of the OPP shall be accomplished through
the [D-Bus OBEX
API](https://git.kernel.org/pub/scm/bluetooth/bluez.git/tree/doc/obex-api.txt)
therefore the bluez snap itself does not need access to other snaps data. 

Below is example output of sending a file:

```
[00:25:56:D1:36:6B]# send /var/snap/bluez/current/f.txt
Attempting to send /var/snap/bluez/current/f.txt to /org/bluez/obex/client/session5
[NEW] Transfer /org/bluez/obex/client/session5/transfer10 
Transfer /org/bluez/obex/client/session5/transfer10
        Status: queued
        Name: f.txt
        Size: 4
        Filename: /var/snap/bluez/current/f.txt
        Session: /org/bluez/obex/client/session5
[CHG] Transfer /org/bluez/obex/client/session5/transfer10 Status: complete
[DEL] Transfer /org/bluez/obex/client/session5/transfer10
```

## Receiving Files

By default there is no way to receive a file using Bluetooth on Ubuntu Core
unless the application snap implements the receiving side. This is because the
incoming transfer has to be allowed and the obexctl tool does not provide
such an agent. It is assumed that the application will implement this. For
reference, here is the [OBEX D-Bus Agent
API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/obex-agent-api.txt)
description.

For convenience, there is a bluez-tests snap that packages the
[simple-obex-agent](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/test/simple-obex-agent)
Python script that implements the mentioned API. It can be used to allow
incoming file transfers through OBEX. The script itself has small
modifications to make it compatible with Ubuntu Core specifics (Ubuntu Core uses
the system, not session bus).

This feature has not been yet released, however, it is available in the edge
channel for testing.

Install the bluez-tests snap

```
$ sudo snap install --edge bluez-tests
```

When the above operation successfully finishes, you are able to use the
simple-obex-agent and experiment with receiving file transfers. Open another
shell on the device and start the simple-obex-agent by typing:

```
$ sudo bluez-tests.simple-obex-agent
```

From now on it will listen for incoming OBEX transfers and when such transfers
happen, it will prompt for a decision: accept or deny.

Please note that the software in the edge channel is for testing purposes only,
therefore, do not hesitate to report any bugs or inconveniences found.

---
title: "FAQ"
table_of_contents: False
---

# FAQ

This section covers some of the most commonly encountered problems and attempts
to provide solutions for them.

## I'm Seeing org.bluez.Error.NotReady

The *NotReady* error code indicates that the stack is not ready to fulfill the
request. One of the reasons might be that the Bluetooth hardware is unpowered.

Whenever you see something like:

```
$ sudo bluez.bluetoothctl 
[NEW] Controller 00:1A:7D:DA:71:08 core16 [default]
[bluetooth]# scan on
Failed to start discovery: org.bluez.Error.NotReady
[bluetooth]#
``` 

Power the chip on explicitly, type:

```
[bluetooth]# power on
[CHG] Controller 00:1A:7D:DA:71:08 Class: 0x500000
Changing power on succeeded
[CHG] Controller 00:1A:7D:DA:71:08 Powered: yes
[bluetooth]#
```

## Pairing Fails With a Device That Requires Confirmation

The common mistake when using *bluetoothctl* to access BlueZ is to forget about
registering an agent. The agent entity is responsible for handling the
authentication requests that are a part of the pairing procedure.

If the agent is not registered then the pairing fails.

Make sure that the agent is registered by typing:

```
[bluetooth]# agent on
Agent registered
[bluetooth]# 
```

It is safe to do it multiple times

```
[bluetooth]# agent on
Agent registered
[bluetooth]# agent on
Agent is already registered
[bluetooth]#
```

## I cannot connect to an already paired device after reboot or long idle time

The Bluetooth devices that required user-confirmation during the pairing
procedure will require the pairing agent to reconnect after they have been
disconnected.

Note that the reason for disconnection might be power-cycling the Ubuntu Core
device or idle-timeout on the remote device side when left idle for a longer
period of time. It will, therefore, happen aside from explicit disconnection.

When this happens use *bluetoothctl* to reconnect to the given device as you
would do it for the first time. Note that you do not have to pair the devices
again (unless you know that one of them has lost the pairing information) but
you will need to connect them.

In order to do this, type:

```
$ sudo bluez.bluetoothctl 
[bluetooth]# agent on
Agent registered
[bluetooth]# connect 90:7F:61:11:44:C8
```

And you shall see the devices connecting again

```
Attempting to connect to 90:7F:61:11:44:C8
[CHG] Device 90:7F:61:11:44:C8 Connected: yes
Connection successful
[ThinkPad Compact Bluetooth Keyboard with TrackPoint]#
```

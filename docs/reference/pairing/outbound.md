---
title: "Outbound Pairing"
table_of_contents: True
---

# Pairing from Ubuntu Core

Having the *bluez* snap installed start the *bluetoothctl* tool which is a
command-line interface to BlueZ.


```
$ sudo bluetoothctl
```

You should see the output similar to the following:


```
$ sudo bluez.bluetoothctl
[NEW] Controller 00:1A:7D:DA:71:08 core16 [default]
[NEW] Device 00:25:56:D1:36:6B ubuntu-0
[bluetooth]#
```

The "[NEW] Controller" line displays the information about your Bluetooth chip.
The "[NEW] Device" line displays the information about already known devices such
as previously paired ones. Note that there might be multiple or no lines
starting with [NEW] Device, as it depends on what happened prior. The
last line is the *bluetoothctl* prompt.

Since the pairing procedure will involve authentication by PIN, it is required
to register with an authentication agent. The agent handles the PIN prompt. In
order to do it type:


```
[bluetooth]# agent on
```

You should see the output like below that indicates that the agent has been
successfully registered.


```
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]#
```

Note that having the agent registered while performing pairing with a device
that does not require user confirmation to the pairing attempt will have no 
negative impact and is safe to do so. 

At this point, you can proceed with scanning for remote Bluetooth devices. To
do this type:

```
[bluetooth]# scan on
```

First you will see the confirmation that the discovery has been started

```
Discovery started
[CHG] Controller 00:1A:7D:DA:71:08 Discovering: yes
```

Which is then followed with found device events that look like:

```
[NEW] Device 08:3E:8E:E6:79:47 annapurna
[NEW] Device 00:25:56:D1:36:6B ubuntu-0
....
[NEW] Device <bluetooth address> <name>
```

The device discovery process will be stopped automatically the moment a pairing
attempt is started.

At this stage, the remote device has been discovered and is known, therefore it
is now possible to pair with it. The target device is identified by its address,
so make sure that you specify the correct one.

Note that after a certain amount of time the device discovery results are
invalidated. When this happens you see output like the following:

```
[DEL] Device 00:25:56:D1:36:6B ubuntu-0
```

If you still want to pair with this device then simply redo the
device discovery step. Do *scan on* once again.

Now do the device pairing:

```
[bluetooth]# pair 00:25:56:D1:36:6B
```

Both of the devices will try to establish a link and as it has been already
described it might require authentication. This guide walks you through pairing
with a keyboard, therefore, there will be PIN prompt unless you have skipped the
agent registration. In that case the pairing will fail.

You should see output like the following:

```
Attempting to pair with 00:25:56:D1:36:6B
[CHG] Device 00:25:56:D1:36:6B Connected: yes
Request confirmation
[agent] Confirm passkey 687331 (yes/no):
```

Type *yes* or *no* depending on if you want the link to be established. Type
*yes* here

```
[agent] Confirm passkey 687331 (yes/no): yes
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001104-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001105-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001106-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 0000110a-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 0000110b-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 0000110c-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 0000110e-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001112-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 0000112f-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001132-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001133-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001200-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001800-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00001801-0000-1000-8000-00805f9b34fb
[CHG] Device 00:25:56:D1:36:6B UUIDs: 00005005-0000-1000-8000-0002ee000001
[CHG] Device 00:25:56:D1:36:6B Paired: yes
Pairing successful
[CHG] Device 00:25:56:D1:36:6B Connected: no
```

At this stage the devices are in a paired state and can be connected.


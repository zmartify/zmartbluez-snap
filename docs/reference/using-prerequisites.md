---
title: "Prerequisites"
table_of_contents: True
---

# Prerequisites

This section describes the requirements that must be satisfied in order to use
Bluetooth on an Ubuntu Core device.

In short you have to make sure that:

 * The BlueZ snap is installed
 * The Bluetooth daemons are running
 * The plugs and slots are connected

## The Bluez Snap is Installed

Make sure that the latest *bluez* snap is installed. You can check this by using
*snap list* command:

```
$ snap list
Name                            Version        Rev   Developer  Notes
bluez                           5.37-2         27    canonical  -
$
```

If *bluez* is not listed by the above command you can install it with:

```
$ sudo snap install bluez
```

## The Bluetooth Daemons are Running

Normally, once the snap is installed, the Bluetooth daemon is up and running.
Nevertheless it is still good to verify this.

For *bluetoothd* type:

```
$ systemctl status snap.bluez.bluez.service
```

The expected output should look like:

```
● snap.bluez.bluez.service - Service for snap application bluez.bluez
   Loaded: loaded (/etc/systemd/system/snap.bluez.bluez.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2016-11-02 15:15:31 UTC; 4 months 11 days ago
 Main PID: 1580 (bluetoothd)
   CGroup: /system.slice/snap.bluez.bluez.service
           └─1580 /snap/bluez/x2/usr/lib/bluetooth/bluetoothd -E
```

For *obexd* type:

```
$ systemctl status snap.bluez.obex.service
```

The expected output should look like:

```
● snap.bluez.obex.service - Service for snap application bluez.obex
   Loaded: loaded (/etc/systemd/system/snap.bluez.obex.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2016-11-02 15:15:31 UTC; 4 months 11 days ago
 Main PID: 1584 (obexd)
   CGroup: /system.slice/snap.bluez.obex.service
           └─1584 /snap/bluez/x2/usr/lib/bluetooth/obexd
```

Note that you need *bluetoothd* for the regular Bluetooth usage, however it is
not enough for exchanging files over Bluetooth. For this to work you need the
*obexd* daemon. It is mentioned here because, for example, on Ubuntu Desktop the
*obexd* is not started by default.

## The Plugs and Slots are Connected

Checking for the Bluetooth plug and slot being auto-connected is one of the snap
verification criteria therefore in 99.9% cases it will be as expected. For the
sake of exercise it is good to verify


```
$ snap interfaces bluez
bluez:service             bluez:client
-                         bluez:bluetooth-control
$
```

You should expect the output like the above, that is the *bluez:service* slot is
connected with the *bluez:client* plug.


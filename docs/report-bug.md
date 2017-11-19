---
title: "Report a Bug"
table_of_contents: False
---

# Report a Bug

Bugs can be reported [here](https://bugs.launchpad.net/snappy-hwe-snaps/+filebug).

## Information Required to Include in a Bug Report

When submitting a bug report, please attach system log coming from the journal:

 * $ journalctl --no-pager > system-log

Moreover please include the following information:

 * Bluetooth adapter information
 * List of paired devices
 * State of the Bluetooth kill-switch
 * The HCI trace

### Bluetooth Adapter Information

```
$ sudo hciconfig -a
```

### List of Paired Devices

```
$ bluetoothctl
[bluetooth]# show
[bluetooth]# devices
[bluetooth]# info <mac addr of any device you have problems with>
```

### State of the Bluetooth kill-switch

```
$ snap install wireless-tools
$ sudo wireless-tools.rfkill list
```

Note that the *rfkill* command is a part of *wireless-tools* snap.

### The HCI Trace

The HCI trace is a snapshot of the communication between the Bluetooth host
(software stack) and the Bluetooth controller (the chip). The *btmon* tool can
be used to capture such for both live debugging and saving it for later. Note
that the HCI trace needs to be captured at the same time the Bluetooth issue
occurs.

When *btmon* is executed without any parameters, it will offer live debugging
which will print in a ‘tail -f’ fashion an ongoing exchange of the commands and
events between the stack and the chip. It is possible however to make it save
the data in the [snoop format](https://tools.ietf.org/html/rfc1761) which can
later be viewed using for example [Wireshark](https://www.wireshark.org).

Now, for live debugging:

```
$ sudo btmon
```

For saving it later in a .snoop format:

```
$ sudo btmon --write ~/hcitrace.snoop
```

In case you are saving the .snoop file under the home directory make sure that
the bluez snap has the home interface connected.

```
$ sudo snap list interfaces
```

If not, then connect it

```
$ sudo snap connect bluez:home :home
```

Alternatively you should be able to save the file into a snap-writable folder
such as either ~/snap/bluez/common or /var/snap/bluez/current.

The nice thing about btmon and how it works is that it is possible to have
several versions of it executed simultaneously. This allows capturing logs as
in the last example in one shell and viewing it live in another.

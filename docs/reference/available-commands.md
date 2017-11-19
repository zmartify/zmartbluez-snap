---
title: "Available commands"
table_of_contents: True
---

# Available Commands

This section will describe which commands are provided by the *bluez* snap.

## Commands

The purpose of the *bluez* snap is to provide the BlueZ Bluetooth stack. Apart
from this it contains various tools shipped with BlueZ itself. The following
table lists the commands that are provided by the *bluez* snap:

| Command      | Short description                                             |
|--------------|---------------------------------------------------------------|
| bluez        | The *bluetoothd* Bluetooth daemon                             |
| obex         | The *obexd* OBEX daemon                                       |
| bluetoothctl | A command-line interface to the BlueZ 			       |
| obexctl      | A command-line interface to the BlueZ for file transfers      |
| hciconfig    | HCI device configuration utility                              |
| hcidump      | Reads raw HCI data and prints it on screen                    |
| hciattach    | Attach a serial UART to the BT stack as a transport interface |
| hcitool      | Tool used to configure Bluetooth connections                  |
| sdptool      | A tool to perform SDP queries on Bluetooth devices            |

There is a quick way of checking what a snap provides. To do this you can use
the snap scheme for exposing commands which is *snap_name.command*. To see
all the commands provided by the *bluez* snap type:

```
$ bluez.<TAB><TAB>
```

The double **TAB** indicates that you should hit the tab key twice for bash
auto-completion to kick in. Immediately you will see a list of
available commands:

```
$ bluez.
bluez.bluetoothctl  bluez.hciattach     bluez.hciconfig     bluez.hcidump
bluez.hcitool       bluez.obexctl       bluez.sdptool       
$ bluez.
```

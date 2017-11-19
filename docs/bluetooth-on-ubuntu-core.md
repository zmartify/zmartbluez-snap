---
title: "Bluetooth on Ubuntu Core"
table_of_contents: True
---

# Ubuntu Core Bluetooth Interfaces

Bluetooth on Ubuntu Core is provided by the BlueZ stack which is an official
Linux Bluetooth protocol stack. The lower-level part of it comes with the kernel
snap while the user-space portion can be installed as a separate snap.

## The Bluetooth interfaces on Ubuntu Core

On Ubuntu Core there are two interfaces which define the communication of the
Bluetooth stack:

 * bluetooth-control
 * bluez

You can learn more on the [interfaces
documentation](https://docs.ubuntu.com/core/en/reference/interfaces/index)

Note that unlike the *bluetooth-control* interface the *bluez* interface is not
installed by the *core* snap, neither the *gadget* nor *kernel*. It shall be
installed by the application snap.

### Putting it all together

As you know now there are two Bluetooth related interfaces on Ubuntu Core, the:
*bluetooth-control* and *bluez*. One of them is provided by the *core* snap
while the another is provided by the application snap.

On a system without *bluez* snap installed, type:

```
$ snap interfaces | grep blue
:bluetooth-control        -
```

Observe that there is a *bluetooth-control* slot provided by the core snap. This
is unlike to *bluez* because no snap exists which provides a slot based on the
*bluez* interface. You need an application snap to reveal it.

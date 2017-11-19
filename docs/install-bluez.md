---
title: "Install bluez"
table_of_contents: True
---

# Install bluez

Install the *bluez* snap via:

```
$ snap install bluez
```

The snap is being downloaded and installed. Observe that the snap has been
installed like follows:

```
$ snap install bluez
bluez 5.37-2 from 'canonical' installed
```

The naming scheme for the *bluez* snap includes the current BlueZ version being
packaged in the snap (5.37 in this case) and the revision of the snap itself
(2nd in this case). Whenever the snap is updated but still provides BlueZ
version 5.37 the last digit will be incremented.

The above output informs that BlueZ 5.37 has been installed on the system. This
effect is equivalent to typing

```
$ sudo apt install bluez
```

on a classic Ubuntu flavor that you run on your desktop or laptop computer.

Again, let's list the interfaces:

```
$ snap interfaces | grep blue
bluez:service             bluez:client
:bluetooth-control        -
$
```

This time it lists the bluez:service slot and the bluez:client plug that are
provided by the *bluez* snap itself.

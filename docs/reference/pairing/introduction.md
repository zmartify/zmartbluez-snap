---
title: "Introduction to Pairing"
table_of_contents: True
---

# Introduction to Pairing

This section teaches how to pair two Bluetooth devices using *bluetoothctl* -
the command-line interface to BlueZ.

## What is Pairing

In Bluetooth terminology pairing is the process of making two devices know about
each other. The key concept is about exchanging so called *link-keys* that are used to
secure the communication. The pairing process involves authentication however
due to the nature and variety of Bluetooth devices there will be different ways
of confirming the pairing attempt:

* Devices such as keyboards or car-kits will require authentication by PIN/passkey code
* Other devices will provide a yes/no choice to the pairing attempt
* Devices without an input interface such as headsets or speakers will not
  require the user to confirm the pairing attempt at all

Pairing with a remote device can be done in two ways due to the fact that it can
be initiated from both endpoints. Both ways are described further in this
section.

* [Inbound pairing](inbound.html)
* [Outbound pairing](outbound.html)

## Handling Authentication Requests by BlueZ

The pairing procedure includes an authentication that requires confirmation by
the user. If you have ever used Bluetooth previously you probably remeber
entering a pin code or answering a "would you like to connect yes/no" question.

To pair with other devices BlueZ uses an agent-style DBus API. See the
following links for more details on this:

 * [Agent API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/agent-api.txt)
 * [Device API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt)

Within the bluetoothctl utility we can register such an agent with a
specific IO capability with the BlueZ service and then process any
further pairing operation.

If no agent is registered with BlueZ and a pairing operation happens,
BlueZ will try to pair with the remote device without further user interaction.

The agent has to be registered explicitly by typing:

```
$ sudo bluetoothctl
[bluetooth]# agent on
Agent registered
```

The pairing section will walk you through the pairing procedure with a
keyboard. It will require passcode authentication.

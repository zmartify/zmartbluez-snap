---
title: "Inbound Pairing"
table_of_contents: True
---

# Pairing From Remote Device

In this scenario it is the remote device that is active in the pairing
procedure. It will search, discover and initiate pairing. The only thing that an
Ubuntu Core device has to make sure of is to be discoverable and pairable, as
this will allow the remote device to discover and initiate a connection with it.

```
$ bluetoothctl
[bluetooth]# discoverable on
Changing discoverable on succeeded
[bluetooth]# pairable on
Changing pairable on succeeded
```

At this stage the Ubuntu Core device is ready to be discovered.
It is important to register the pairing agent so that the authentication process
can be completed. Type:

```
$ bluetoothctl
[bluetooth]# agent on
Agent registered
[bluetooth]# default-agent 
Default agent request successful
```

At this stage the Ubuntu Core device is ready to be discovered. Take your remote
Bluetooth device and start the discovering process. After a short while you
should see the Ubuntu Core device on the list of found devices. Initiate the
pairing.

Notice that bluetoothctl will display the pairing confirmation coming from
the agent:

```
[CHG] Device 00:1A:7D:DA:71:08 Connected: yes
Request confirmation
[agent] Confirm passkey 687331 (yes/no):
```

The agent will require you to type yes or no depending on if you like to allow
the devices to connect or not. Type yes here

```
[agent] Confirm passkey 687331 (yes/no): yes
[CHG] Device 00:1A:7D:DA:71:08 Connected: no
```

At this stage the devices are paired and can be connected.


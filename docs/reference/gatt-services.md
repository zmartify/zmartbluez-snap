---
title: "Accessing GATT Services"
table_of_contents: True
---

# Accessing GATT Services

In this example we want to connect with a LE device and explore its
provided GATT services. The used LE device in this example provides
a number of vendor specific GATT services but also the standard
battery GATT service.

First, connect with the discovered LE device by using the bluetoothctl command

```
$ sudo bluetoothctl
[bluetooth]# connect 5C:31:3E:71:0C:E7
Attempting to connect to 5C:31:3E:71:0C:E7
[CHG] Device 5C:31:3E:71:0C:E7 Connected: yes
Connection successful
```

As soon as BlueZ has discovered which GATT services are available the
bluetoothctl utility will print out the following:

```
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 00001801-0000-1000-8000-00805f9b34fb
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 0000180f-0000-1000-8000-00805f9b34fb
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 0d271100-f0d4-469d-afd3-605a6ebbdb13
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 0d27fa01-f0d4-469d-afd3-605a6ebbdb13
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 0d27fa60-f0d4-469d-afd3-605a6ebbdb13
[CHG] Device 5C:31:3E:71:0C:E7 UUIDs: 0d27ffc0-f0d4-469d-afd3-605a6ebbdb13
[NEW] Service /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010 Vendor specific (Primary)
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char0011 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char0013 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char0015 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char0017 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char0019 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char001b Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010/char001d Vendor specific
[NEW] Service /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f Vendor specific (Primary)
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f/char0020 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f/char0022 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f/char0024 Vendor specific
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f/char0026 Vendor specific
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f/char0026/desc0028 Client Characteristic Configuration
[NEW] Service /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029 Battery Service (Primary)
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a Battery Level
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a/desc002c Client Characteristic Configuration
[NEW] Service /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service002d Vendor specific (Primary)
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service002d/char002e Vendor specific
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service002d/char002e/desc0030 Client Characteristic Configuration
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service002d/char002e/desc0031 Characteristic User Description
[NEW] Service /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032 Vendor specific (Primary)
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0033 Vendor specific
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0033/desc0035 Client Characteristic Configuration
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0033/desc0036 Characteristic User Description
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0037 Vendor specific
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0037/desc0039 Client Characteristic Configuration
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char0037/desc003a Characteristic User Description
[NEW] Characteristic /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char003b Vendor specific
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char003b/desc003d Client Characteristic Configuration
[NEW] Descriptor /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032/char003b/desc003e Characteristic User Description
[CHG] Device 5C:31:3E:71:0C:E7 GattServices: /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0010
[CHG] Device 5C:31:3E:71:0C:E7 GattServices: /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service001f
[CHG] Device 5C:31:3E:71:0C:E7 GattServices: /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029
[CHG] Device 5C:31:3E:71:0C:E7 GattServices: /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service002d
[CHG] Device 5C:31:3E:71:0C:E7 GattServices: /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0032
[CHG] Device 5C:31:3E:71:0C:E7 Name: X4-LIFE Xmarty 2.0
[CHG] Device 5C:31:3E:71:0C:E7 Alias: X4-LIFE Xmarty 2.0
```

It is now possible to select specific characteristics and read their values or,
if possible, also write them. This example focuses on the battery level
characteristic from the battery GATT service.

```
[5C-31-3E-71-0C-E7]# select-attribute /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a
[X4-LIFE Xmarty 2.0:/service0029/char002a]# read
Attempting to read /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a
[CHG] Attribute /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a Value: 0x49
  49
```

It is also possible to receive notifications when the value of a characteristic
changes.

```
[X4-LIFE Xmarty 2.0:/service0029/char002a]# notify on
[CHG] Attribute /org/bluez/hci0/dev_5C_31_3E_71_0C_E7/service0029/char002a Notifying: yes
Notify started
```

This will now notify whenever the value of the selected characteristic changes.

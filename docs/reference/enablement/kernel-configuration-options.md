---
title: "Linux kernel configuration options"
table_of_contents: True
---

# Linux Kernel Configuration Options

This section lists the Linux kernel configuration options related to the
Bluetooth support. It is based on the Linux kernel v4.4.

Note that the default Linux kernel for Ubuntu Core has al the necessary bits
enabled by default.

Most of the Bluetooth systems will support *Classic* mode therefore you need
to make sure that the following options are selected.

```
  [*] Networking support
      <M> Bluetooth subsystem support
    	[*]   Bluetooth Classic (BR/EDR) features
	<M>     RFCOMM protocol support
	[*]       RFCOMM TTY support
	<M>     BNEP protocol support
	[*]       Multicast filter
	[*]       Protocol filter support
	<M>     CMTP protocol support
	<M>     HIDP protocol support
	[*]     Bluetooth High Speed (HS) features
	[*]   Bluetooth Low Energy (LE) features
	<M>     Bluetooth 6LoWPAN support
	[ ]   Bluetooth self testing support
	[*]   Export Bluetooth internals in debugf
```

Note that this is a general set and it might be further tweaked to match your
device use-cases and capabilities. For example, on devices that will not offer
networking over Bluetooth, a *BNEP* can be disabled. 

Note that if your Bluetooth controller (chip) supports Bluetooth Low Energy,
then leave the BLE related options selected or disable otherwise:

```
  [*] Networking support
      <M> Bluetooth subsystem support
	[*]   Bluetooth Low Energy (LE) features
	<M>     Bluetooth 6LoWPAN support
```

It is also important to remember about the [UHID
driver](https://lwn.net/Articles/508083/). It is needed for
Bluetooth Low Energy (a.k.a. Smart) keyboards and mice.

```
Device Drivers
  HID support
    {M} HID bus support
    [*]   Battery level reporting for HID devices
    [*]   /dev/hidraw raw HID device support
    <M>   User-space I/O driver support for HID subsystem
    <M>   Generic HID driver 
```

Below are the Linux kenrel config options for reference. They are based on the 
*Linux core16 4.4.0-1040-raspi2* kernel which is the official Ubuntu Core Linux
kernel for Raspberry Pi 2/3.

```
CONFIG_NET=y
CONFIG_BT=m
CONFIG_BT_BREDR=y
CONFIG_BT_RFCOMM=m
CONFIG_BT_RFCOMM_TTY=y
CONFIG_BT_BNEP=m
CONFIG_BT_BNEP_MC_FILTER=y
CONFIG_BT_BNEP_PROTO_FILTER=y
CONFIG_BT_CMTP=m
CONFIG_BT_HIDP=m
CONFIG_BT_HS=y
CONFIG_BT_LE=y
CONFIG_BT_6LOWPAN=m
CONFIG_BT_DEBUGFS=y

CONFIG_BT_HCIBCM203X=m
CONFIG_BT_HCIBFUSB=m
CONFIG_BT_HCIBPA10X=m
CONFIG_BT_HCIBTSDIO=m
CONFIG_BT_HCIBTUSB=m
CONFIG_BT_HCIBTUSB_BCM=y
CONFIG_BT_HCIBTUSB_RTL=y
CONFIG_BT_HCIUART=m
CONFIG_BT_HCIUART_3WIRE=y
CONFIG_BT_HCIUART_ATH3K=y
CONFIG_BT_HCIUART_BCM=y
CONFIG_BT_HCIUART_BCSP=y
CONFIG_BT_HCIUART_H4=y
CONFIG_BT_HCIUART_INTEL=y
CONFIG_BT_HCIUART_LL=y
CONFIG_BT_HCIUART_QCA=y
CONFIG_BT_HCIVHCI=m

CONFIG_BT_ATH3K=m
CONFIG_BT_BCM=m
CONFIG_BT_INTEL=m
CONFIG_BT_MRVL=m
CONFIG_BT_MRVL_SDIO=m
CONFIG_BT_QCA=m
CONFIG_BT_RTL=m
CONFIG_BT_WILINK=m
```

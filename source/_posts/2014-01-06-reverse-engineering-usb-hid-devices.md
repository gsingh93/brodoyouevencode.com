---
layout: post
title: "Reverse Engineering USB HID Devices"
date: 2014-01-06 21:05
comments: true
published: true
tags: ['reverse engineering', 'usb', 'c']
---

Recently, one of my friends let me borrow his [Magtek Mini Swipe Card Reader](https://www.magtek.com/shop/mini.aspx) to play with. It was cool to see the data stored on my credit card and school ID card, but I was annoyed that the data was typed on the screen, emulating a keyboard. In other words, there was no way to get this data directly to your own program; it had to be parsed after it was output into some text editor on the host computer. I had been curious about the USB protocol for some time, and I had always wanted to write my own driver, so I set out to reverse engineer how the card reader worked and write my own driver for it. I didn't find too much information online, and what I did find was scattered in various locations, so hopefully this guide will help others reverse engineer their own USB devices.

USB Background
--------------

* Request based
* Descriptors
* Hubs
* lspci
* vendor/product id
* HID vs other devices
* Magic carpet and other weird specs

Reverse Engineering the Device
------------------------------

* Wireshark, usbmon, vusb-analyzer, and other windows software
* Hardware tools
* Detaching driver
* Understanding usbmon output
* Finding spec for our device

Writing the Driver
------------------

* lsusb

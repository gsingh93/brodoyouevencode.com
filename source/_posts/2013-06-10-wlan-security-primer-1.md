---
layout: post
title: WLAN Security Primer 1
date: 2013-06-10 08:23
comments: true
sharing: true
---
### Setting Up Your Environment
[Part 1](http://www.securitytube.net/video/1756) of the series is fairly short. Vivek covers the motivation for WLAN security, the software and hardware you'll need for the rest of the videos, and goes through a complete installation and configuration of them.

<!--more-->

In summary, you'll need to have [BackTrack](http://www.backtrack-linux.org/) setup on as a virtual machine or a partition and you'll need a network card capable of packet sniffing and packet injection. Vivek uses the Alfa Networks AWUS036H USB network card because it's cheap and already well integrated into BackTrack. The version of BackTrack used in the videos is version four, but any higher version should work just fine. If you have any issues, you can check out [the video](http://www.securitytube.net/video/1756) for a complete walk through.

[Part 2](http://www.securitytube.net/video/1757) of the series is where it starts to get a bit more interesting. This video covers channels, bands, and how to get started sniffing. Start off by plugging in your network card and starting up BackTrack. To check if the network card is connected, type `ifconfig -a` in the terminal. You should see something like `wlan0` show up. While this interface may be connected, it may not be up an running. All running network interfaces can be seen with `ifconfig`. If you don't see `wlan0` in that list, you'll need to run `ifconfig wlan0 up` to bring that interface up (`ifconfig wlan0 down` will do the opposite and bring that interface down).

Now that you're card is connected and running, we're going to need to create a virtual interface on top of it. The reason for this is because we need to sniff on a network interface that's in [monitor](http://en.wikipedia.org/wiki/Monitor_mode) mode, which means that it accepts all packets on the network (instead of just ones directed to it). It's a virtual interface because it isn't created by it's own physical card. To create this interface, we're going to use a program called airmon-ng. If you type `airmon-ng` in the terminal you'll see a list of wireless interfaces (you should see wlan0 there). If you type `airmon-ng start wlan0`, you'll create a virtual interface in monitor mode (in my case it's called `mon0`). If you type `airmon-ng` again, you'll see the new `mon0` interface in the list of wireless interfaces. You'll also see it if you type `ifconfig` again. Finally, if you type `iwconfig` you'll see both wlan0 and mon0 there, but in information about mon0, you'll see some text that says "Mode: monitored". You'll also notice that the MAC address of both interfaces (HWaddr in BT) is the same for both cards. This is because mon0 is a virtual interface on top of the physical interface wlan0.

You can go ahead and start Wireshark now by typing `wireshark &`. If you go to Capture -> Interfaces, you'll see mon0 in the list. Click "Start" and you Wireshark should start capturing packets on that interface.

### Bands and Channels
Now for a little theory. When your WiFi card is communicating with other computers and networks, it's doing so using a particular frequency. Some example frequencies are 2.4GHz, 3.6GHz, and 5GHz, and these frequencies are called [bands](http://en.wikipedia.org/wiki/Band_(radio)). In each band or frequency ranges, there are a lot of different frequencies the WiFi card can operate at. This range of frequencies is broken into subdivisions called [channels](http://en.wikipedia.org/wiki/List_of_WLAN_channels). So for example, channel 1 in the 2.4 GHz band operates between 2.401 and 2.423 GHz and channel 2 operates between 2.406 and 2.428 GHz (You can find all of the range frequencies [here](http://en.wikipedia.org/wiki/802.11b). Now why is this important? Well, when you're sniffing a WiFi network, your network card can only be on one channel at a time. In order to sniff multiple channels at the same time, your card either needs to have multiple radios to talk to listen to multiple channels (unlikely) or you need to hop between each channel (this will result in some packet loss).

### airodump-ng

BackTrack comes with a nice tool that allows us to hop between channels easily. Airodump-ng is a tool that allows us to select which bands and channels our card should operate on. If we run the command `airodump-ng mon0 --band bg`, our interface will hop between all of the channels on the b and g bands (2.4 GHz). If you open up Wireshark now, the traffic you see will be from each channel of the band. In the next articles, you'll learn what all of the information on that screen means.
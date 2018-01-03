---
type: post
title: "Wake on LAN your PC's"
---

First, you need to have WOL enabled in bios. See [What Is Wake-on-LAN, and How Do I Enable It?](https://www.howtogeek.com/70374/how-to-geek-explains-what-is-wake-on-lan-and-how-do-i-enable-it/) for instructions.

Second, you need [Wake on Lan](https://play.google.com/store/apps/details?id=co.uk.mrwebb.wakeonlan) app on Android to wake up your PC's.

As the PC you want to control is turned on, open the Android app and scan the network.

Add the desired PC (MAC address) to the bookmark list.

Suspend the PC with:
```bash
sudo systemctl suspend
```
Now, from Android phone, click to Wake on LAN your PC.

See demo video:

<iframe width="100%" height="480px" src="https://www.youtube.com/embed/-jBCUAHkNlM" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

### Warning!
WOL is not working through a OpenVPN TUN setup, need more documenting how to make this work.

Future work:
 * [#1](https://bish.co.uk/2013/04/25/raspberry-pi-as-a-wol-server/) if option above not working, make a WOL server so that you can remote wake up pc from the internet through VPN
 * [#2](https://github.com/dferg/WakeProxyd) make WOL work even if your BIOS is not capable (by using a router/raspberry GPIO port connected to PC power switch)

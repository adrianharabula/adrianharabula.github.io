---
type: post
title: "How to enable watchdog on Raspberry Pi 3"
description: "Here, a real quick setup of the watchdog on Raspberry Pi. It is a hardware counter. If OS becomes unresponsive and the counter is not reset, Pi will automatically reboot."
---

Here, a real quick setup of the watchdog on Raspberry Pi.

It is a hardware counter. If OS becomes unresponsive and the counter is not reset, Pi will automatically reboot.

First enable watchdog from `/boot/config.txt`, adding the following line:

```
dtparam=watchdog=on
```

Then install watchdog service:
```
sudo apt install watchdog
```

Uncomment the following line from `/etc/watchdog.conf`
```
max-load-1              = 24
```

Restart your Raspberry.

After restart, test watchdog with bomb fork:
```
:(){ :|: & };:
```

This command will render your Pi unusable, and watchdog will kick in and reboot your Raspberry!
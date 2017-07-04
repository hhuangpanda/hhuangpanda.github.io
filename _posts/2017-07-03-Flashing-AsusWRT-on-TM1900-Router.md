---
layout: post
title: Flashing AsusWRT or Merlin on a TM-1900 Router
---

The TM1900 router has the same hardware as the Asus RT AC68U/R/W. The only difference is the T-Mobile branding on the outside. Firmware wise, the TM-1900 has its IP address at 192.168.29.1 rather than Asus' 192.168.1.1 and its default password is *password* rather than *admin*. 

Why flash the firmware if the existing one already works? There may be many reasons. 
- Custom firmware has more features, such as VPN support.
- Custom firmware may fix bugs or security issues.
- The lights on the router bother you and you want to turn them off in the custom firmware.
- Sometimes you feel like SSH-ing into the router.
- It's your router, why not?

# Required Programs on your PC
Before beginning to flash a brand new firmware onto the router, some prerequisite software is needed. This guide is primarily for the PC, it's slightly more difficult on a MAC/Linux machine because you'd need to edit hex values in some of the binaries manually. The following programs are more or less required in order to flash the router.
- An SSH client to get into the router. The standard recommendation is PuTTY. Other terminals such as MobaXterm are also fine.
- A SCP client such as WinSCP to move files between the router and the computer.
- A text editor such as NotePad++ or Sublime Text with a HEX editor plugin to view and edit files.

# Required Files
* TODO
# Instructions
* TODO

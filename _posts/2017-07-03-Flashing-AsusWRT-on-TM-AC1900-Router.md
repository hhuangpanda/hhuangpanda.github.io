---
layout: post
title: Flashing AsusWRT or Merlin on a TM-AC1900 Router
---

The TM-AC1900 router has the same hardware as the Asus RT-AC68U/R/W. The only difference is the T-Mobile branding on the outside. Firmware wise, the TM-AC1900 has its IP address at 192.168.29.1 rather than Asus' 192.168.1.1 and its default password is *password* rather than *admin*. 

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
All required files can be download [here][1]. It includes:
- cfe.exe: This will copy over the MAC addresses and secret code from the old firmware environment / bootloader (cfe bin file) to the new one.
- FW_RT_AC68U_30043763626.trx: This version of the Asus firmware is recommended for flashing before upgrading. It ensures that the router has a 64MB jffs partition.
- mtd-write: Run this executable to flash the cfe. The file included in the link is also known as mtd-write v2.
- Rescue.exe: not necessarily required. It allows a user to flash the router with an older version of a firmware. This can also be done in the mini-cfe environment in the browser. In any case, both methods only work once the router has been put in rescue mode.
- rt-ac68u_1.0.2.0_us.bin: This is the bootloader that makes sure that DDR3 is unlocked to 800 MHz and increases rootfs/mtd3 to 64MB. This file should be renamed to new_cfe.bin and will need to be modified with the existing cfe's secret code and mac addresses.
- TM-AC1900_3.0.0.4_376_1703-g0ffdbba.trx: Downgrade to this version of the T-Mobile firmware to enable SSH. Requires the router to be set to rescue mode. This firmware downgrade is not needed if the HTML hack works to enable SSH/Telnet.

# Instructions
* TODO

[1]: https://mega.nz/#!040jGIRS!h3yxFOjlt6MoaDUfJmgqm34PPMjhn09S4j36mt4LOAo

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
## Changing the computer's IP address
The router's default address is probably 192.168.29.1. First, it's worth setting a static IP address for the computer before changing the firmware of the router. It's also best to use ethernet to connect to the router rather than Wi-Fi. Go to Control Panel -> Change adapter settings -> right click the appropriate connection -> select Internet Protocol Version 4 -> click on properties -> Use the following IP address -> change IP address to 192.168.29.9, leave the subnet mask as is, set the default gateway to 192.168.29.1. The DNS settings can be left as is, if you have to put in some IPs, use 8.8.8.8 and 8.8.4.4, which are Google's DNS.
## Part 1 - Getting an older version of the T-Mobile firmware to enable SSH/Telnet
This step can be skipped if you are able to edit the HTML in the router software under Administration->System or by going straight to http://192.168.1.1/Advanced_System_Content.asp. Right click on the page and select inspect element, search HTML for *sshd_enable*
```
<select name="sshd_enable" class="input_option" onchange="check_sshd_enable(this.value);">
<option value="0">No</option>
<option value="1">LAN + WAN</option>
<option value="2" selected="">LAN only</option>
</select>
```
or search for *telnetd*
```
<tr id="telnet_tr">
<th>Enable Telnet</th>
<td>
<input name="telnetd_enable" value="1" type="radio">Yes
<input name="telnetd_enable" value="0" checked="" type="radio">No
</td>
</tr>
```
You will find that there might be a disabled flag in the HTML, delete it and press *enter*, and you should be able to see the ssh/telnet options. Check the appropriate option and try Part 2, if it works, this part can be skipped.

The router needs to be put in recovery mode, which is somewhat more difficult with T-Mobile's firmware. 
1. Remove power to the router
2. hold both the reset and WPS buttons at the same time
3. Turn on the router, keep holding those buttons
4. Navigate to 192.168.29.1 while holding the buttons. If you don't see Mini-CFE on the page, open Resuce.exe from the files downloaded before.
5. While continuing to hold the buttons, upload TM-AC1900_3.0.0.4_376_1703-g0ffdbba.trx. Keep holding the buttons while the upload is happening. Do not release until the upload is complete, this may take a minute.
6. Reboot the router
7. Wipe NVRAM, which can be done in one of two ways: 
    1. Command line
        - SSH/Telnet into the router and in the command line type "mtd-erase2 nvram", press *enter*
        - type "reboot", press *enter*
    2. Hardware
        - Power off the router
        - Wait 10 seconds
        - Hold the WPS button
        - Power on the router while continuing to hold the WPS button. Release WPS button after 20 seconds.

## Part 2 - SSH/Telnet into the router
For a quick 101 into the command line, all commands are run by pressing the *enter* button. Make sure there are no typos, once the *enter* is pressed, the command is run and if there is a problem there may be no way back.






[1]: https://mega.nz/#!040jGIRS!h3yxFOjlt6MoaDUfJmgqm34PPMjhn09S4j36mt4LOAo

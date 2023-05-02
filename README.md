# How-to: Install Dell DW1830 Wifi/BT on Arch Linux or EndeavourOS (and similar)

This guide is a how to get a Dell DW1830 Wifi/BT card (Broadcom 43602 + Broadcom BCM20703A1) working in Arch Linux or EndeavourOS

I can't confirm on Arch Linux specifically, but EndeavourOS incorrectly detects the DW1830 and loads the wrong kernel drivers. As a side effect, the bluetooth service is disabled by default. In my particular instance, the DW1830 is installed in a Dell XPS 15 9560. This is a non-OEM setup so it's possible not everything in this guide will apply.

## Guide
The general solution is to uninstall `broadcom-wl-dkms` and/or `broadcom-wl` and then enable the bluetooth service.

For example:

`yay -R broadcom-wl-dkms`

If, through the course of troubleshooting you've installed `b43-firmware` or the `b43-firmware-classic`/`b43legacy-firmware` variants, you should be able to safely uninstall them.

I.e.: 
`yay -R b43-firmware`

Next, enable the bluetooth service:

`sudo systemctl enable bluetooth.service`

At this point, you should be able to restart and you'll have working WIFI and Bluetooth.

## Troubleshooting
If Bluetooth is not working, head over to https://github.com/winterheart/broadcom-bt-firmware and follow the instructions for installing the appropriate BT firmware. Take special note of the section titled "Notes about combined WiFi+Bluetooth devices"

If you're still running into issues, become familiar with `dmesg`, `lspci`, `lsmod`, `modprobe`, `depmod` which are referenced in the wiki links below. These commands combined with a sprinkling of `grep` should get you the information you need to solve your specific issues.

### Credits: 
- [nsvdhx on the Arch forums](https://bbs.archlinux.org/viewtopic.php?id=267367)
- [@winterheart](https://github.com/winterheart) for the broadcom bt drivers
- The Arch wiki pages for [Broadcom Wireless](https://wiki.archlinux.org/title/broadcom_wireless) and [Bluetooth](https://wiki.archlinux.org/title/bluetooth)

<img src="Images/Readme-Title.png" width="679" height="48"/>

[![Stars](https://img.shields.io/github/stars/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Stars)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/stargazers)
[![Forks](https://img.shields.io/github/forks/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Forks)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/network/members)
[![Release](https://img.shields.io/github/v/release/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Download)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest)
-----

**English** | [Français](README_FR.md)

## Contents

- [Configuration](#configuration)
- [What work ?](#what-work-)
- [Installation](#installation)
    - [Make the Installation USB](#make-the-installation-usb) 
    - [Setup the SMBIOS](#setup-the-smbios)
- [Credits](#credits)
- [Need help ?](#need-help-)

## Configuration

| Specifications | Detail |
| -------------- | ------ |
| Processor | Intel Core i5-7400 |
| Memory | 16GB DDR4 2400MHz |
| Hard Disk | Kingston SSD SATA 120GB |
| Integrated Graphics | Intel HD Graphics 630 |
| Monitor 1 | Acer Nitro XV240Y 165Hz 1ms |
| Monitor 2 | iiyama ProLite XB2483HSU |
| Bluetooth | TP-Link UB400 (Bluetooth 4.0 USB Dongle) |
| CD/DVD | LG GH24NSD DVD-RW |

## What work ?

| Service | State |
| ------- | ----- |
| HDMI | Working at 1920x1080@120Hz |
| DVI | Working at 1920x1080@60Hz |
| Ethernet | Working |
| iGPU | Working |
| DRM | Working partially ([see more info](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/issues/))
| Wi-Fi | Not Present on my configuration (may require extra setup)|
| Bluetooth | Working |
| USB | Working at maximum speed (USB 3.1/3.0/2.0) |
| iCloud | Working but requires your own SMBIOS |
| iMessage | Working but requires your own SMBIOS |
| FaceTime | Working but requires your own SMBIOS |
| Mac App Store | Working but requires your own SMBIOS |
| Handoff | Not working (Wi-Fi is needed and i don't have it) |

## Installation

### Make the Installation USB

Download [balenaEtcher](https://www.balena.io/etcher/) and the [macOS Monterey 12.4 Image](https://43dmj0-my.sharepoint.com/personal/roxor-007_43dmj0_onmicrosoft_com/Documents/OnedriveXbot/Olarila%20Monterey%2012.4.raw?ga=1).

Open balenaEtcher, select the `.raw` image you downloaded earlier, select the USB you want to use and click "Flash".

**NOTE : THIS WILL ERASE ALL THE DATA PRESENT ON YOUR USB, i'm not responsible for any loss of data.**

Once the flash is successfully completed, you will need to mount the EFI of your USB (search on Google if you need help).

Open the EFI of your USB and **delete everything** (the root of the EFI should be blank).

Now, [download this EFI](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/releases/latest) and paste the "EFI" folder at the root of the USB it should look like this :

![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)

Finally, your USB is ready but before using it you will have to [Setup the SMBIOS](#setup-the-smbios)

**⚠️ It will not boot if you skip this part, so make sure to follow the following steps carefully**

### Setup the SMBIOS

To use this EFI, you will need to setup the SMIOS to match your configuration.

| SMIOS | Hardware |
| ----- | -------- |
| iMac18,1 | Used for computers utilizing the iGPU for displaying |
| iMac18,3 | Used for computers using a dGPU for displaying, and an iGPU for computing tasks only |

Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS/archive/refs/heads/master.zip) and extract it.

If you're on Windows, execute "GenSMBIOS.bat".

If you're on macOS, execute "GenSMBIOS.command".

**NOTE : You need to have the [latest version of Python](https://www.python.org/downloads/) installed to run this program.**

Once the script is running, pick the option 1 for downloading MacSerial.

After that, pick option 3 for selecting the SMBIOS and enter "iMac18,1" or "iMac18,3" (without the quote) according to your configuration.

This will give you an output similar to the following : 

```
  #######################################################
 #               iMac18,1 SMBIOS Info                  #
#######################################################

Type:         iMac18,1
Serial:       C02FG0D5H7JY
Board Serial: C02112270CDH69FAD
SmUUID:       75609BAC-B4BF-4DC0-8D98-E09177474DB8
Apple ROM:    90B21FCE4687
```

The `Type` part gets copied to Generic -> SystemProductName.

The `Serial` part gets copied to Generic -> SystemSerialNumber.

The `Board Serial` part gets copied to Generic -> MLB.

The `SmUUID` part gets copied to Generic -> SystemUUID.

Don't use the `Apple ROM` part !

For Generic -> ROM, we use the MAC Address of the network interface, in all lowercase, and without `:`

**For example :**

**MAC :** `00:16:CB:00:11:22`
    
**ROM :** `0016cb001122`

**ℹ️ Remember to look on [Apple Check Coverage](https://checkcoverage.apple.com/) and you want to get a message back like : "Invalid Serial" or "Purshase Date not Validated". If it's not the case, you need to regenerate another serial.**

**NOTE : You and you alone are responsible for your Apple ID, read the guide carefully and take full responsibility if you screw up. Dortania, me and any other guides are not held accountable for what you do.**

## Credits

- Thanks to [Apple](https://apple.com) for [macOS](https://www.apple.com/macos/)
- Thanks to [Dortania](https://github.com/dortania) for [OpenCore Bootloader](https://dortania.github.io/)
- Thanks to [Acidanthera](https://github.com/acidanthera) for providing [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup), [Apple ALC](https://github.com/acidanthera/AppleALC), [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases/tag/2.6.2), [CPUFriend](https://github.com/acidanthera/CPUFriend), [IntelMausi](https://github.com/acidanthera/IntelMausi), [Lilu](https://github.com/acidanthera/Lilu), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), [WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- Thanks to [RehabMan](https://github.com/RehabMan) for providing [USBInjectAll](https://github.com/RehabMan/OS-X-USB-Inject-All)
- Thanks to [Olarila](https://www.olarila.com) for providing the [macOS Monterey 12.4 Image](https://43dmj0-my.sharepoint.com/personal/roxor-007_43dmj0_onmicrosoft_com/Documents/OnedriveXbot/Olarila%20Monterey%2012.4.raw?ga=1)
- Thanks to [Aurélien Audero](https://github.com/AurelienAudero) for building the [Intel i5-7400 Hackintosh EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI)

## Need help ?

Click [here](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose) to create an issue on GitHub.

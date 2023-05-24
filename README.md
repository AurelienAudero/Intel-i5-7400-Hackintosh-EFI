<img src="Images/Readme-Title.png" width="679" height="85"/>

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
    - [Setup the BIOS](#setup-the-bios)
- [Credits](#credits)
- [Need help ?](#need-help-)

## Configuration

| Specifications | Detail |
| -------------- | ------ |
| Processor | Intel Core i5-7400 |
| Memory | 16GB DDR4 2400MHz |
| Motherboard | MSI B250 Gaming Pro Carbon |
| Hard Disk | Kingston SSD SATA 120GB |
| Integrated Graphics | Intel HD Graphics 630 |
| Wi-Fi and Bluetooth Card | Broadcom BCM94360plus |
| Monitor 1 | Acer Nitro XV240Y 165Hz 1ms |
| Monitor 2 | iiyama ProLite XB2483HSU |
| CD/DVD | LG GH24NSD DVD-RW |

## What work ?

| Service | State |
| ------- | ----- |
| HDMI | Working at 1920x1080@120Hz |
| DVI | Working at 1920x1080@60Hz |
| Ethernet | Working at full speed |
| iGPU | Working |
| DRM | Working partially ([see more info](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/5)) |
| Wi-Fi | Working at full speed |
| Bluetooth | Working |
| USB | Working at full speed (up to USB 3.1) |
| Sleep | May work depending of your configuration |
| iCloud | Working |
| iMessage and FaceTime | Working |
| Handoff and Continuity | Working |
| Mac App Store | Working |

## Installation

### Make the Installation USB

Download [balenaEtcher](https://www.balena.io/etcher/) and the [macOS Ventura 13.4 Image](https://www.mediafire.com/file/7nwiwc08e1tbsjg/Olarila+Ventura+13.4.raw/file) (⚠️ It's recommanded to use an Ad Blocker ⚠️).

Open balenaEtcher, select the `.raw` image you downloaded earlier, select the USB you want to use and click "Flash".

**NOTE : THIS WILL ERASE ALL THE DATA PRESENT ON YOUR USB, PLEASE BACKUP IMPORTANTS FILES !**

Once the flash is successfully completed, you will need to mount the EFI of your USB (search on Google if you need help).

Open the EFI of your USB and **delete everything** (the root of the EFI should be blank).

Now, [download the latest version of this EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest) and paste the "EFI" folder at the root of the USB it should look like this :

![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)

Finally, your USB is ready but before using it you will have to [Setup the SMBIOS](#setup-the-smbios)

**⚠️ It will not boot if you skip this part, so make sure to follow the following steps carefully**

### Setup the SMBIOS

To use this EFI, you will need to setup the SMIOS to match your configuration.

| SMIOS | Hardware |
| ----- | -------- |
| iMac18,1 | Used for computers utilizing the iGPU for displaying |
| iMac18,3 | Used for computers using a dGPU for displaying, and an iGPU for computing tasks only |
| Macmini8,1 | Used for computers having issues with iMac18,1 and that are utilizing the iGPU for displaying |

Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS/archive/refs/heads/master.zip) and extract it.

If you're on Windows, execute "GenSMBIOS.bat".

If you're on macOS, execute "GenSMBIOS.command".

**NOTE : You need to have the [latest version of Python](https://www.python.org/downloads/) installed to run this program.**

Once the script is running, pick the option 1 for downloading MacSerial.

After that, pick option 3 for selecting the SMBIOS and enter `iMac18,1` or `iMac18,3` or `Macmini8,1` (case sensitive) according to your configuration.

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

The `Type` part gets copied to `Generic -> SystemProductName`.

The `Serial` part gets copied to `Generic -> SystemSerialNumber`.

The `Board Serial` part gets copied to `Generic -> MLB`.

The `SmUUID` part gets copied to `Generic -> SystemUUID`.

Don't use the `Apple ROM` part !

For `Generic -> ROM`, we use the MAC Address of the network interface, in all lowercase, and without `:`

**For example :**
- **MAC :** `00:16:CB:00:11:22`
- **ROM :** `0016cb001122`

**ℹ️ Remember to look on [Apple Check Coverage](https://checkcoverage.apple.com/) and you want to get this message back : "We’re sorry, we’re unable to check coverage for this serial number". If it's not the case, you need to regenerate another serial.**

**ℹ️ If you choose the `Macmini8,1` SMBIOS, it's recommanded to change the value in `Misc -> Security -> SecureBootModel` to `j174` in the config.plist**

**⚠️ NOTE : You and you alone are responsible for your Apple ID, read the guide carefully and take full responsibility if you screw up. Dortania, me and any other guides are not held accountable for what you do.**

### Setup the BIOS
**ℹ️ NOTE : All of these options may not be present in your BIOS, it is recommended to match as closely as possible but don't be too concerned if many of these options are not available in your BIOS.**

| ❌ You should disable | ✅ You should enable |
|-----------------------|----------------------|
| Fast Boot             | VT-x                 |
| Secure Boot           | Above 4G Decoding    |
| Serial/COM Port       | Hyper-Threading      |
| Parallel Port         | Execute Disable Bit  |
| VT-d                  | EHCI/XHCI Handoff    |
| CSM                   |                      |
| Thunderbolt           |                      |
| Intel SGX             |                      |
| Intel Platform Trust  |                      |
| CFG Lock              |                      |

|                🛠️ Settings you should change              |
|-----------------------------------------------------------|
| **OS Type :** `Windows 8.1/10 UEFI Mode` (or `Other OS`)  |
| **DVMT Pre-Allocated (iGPU Memory) :** `128MB` or higher  |
| **SATA Mode :** `AHCI`                                    |

## Credits

- Thanks to [Apple](https://apple.com) for [macOS](https://www.apple.com/macos/)
- Thanks to [Dortania](https://github.com/dortania) for [OpenCore Bootloader](https://dortania.github.io/) and for providing [CtlnaAHCIPort](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/CtlnaAHCIPort.kext.zip)
- Thanks to [Acidanthera](https://github.com/acidanthera) for providing [Apple ALC](https://github.com/acidanthera/AppleALC), [CPUFriend](https://github.com/acidanthera/CPUFriend), [CpuTscSync](https://github.com/acidanthera/CpuTscSync), [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock), [IntelMausi](https://github.com/acidanthera/IntelMausi), [Lilu](https://github.com/acidanthera/Lilu), [VirtualSMC](https://github.com/acidanthera/VirtualSMC) and [WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- Thanks to [Olarila](https://www.olarila.com) for providing the [macOS Ventura 13.4 Image](https://www.mediafire.com/file/7nwiwc08e1tbsjg/Olarila+Ventura+13.4.raw/file)
- Thanks to [Aurélien Audero](https://github.com/AurelienAudero) for building the [Intel i5-7400 Hackintosh EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI)

## Need help ?

Click [here](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose) to create an issue on GitHub.

If you have a question, you can create a thread [here](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose)

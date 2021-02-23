# i5-7400-EFI-by-Aure

This is an EFI Folder optimized for the setup specified below, you can use it for you Hackintosh.

It uses Opencore 0.6.6 as bootloader.

When you're first booting to this EFI Folder, you automatically agree to [The Terms and Conditions of Uses](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/LICENSE.md).

**FOLLOW THE INSTRUCTIONS BELOW THE SCREENSHOTS BEFORE BOOTING !**

## Screenshots

![Global-View-of-System](/Images/Global-View-of-System.png)

![About-This-Mac](/Images/About-This-Mac.png)

![System-Report-USB](/Images/System-Report-USB.png)

![System-Report-Displays](/Images/System-Report-Displays.png)

## Recommandation

### 1

Don't Update macOS unless you've update Opencore, The Drivers and the Config.plist by your own or you use an updated version of this EFI that is compatible with the version to the which one you want to update.

### 2

Keep a local backup of your EFI and don't modify the config.plist with Opencore Configurator (it can break the EFI and make macOS unbootable).

Don't use Clover Configurator too (It will add Clover Specifics Things to the config.plist and can break the EFI too.

### 3

If you boot Windows from Opencore, do this at your own risks !

It can cause blue screens (BSOD), can make Windows unstable or make Windows unbootable.

Windows can also thinks that you're using Windows on a real Mac using Bootcamp due to Opencore that injects SSDTs in Windows while booting with it.

## Setup
| Parts       | Model                               |
|-------------|-------------------------------------|
| OS          | macOS Big Sur 11.1 (20C69)          |
| Bootloader  | Opencore 0.6.6                      |
| Motherboard | MSI GAMING PRO CARBON B250          |
| Processor   | Intel Core i5-7400 @3.0Ghz          |
| GPU         | Intel HD Graphics 630               |
| RAM         | 1x 8Go 2400MHz DDR4                 |
| Hard Drive  | Western Digital HDD Caviar Blue 1TB |

## What's works

| Service               | State                                                                                                                  |
|-----------------------|------------------------------------------------------------------------------------------------------------------------|
| OS in General         | Working                                                                                                                |
| Dark Mode             | Working                                                                                                                |
| Windows Dualboot      | Unstable ! Requires [config.plist edition](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure#windows-dual-boot)    |
| iGPU (HD 630)         | Working                                                                                                                |
| Graphics Acceleration | Working                                                                                                                |
| iCloud                | Working but requires your own SMBIOS                                                                                   |
| iMessage              | Not Tested but requires your own SMBIOS                                                                                |
| FaceTime              | Not Tested but requires you own SMBIOS                                                                                 |
| Mac AppStore          | Working but requires your own SMBIOS                                                                                   |
| Wi-Fi                 | Not Tested but non present on the motherboard by default                                                               |
| Bluetooth             | Not Tested but non present on the motherboard by default                                                               |

## SMBIOS

| Model    | Usage                                                                                                      |
|----------|------------------------------------------------------------------------------------------------------------|
| iMac18,1 | Use this for utilizing iGPU (HD 630) for Displaying                                                        |
| iMac18,3 | Use this for utilizing dGPU (AMD or NVIDIA) for Displaying, GPU-Intensive Tasks and iGPU for Compute Tasks |

For generate an SMBIOS, refer to the guide at [The Official Opencore Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/kaby-lake.html#platforminfo) and follow the instructions in the blue rectangle.

## Windows Dual-Boot

### Method 1 (Low Risk, Recommanded)

Tap on F11 on Startup to choose where to boot (Windows or macOS)

### Method 2 (High Risk, Don't recommanded !)

Change the boot order in your motherboard's BIOS/UEFI to boot first on Opencore.

Now mount your EFI with Opencore configurator (But don't use it to modify your EFI !) and go to your EFI Folder > OC.

Edit your "config.plist" with "TextEdit" or you're favorite text editor and search for "ScanPolicy" and change the value to "0".

It will now show Windows in the bootloader. You this method at your own risk [as specified on top of this document](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure#recommandation)

## Fix Clock in Windows

When you're dualbooting and Linux-based Operating System or a macOS System with Windows, it can have break the clock in Windows.

To fix that, you can modify a registry key in Windows Registry.

Go to "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" and modify the DWORD value named "RealTimeIsUniversal" to "1".

If the the DWORD value "RealTimeIsUniversal" is not present in this directory, create a "DWORD (32-Bit Value) and call it "RealTimeIsUniversal" (case-sensitive).

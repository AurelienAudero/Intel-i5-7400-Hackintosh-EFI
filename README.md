# i5-7400-EFI-by-Aure

This is an EFI Folder optimized for the setup specified below, you can use it for you Hackintosh.

It uses Clover as bootloader.

**⚠️ FOLLOW THE INSTRUCTIONS AT [CONFIGURATION CHAPTER](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure#configuration) BEFORE BOOTING ⚠️**

**⚠️ This EFI is INCOMPATIBLE with macOS Big Sur** *If you want to use it, you need to upgrade to macOS Monterey 12.0 Beta (21A5248p)*

## Why i switched from Opencore to Clover

Clover provide more stability than Opencore for this system, Clover is a lot more user-friendly too and it's easier for you to create your EFI based on this one ([Legal details about creating your own EFI based on this one](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/blob/master/Share-LICENSE.md)).

With Clover, you can modify EFI using Clover Configurator with less risks of breaking a thing and FINALLY boot to Windows WITHOUT ANY PROBLEMS 🎉

When you're first booting to this EFI Folder, you automatically agree to [The Terms and Conditions of Uses](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/blob/master/LICENSE).

## Screenshots

![About-This-Mac](/Images/About-This-Mac.png)

![System-Report-Displays](/Images/System-Report-Displays.png)

## Recommandation

### 1

Don't Update macOS unless you've update Clover, the drivers and the kexts by your own or you use an updated version of this EFI that is compatible with the version to the which one you want to update.

### 2

Keep a local backup of your EFI.

## Setup
| Parts       | Model                               |
|-------------|-------------------------------------|
| OS          | macOS Monterey 12.0 Beta (21A5248p) |
| Bootloader  | Clover Bootloader r5137             |
| Motherboard | MSI GAMING PRO CARBON B250          |
| Processor   | Intel Core i5-7400 @3.0Ghz          |
| GPU         | Intel HD Graphics 630               |
| RAM         | 1x 8Go 2400MHz DDR4                 |
| Hard Drive  | Kingston A400 SSD 120Go             |

## What's works

| Service               | State                                                                                                                        |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------|
| OS in General         | Working                                                                                                                      |
| Dark Mode             | Working                                                                                                                      |
| Windows Dualboot      | Working                                                                                                                      |
| iGPU (HD 630)         | Working (In some cases, if you use 2 or more monitors, you may get a bug, [Learn More about here](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/issues/2))|
| Graphics Acceleration | Working                                                                                                                      |
| iCloud                | Working but requires your own SMBIOS                                                                                         |
| iMessage              | Working but requires your own SMBIOS                                                                                         |
| FaceTime              | Working but requires you own SMBIOS                                                                                          |
| Mac AppStore          | Working but requires your own SMBIOS                                                                                         |
| Wi-Fi                 | Not Tested but non present on the motherboard by default                                                                     |
| Bluetooth             | Working but non present on the motherboard by default (TPLink UB400 USB Adapter used)                                        |

## Configuration

1) Download the latest version of this EFI by clicking on [Releases](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/releases)
2) Extract the downloaded archive
3) Delete ALL the content in the extracted folder EXCEPT the folder named "EFI"
4) Go to EFI -> CLOVER and Edit "config.plist" with a text editor (Default Windows Notepad, Visual Studio Code, Notepad++, ...)
5) Go to the following page by clicking [HERE](https://github.com/corpnewt/GenSMBIOS)
6) On the new opened page, click on the "⬇️ CODE" green button and click "Download ZIP"
7) Exract the downloaded archive
8) Run "GenSMBIOS.bat" with admin rights on Windows or simply double click on "GenSMBIOS.command" on macOS/Linux
9) Press "1" and press "Enter" key and wait until you are back to the home screen
10) Press "3" and press "Enter" key
11) Type "MacPro7,1" (case-sensitive) and press "Enter" key
12) You will get 4 lines like [this](https://github.com/AurelienAudero/i5-7400-EFI-by-Aure/blob/master/Images/GenSMBIOS-CopyPaste-Screen.png)
13) Make a search with "CTRL + F" or "CMD + F"
14) Type "{Serial}" in the Search field (case-sensitive)
15) Copy what's show after "Serial: " in the Command Prompt/Terminal
16) Replace {Serial} ("{}" included) with the content you copied
17) Make another search with "CTRL + F" or "CMD + F"
18) Type "{Board Serial}" in the Search field (case-sensitive)
19) Copy what's show after "Board Serial: " in the Command Prompt/Terminal
20) Replace {Board Serial} ("{}" included) with the content you copied
21) Make a last search with "CTRL + F" or "CMD + F"
22) Type "{SmUUID}" in the Search field (case-sensitive)
23) Copy what's show after "SmUUID: " in the Command Prompt/Terminal
24) Replace {SmUUID} ("{}" included) with the content you copied
25) Save the "config.plist" file
26) Go back to the Command Prompt/Terminal
27) Press "Enter" key
28) Press "Q" and "Enter key" again
29) You can close the Command Prompt/Terminal window
30) Mount the EFI of your USB (use Clover Configurator on macOS, search with Google for Windows or Linux)
31) Delete the "EFI" of USB (⚠️ DON'T DO "Replace", DELETE AND COPY IT ⚠️)
32) Copy the EFI that we made above on the USB Drive (where the old "EFI" Folder was)
33) Eject the EFI Partition you mounted previously
34) 🎉 YOU CAN NOW BOOT FROM YOUR USB

## Fix Clock in Windows

When you're dualbooting a Linux-based Operating System or a macOS System with Windows, it can break the clock in Windows.

To fix that, you can modify a registry key in Windows Registry.

Go to "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" and modify the DWORD value named "RealTimeIsUniversal" to "1".

If the the DWORD value "RealTimeIsUniversal" is not present in this directory, create a "DWORD (32-Bit Value) and call it "RealTimeIsUniversal" (case-sensitive).

<img src="Images/Readme-Title.png" width="679" height="85"/>

[![Stars](https://img.shields.io/github/stars/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Stars)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/stargazers)
[![Forks](https://img.shields.io/github/forks/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Forks)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/network/members)
[![Release](https://img.shields.io/github/v/release/AurelienAudero/Intel-i5-7400-Hackintosh-EFI?label=Download)](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest)
-----

[English](README.md) | **Français**

## Sommaire

- [Configuration](#configuration)
- [Qu'est-ce qui fonctionne ?](#quest-ce-qui-fonctionne-)
- [Installation](#installation)
    - [Créer la clé USB d'installation](#créer-la-clé-usb-dinstallation) 
    - [Configurer le SMBIOS](#configurer-le-smbios)
    - [Configurer le BIOS](#configurer-le-bios)
    - [Post-installation](#post-installation)
- [Crédits](#crédits)
- [Besoin d'aide ?](#besoin-daide-)

## Configuration

| Spécifications | Détail |
| -------------- | ------ |
| Processeur | Intel Core i5-7400 |
| Mémoire RAM | 16GB DDR4 2400MHz |
| Carte Mère | MSI B250 Gaming Pro Carbon |
| Disque Dur macOS | Crucial BX500 480GB (SSD SATA) |
| Autres Disques Durs | <ul><li>Crucial P5 Plus 1To (NVMe PCIe Gen 4)</li><li>Kingston A400 120GB (SSD SATA)</li><li>Western Digital Blue 1To 3.5" 7200RPM (HDD SATA) |
| Graphiques Intégrés | Intel HD Graphics 630 |
| Carte Wi-Fi et Bluetooth | Broadcom BCM94360plus |
| Moniteur 1 | Acer Nitro XV240Y 165Hz 1ms |
| Moniteur 2 | iiyama ProLite XB2483HSU |
| CD/DVD | LG GH24NSD DVD-RW |

## Qu'est-ce qui fonctionne ?

| Service | État |
| ------- | ---- |
| HDMI | Fonctionnel à 1920x1080@120Hz |
| DVI | Fonctionnel à 1920x1080@60Hz |
| Ethernet | Fonctionnel à pleine vitesse |
| iGPU | Fonctionnel |
| DRM | Partiellement fonctionnel ([voir plus d'infos](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/5))
| Wi-Fi | Fonctionnel ([nécéssite un patch - voir plus d'infos](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/25)) |
| Bluetooth | Fonctionnel |
| USB | Fonctionnel à pleine vitesse (jusqu'à USB 3.1) |
| Sleep | Peut fonctionner selon votre configuration |
| iCloud | Fonctionnel |
| iMessage et FaceTime | Fonctionnel |
| Handoff et Continuité | Fonctionnel ([nécéssite un patch - voir plus d'infos](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/25)) |
| Mac App Store | Fonctionnel |

## Installation

### Créer la clé USB d'installation

1. Téléchargez [balenaEtcher](https://www.balena.io/etcher/) et [l'image de macOS Sonoma 14.3.1](https://www.mediafire.com/file/ir55u3ldpk7hqbf/Olarila+Sonoma+14.3.1.raw/file) (⚠️ Il est recommandé d'utiliser un bloqueur de pub ⚠️).
2. Ouvrez balenaEtcher, sélectionnez l'image `.raw` téléchargée plus tôt, sélectionnez la clé USB que vous souhaitez utiliser et cliquez sur "Flash".
> **⚠️ CELA VA EFFACER TOUT LE CONTENUE SUR VOTRE CLÉ USB, VEUILLEZ SAUVERGARDER VOS DONNÉES IMPORTANTES !**
3. Une fois que le flash s'est terminé avec succès, vous devez monter l'EFI de votre clé USB (chercher sur Google si vous avez besoin d'aide).
4. Ouvrez l'EFI de votre clé USB et **supprimer tout** (la racine de l'EFI doit être vide).
5. [Téléchargez la dernière version de cet EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest) et collez-le à la racine de la clé USB
> Cela doit ressembler à ça :
> ![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)

Votre clé USB est prête mais avant de l'utiliser vous devez [Configurer le SMBIOS](#configurer-le-smbios)

> **⚠️ Cela ne démarrera pas si vous passez cette partie, veuillez donc suivre les étapes suivantes avec attention**

### Configurer le SMBIOS

Pour utiliser cette EFI, vous avez besoin de configurer le SMBIOS.

1. Téléchargez [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) et extrayez-le.
2. Lancez le programme en exécutant `GenSMBIOS.bat` si vous êtes sous Windows ou `GenSMBIOS.command` si vous êtes sous macOS.
3. Une fois le script en cours d'exécution, choisissez l'option 1 pour télécharger MacSerial.
4. Choisissez l'option 3 pour sélectionner le SMBIOS et entrez `Macmini8,1` (sensible à la casse).

> Cela vous donnera une sortie similaire à la suivante :
> 
> ```
>   #######################################################
>  #              Macmini8,1 SMBIOS Info                 #
> #######################################################
> 
> Type:         Macmini8,1
> Serial:       C07LNUYMJYVX
> Board Serial: C07345500CDKXPGJC
> SmUUID:       C58DD217-9C50-439D-9D72-E81D99DBB062
> Apple ROM:    903C92E450A1
> ```

5. Vérifiez le numéro de série généré sur [Apple Check Coverage](https://checkcoverage.apple.com/). Vous devez recevoir ce message : "Nous sommes désolés, mais nous ne pouvons pas consulter la couverture associée à ce numéro de série". Si vous ne l'obtenez pas, vous devez régénérer un autre numéro de série.
6. En utilisant [ProperTree](https://github.com/corpnewt/ProperTree), modifiez votre fichier `config.plist` en utilisant la sortie donnée par GenSMBIOS :
    - La partie `Type` doit être copiée dans `Generic -> SystemProductName`.
    - La partie `Serial` doit être copiée dans `Generic -> SystemSerialNumber`.
    - La partie `Board Serial` doit être copiée dans `Generic -> MLB`.
    - La partie `SmUUID` doit être copiée dans `Generic -> SystemUUID`.
    - N'utilisez pas la partie `Apple ROM` !
    - Pour `Generic -> ROM`, on utilise l'adresse MAC de l'interface réseau, en minuscules, et sans `:`

> **ℹ️ Par exemple :**
> - **MAC :** `00:16:CB:00:11:22`
> - **ROM :** `0016cb001122`
>
> **⚠️ NOTE ET AVERTISSEMENTS :**
> - Vous avez besoin d'avoir [la dernière version de Python](https://www.python.org/downloads/) installée pour utiliser GenSMBIOS.**
> - Vous et vous seul êtes responsable de votre Identifiant Apple, lisez attentivement le guide et assumez l'entière responsabilité si vous vous trompez. Dortania, moi et tous les autres guides ne pourront pas être tenus responsables de ce que vous faites.


### Configurer le BIOS

>**ℹ️ NOTE :**
> - Certaines de ces options peuvent ne pas être présentes dans votre BIOS, il est recommandé de les faire correspondre le plus précisément possible mais ne vous inquiétez pas trop si bon nombre de ces options ne sont pas disponibles dans votre BIOS.
> - Il est recommandé de changer la langue de votre BIOS en Anglais lors de sa configuration. Vous pouvez le remettre dans votre langue préférée une fois les modifications effectuées.

| ❌ Vous devez désactiver | ✅ Vous devez activer |
|--------------------------|-----------------------|
| Fast Boot                | VT-x                  |
| Secure Boot              | Above 4G Decoding     |
| Serial/COM Port          | Hyper-Threading       |
| Parallel Port            | Execute Disable Bit   |
| VT-d                     | EHCI/XHCI Handoff     |
| CSM                      |                       |
| Thunderbolt              |                       |
| Intel SGX                |                       |
| Intel Platform Trust     |                       |
| CFG Lock                 |                       |

|           🛠️ Paramètres que vous devez changer           |
|----------------------------------------------------------|
| **OS Type :** `Windows 8.1/10 UEFI Mode` (ou `Other OS`) |
| **DVMT Pre-Allocated (iGPU Memory) :** `128MB` ou plus   |
| **SATA Mode :** `AHCI`                                   |

### Post-Installation
1. Montez l'EFI du disque dur sur lequel macOS est installé.
2. Montez l'EFI de la clé USB que vous avez utilisé pour installer macOS.
3. Copiez tout le contenu de la partition EFI de la clé USB vers l'EFI du disque dur sur lequel macOS est installé.
> Cela doit ressembler à ça :
> ![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)
4. Vous pouvez maintenant démarrer directement à partir de votre disque dur.

## Crédits

- Merci à [Apple](https://apple.com) pour [macOS](https://www.apple.com/macos/)
- Merci à [Acidanthera](https://github.com/acidanthera) de fournir [Apple ALC](https://github.com/acidanthera/AppleALC), [CPUFriend](https://github.com/acidanthera/CPUFriend), [CpuTscSync](https://github.com/acidanthera/CpuTscSync), [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock), [IntelMausi](https://github.com/acidanthera/IntelMausi), [Lilu](https://github.com/acidanthera/Lilu), [NVMeFix](https://github.com/acidanthera/NVMeFix), [OpenCore Bootloader](https://github.com/acidanthera/OpenCorePkg), [VirtualSMC](https://github.com/acidanthera/VirtualSMC) et [WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- Merci à [Dortania](https://github.com/dortania) de fournir [AMFIPass](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Acidanthera/AMFIPass-v1.4.0-RELEASE.zip), [CtlnaAHCIPort](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/CtlnaAHCIPort.kext.zip), [IO80211FamilyLegacy](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip), [IOSkywalkFamily](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IOSkywalkFamily-v1.1.0.zip) and [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)
- Merci à [Olarila](https://www.olarila.com) de fournir [l'image de macOS Sonoma 14.0](https://www.mediafire.com/file/wio1f0s9e8bzyiw/Olarila+Sonoma.raw/file)
- Merci à [Aurélien Audero](https://github.com/AurelienAudero) pour la conception de [Intel i5-7400 Hackintosh EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI)

## Besoin d'aide ?

Cliquez [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose) pour créer une issue sur GitHub.

Si vous avez une question, vous pouvez la poser [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose)

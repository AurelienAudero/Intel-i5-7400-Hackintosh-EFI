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
- [Crédits](#crédits)
- [Besoin d'aide ?](#besoin-daide-)

## Configuration

| Spécifications | Détail |
| -------------- | ------ |
| Processeur | Intel Core i5-7400 |
| Mémoire RAM | 16GB DDR4 2400MHz |
| Carte Mère | MSI B250 Gaming Pro Carbon |
| Disque Dur | Kingston SSD SATA 120GB |
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
| DRM | Partiellement Fonctionnel ([Voir plus d'infos](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/5))
| Wi-Fi | Fonctionnel à pleine vitesse |
| Bluetooth | Fonctionnel |
| USB | Fonctionnel à pleine vitesse (jusqu'à USB 3.1) |
| Sleep | Peut fonctionner selon votre configuration |
| iCloud | Fonctionnel |
| iMessage et FaceTime | Fonctionnel |
| Handoff et Continuité | Fonctionnel |
| Mac App Store | Fonctionnel |

## Installation

### Créer la clé USB d'installation

Télécharger [balenaEtcher](https://www.balena.io/etcher/) et [l'image de macOS Ventura 13.0](https://www.mediafire.com/file/h4b95ayw359163w/Olarila+Ventura.raw/file) (⚠️ Il est recommandé d'utiliser un bloqueur de pub ⚠️).

Ouvrez balenaEtcher, sélectionnez l'image `.raw` téléchargée plus tôt, sélectionnez la clé USB que vous souhaitez utiliser et cliquez sur "Flash".

**NOTE : CELA VA EFFACER TOUT LE CONTENUE SUR VOTRE CLÉ USB, VEUILLEZ SAUVERGARDER VOS DONNÉES IMPORTANTES !**

Une fois que le flash s'est terminé avec succès, vous devez monter l'EFI de votre clé USB (chercher sur Google si vous avez besoin d'aide).

Ouvrez l'EFI de votre clé USB et **supprimer tout** (la racine de l'EFI doit être vide).

Maintenant, [télécharger la dernière version de cet EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest) et coller-le à la racine de la clé USB, cela doit ressembler à ça :

![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)

Votre clé USB est prête mais avant de l'utiliser vous devez [Configurer le SMBIOS](#configurer-le-smbios)

**⚠️ Cela ne démarrera pas si vous passez cette partie, veuillez donc suivre les étapes suivantes avec attention**

### Configurer le SMBIOS

Pour utiliser cette EFI, vous avez besoin de configurer le SMBIOS en fonction de votre configuration.

| SMIOS | Matériel |
| ----- | -------- |
| iMac18,1 | Utilisé pour les ordinateurs utilisant l'iGPU pour l'affichage |
| iMac18,3 | Utilisé pour les ordinateurs utilisant une carte graphique dédiée (dGPU) pour l'affichage, et l'iGPU pour les tâches informatiques uniquement |
| Macmini8,1 | Utilisé pour les ordinateurs ayant des problèmes avec iMac18,1 et qui utilisent l'iGPU pour l'affichage |

Télécharger [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS/archive/refs/heads/master.zip) et l'extraire.

Si vous êtes sur Windows, exécutez "GenSMBIOS.bat".

Si vous êtes sur macOS, exécutez "GenSMBIOS.command".

**NOTE : Vous avez besoin d'avoir [la dernière version de Python](https://www.python.org/downloads/) installée pour utiliser ce programme.**

Une fois le programme ouvert, utilisez l'option 1 pour télécharger MacSerial.

Après ça, choissisez l'option 3 pour séléctionner le SMBIOS et entrer "iMac18,1" ou "iMac18,3" (sans les guillemets) en fonction de votre configuration

Cela vous donnera une sortie similaire à la suivante :

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

La partie `Type` doit être copiée dans `Generic -> SystemProductName`.

La partie `Serial` doit être copiée dans `Generic -> SystemSerialNumber`.

La partie `Board Serial` doit être copiée dans `Generic -> MLB`.

La partie `SmUUID` doit être copiée dans `Generic -> SystemUUID`.

N'utilisez pas la partie `Apple ROM` !

Pour `Generic -> ROM`, on utilise l'adresse MAC de l'interface réseau, en minuscules, et sans `:`

**Par exemple :**
- **MAC :** `00:16:CB:00:11:22`
- **ROM :** `0016cb001122`

**ℹ️ Rappelez vous de regarder sur [Apple Check Coverage](https://checkcoverage.apple.com/) and vous devez avoir ce message : "Nous sommes désolés, mais nous ne pouvons pas consulter la couverture associée à ce numéro de série". Si cela n'est pas le cas, vous devez regénérer d'autres numéros.**

**ℹ️ Si vous choissisez `Macmini8,1` comme SMBIOS, il est recommandé de changer la valeur dans `Misc -> Security -> SecureBootModel` à `j174` dans le config.plist**

**⚠️ NOTE : Vous et vous seul êtes responsable de votre Identifiant Apple, lisez attentivement le guide et assumez l'entière responsabilité si vous vous trompez. Dortania, moi et tous les autres guides ne pourront pas être tenus responsables de ce que vous faites.**

### Setup the BIOS
**ℹ️ NOTE : Certaines de ces options peuvent ne pas être présentes dans votre BIOS, il est recommandé de les faire correspondre le plus précisément possible mais ne vous inquiétez pas trop si bon nombre de ces options ne sont pas disponibles dans votre BIOS.**

**⚠️ NOTE : Il est fortement recommandé de changer la langue de votre BIOS en Anglais le temps de configurer le BIOS. Vous pourrez le remettre en Français une fois les modifications effectuées.**$

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

## Crédits

- Merci à [Apple](https://apple.com) pour [macOS](https://www.apple.com/macos/)
- Merci à [Dortania](https://github.com/dortania) pour [OpenCore Bootloader](https://dortania.github.io/) et pour fournir [CtlnaAHCIPort](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/CtlnaAHCIPort.kext.zip)
- Merci à [Acidanthera](https://github.com/acidanthera) pour fournir [Apple ALC](https://github.com/acidanthera/AppleALC), [CPUFriend](https://github.com/acidanthera/CPUFriend), [CpuTscSync](https://github.com/acidanthera/CpuTscSync), [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock), [IntelMausi](https://github.com/acidanthera/IntelMausi), [Lilu](https://github.com/acidanthera/Lilu), [VirtualSMC](https://github.com/acidanthera/VirtualSMC) et [WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- Merci à [Olarila](https://www.olarila.com) pour fournir [l'image de macOS Ventura 13.0](https://www.mediafire.com/file/h4b95ayw359163w/Olarila+Ventura.raw/file)
- Merci à [Aurélien Audero](https://github.com/AurelienAudero) pour la conception de [Intel i5-7400 Hackintosh EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI)

## Besoin d'aide ?

Cliquez [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose) pour créer une issue sur GitHub.

Si vous avez une question, vous pouvez la poser [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose)

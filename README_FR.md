<img src="Images/Readme-Title.png" width="679" height="48"/>

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
- [Crédits](#crédits)
- [Besoin d'aide ?](#besoin-daide-)

## Configuration

| Spécifications | Détail |
| -------------- | ------ |
| Processeur | Intel Core i5-7400 |
| Mémoire RAM | 16GB DDR4 2400MHz |
| Disque Dur | Kingston SSD SATA 120GB |
| Graphiques Intégrés | Intel HD Graphics 630 |
| Moniteur 1 | Acer Nitro XV240Y 165Hz 1ms |
| Moniteur 2 | iiyama ProLite XB2483HSU |
| Bluetooth | TP-Link UB400 (Bluetooth 4.0 USB Dongle) |
| CD/DVD | LG GH24NSD DVD-RW |

## Qu'est-ce qui fonctionne ?

| Service | État |
| ------- | ---- |
| HDMI | Fonctionnel à 1920x1080@120Hz |
| DVI | Fonctionnel à 1920x1080@60Hz |
| Ethernet | Fonctionnel |
| iGPU | Fonctionnel |
| DRM | Partiellement Fonctionnel ([Voir plus d'infos](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/5))
| Wi-Fi | Non présent sur ma configuration (peut nécessiter une configuration supplémentaire)|
| Bluetooth | Fonctionnel |
| USB | Fonctionnel à la vitesse maximale (USB 3.1/3.0/2.0) |
| iCloud | Fonctionnel mais nécéssite votre propre SMBIOS |
| iMessage | Fonctionnel mais nécéssite votre propre SMBIOS |
| FaceTime | Fonctionnel mais nécéssite votre propre SMBIOS |
| Mac App Store | Fonctionnel mais nécéssite votre propre SMBIOS |
| Handoff | Non fonctionnel (le Wi-Fi est nécéssaire et je n'en ai pas) |

## Installation

### Créer la clé USB d'installation

Télécharger [balenaEtcher](https://www.balena.io/etcher/) et [l'image de macOS Monterey 12.4](https://43dmj0-my.sharepoint.com/personal/roxor-007_43dmj0_onmicrosoft_com/Documents/OnedriveXbot/Olarila%20Monterey%2012.4.raw?ga=1).

Ouvrez balenaEtcher, sélectionnez l'image `.raw` téléchargée plus tôt, sélectionnez la clé USB que vous souhaitez utiliser et cliquez sur "Flash".

**NOTE : CELA VA EFFACER TOUT LE CONTENUE SUR VOTRE CLÉ USB, je ne suis pas responsable de toute perte de données.**

Une fois que le flash s'est terminé avec succès, vous devez monter l'EFI de votre clé USB (chercher sur Google si vous avez besoin d'aide).

Ouvrez l'EFI de votre clé USB et **supprimer tout** (la racine de l'EFI doit être vide).

Maintenant, [télécharger cet EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/releases/latest) et coller-le à la racine de la clé USB, cela doit ressembler à ça :

![EFI-directory-Screenshot](/Images/EFI-directory-Screenshot.png)

Votre clé USB est prête mais avant de l'utiliser vous devez [Configurer le SMBIOS](#configurer-le-smbios)

**⚠️ Cela ne démarrera pas si vous passez cette partie, veuillez donc suivre les étapes suivantes avec attention**

### Configurer le SMBIOS

Pour utiliser cette EFI, vous avez besoin de configurer le SMBIOS en fonction de votre configuration.

| SMIOS | Matériel |
| ----- | -------- |
| iMac18,1 | Utilisé pour les ordinateurs utilisant l'iGPU pour l'affichage |
| iMac18,3 | Utilisé pour les ordinateurs utilisant une carte graphique dédiée (dGPU) pour l'affichage, et l'iGPU pour les tâches informatiques uniquement |

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

La partie `Type` doit être copiée dans Generic -> SystemProductName.

La partie `Serial` doit être copiée dans Generic -> SystemSerialNumber.

La partie `Board Serial` doit être copiée dans Generic -> MLB.

La partie `SmUUID` doit être copiée dans Generic -> SystemUUID.

N'utilisez pas la partie `Apple ROM` !

Pour Generic -> ROM, on utilise l'adresse MAC de l'interface réseau, en minuscules, et sans `:`

**Par exemple :**
- **MAC :** `00:16:CB:00:11:22`
- **ROM :** `0016cb001122`

**ℹ️ Rappelez vous de regarder sur [Apple Check Coverage](https://checkcoverage.apple.com/) and vous devez avoir un message comme : "Invalid Serial" or "Purshase Date not Validated". Si cela n'est pas le cas, vous devez regénérer d'autres numéros.**

**NOTE : Vous et vous seul êtes responsable de votre Identifiant Apple, lisez attentivement le guide et assumez l'entière responsabilité si vous vous trompez. Dortania, moi et tous les autres guides ne pourront pas être tenus responsables de ce que vous faites.**

## Crédits

- Merci à [Apple](https://apple.com) pour [macOS](https://www.apple.com/macos/)
- Merci à [Dortania](https://github.com/dortania) pour [OpenCore Bootloader](https://dortania.github.io/)
- Merci à [Acidanthera](https://github.com/acidanthera) pour fournir [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup), [Apple ALC](https://github.com/acidanthera/AppleALC), [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases/tag/2.6.2), [CPUFriend](https://github.com/acidanthera/CPUFriend), [IntelMausi](https://github.com/acidanthera/IntelMausi), [Lilu](https://github.com/acidanthera/Lilu), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), [WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- Merci à [RehabMan](https://github.com/RehabMan) pour fournir [USBInjectAll](https://github.com/RehabMan/OS-X-USB-Inject-All)
- Merci à [Olarila](https://www.olarila.com) pour fournir [l'image de macOS Monterey 12.4](https://43dmj0-my.sharepoint.com/personal/roxor-007_43dmj0_onmicrosoft_com/Documents/OnedriveXbot/Olarila%20Monterey%2012.4.raw?ga=1)
- Merci à [Aurélien Audero](https://github.com/AurelienAudero) pour la conception de [Intel i5-7400 Hackintosh EFI](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI)

## Besoin d'aide ?

Cliquez [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose) pour créer une issue sur GitHub.

Si vous avez une question, vous pouvez la poser [ici](https://github.com/AurelienAudero/Intel-i5-7400-Hackintosh-EFI/issues/new/choose)

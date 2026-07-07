# 🔌 Switch_NDIS_basic - Basculement mode réseau Raspberry Pi Zero

![Bash](https://img.shields.io/badge/Bash-5%2B-informational?style=for-the-badge)
![PHP](https://img.shields.io/badge/PHP-8%2B-777BB4?style=for-the-badge)
![RaspberryPi](https://img.shields.io/badge/Raspberry_Pi_Zero-W-C51A4A?style=for-the-badge)
![Licence](https://img.shields.io/badge/Licence-MIT-green?style=for-the-badge)

Scripts permettant de basculer facilement le Raspberry Pi Zero entre le mode **RNDIS** (USB gadget réseau, utilisé avec BYOPM) et le mode **classique** (dhcpcd, réseau Wi-Fi/Ethernet standard). Le script détecte automatiquement le mode actuel et effectue le basculement.

---

## Fonctionnalités

- Détection automatique du mode réseau actif (RNDIS vs classique)
- Basculement en un clic entre les deux modes
- Activation/désactivation des services systemd appropriés (`nm_gadget`, `dhcpcd`)
- Interface web PHP simple pour déclencher le basculement depuis un navigateur

---

## Contexte

Le Raspberry Pi Zero peut fonctionner dans deux modes réseau :

| Mode | Service actif | Utilisation |
|------|--------------|-------------|
| **RNDIS (Gadget)** | `nm_gadget.service` | Connexion USB directe (ex. BYOPM, KeePass) |
| **Classique** | `dhcpcd.service` | Wi-Fi ou Ethernet standard |

Ce script est conçu pour être utilisé conjointement avec le projet [BYOPM](https://github.com/Axolotty/BYOPM).

---

## Prérequis

- Raspberry Pi Zero W
- Raspberry Pi OS (Lite ou Desktop)
- Service `nm_gadget` configuré (voir BYOPM)
- PHP et nginx installés (pour l'interface web)
- Droits `sudo`

---

## Installation

```bash
git clone https://github.com/Axolotty/Switch_NDIS_basic.git
cd Switch_NDIS_basic
chmod +x rndis.sh
```

Placer `index.php` dans le répertoire web nginx et `rndis.sh` dans un emplacement accessible par le serveur web.

---

## Utilisation

### Depuis le terminal

```bash
sudo ./rndis.sh
```

Le script affiche le mode actuel et effectue le basculement :

```
Le RPI 0 est en mode RNDIS (en mode Keypass), passage en mode classique...
```

ou :

```
Le RPI 0 est en mode classique, passage en mode RNDIS (en mode Keypass)...
```

### Via l'interface web

Accéder à l'interface PHP depuis un navigateur connecté au Pi :

```
http://<adresse-du-pi>/
```

Le bouton déclenche `rndis.sh` via PHP.

---

## Fichiers du projet

| Fichier | Description |
|---------|-------------|
| `rndis.sh` | Script Bash de basculement réseau |
| `index.php` | Interface web PHP pour déclencher le basculement |

---

## Licence

MIT © Axolotty

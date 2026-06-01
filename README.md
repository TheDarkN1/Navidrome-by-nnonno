# Navidrome-by-nnonno
I created a Navidrome server for song streaming


# 🎵 Mon Serveur Navidrome

<p align="center">
  <img src="[https://www.navidrome.org/logo.png](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%2Fid%2FOIP.aQQe8PAGNA_UA7wzvX9gAQHaHa%3Fpid%3DApi&f=1&ipt=2cfde06bc2190d3f5cb39828580b0d995098d1224426c6aaa6d8769bc7bc5377&ipo=images)" width="120" alt="Navidrome Logo">
</p>

<p align="center">
  <strong>Serveur de streaming musical auto-hébergé basé sur Navidrome</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Navidrome-Latest-green" alt="Navidrome">
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Proxmox-Virtualisation-orange" alt="Proxmox">
</p>

---

## 📋 Présentation

Ce projet permet d'héberger une bibliothèque musicale personnelle accessible depuis n'importe quel appareil.

Fonctionnalités :

* Streaming audio via Navidrome
* Gestion des playlists
* Compatible Subsonic
* Applications mobiles Android et iOS
* Interface web moderne en passant par Feishin
* Accès distant sécurisé via reverse proxy (Pangolin)

---

## 📸 Captures d'écran

Ajoutez ici vos captures d'écran :

![Accueil](screenshots/home.png)

---

## 🚀 Quick Start

### Installation de docker 

Mettre à jour les paquets et installer les dépendances nécessaires 

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
```
Créer le dossier des clés

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

Télécharger la clé GPG

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
Autoriser la lecture de la clé

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
Ajouter le dépôt officiel Docker

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/debian \
$(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Recharger les dépôts

```bash
sudo apt update
```
Installer Docker

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Activer Docker au démarrage

```bash
sudo systemctl enable docker
```
Démarrer Docker immédiatement

```bash
sudo systemctl enable docker
```

Vérifier l'installation

```bash
docker --version
docker compose version
```

### Préparation de l'environnement

Création du dossier de données
le dossier qui contiendra la configuration et la base de données de Navidrome :

```bash
mkdir -p /srv/navidrome
```

Identification du disque

```bash
lsblk
```
Montage du disque

```bash
mount /dev/sdb1 /mnt/music
```
Montage automatique au démarrage

Récupérer l'UUID du disque :

```bash
blkid
```

Ajouter l'entrée correspondante dans le fichier /etc/fstab :

```bash
nano /etc/fstab
```

UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt/music ext4 defaults 0 2

Tester la configuration :

```bash
mount -a
```


### Docker Compose

Créer un fichier `docker-compose.yml`

dans 

```bash
cd /srv/navidrome
```

```yaml

services:
  navidrome:
    image: deluan/navidrome:latest
    container_name: navidrome
    restart: unless-stopped

    ports:
      - "4533:4533"

    environment:
      ND_SCANSCHEDULE: 1h
      ND_WATCHFOLDER: "true"

    volumes:
      - /srv/navidrome/data:/data
      - /mnt/music:/music:ro

```

### Lancement

```bash
docker compose up -d
```

### Accès

```text
http://IP_DU_SERVEUR:4533
```

---

## ⚙️ Infrastructure

| Service   | Description            |
| --------- | ---------------------- |
| Proxmox   | Hyperviseur            |
| Debian 13 | Système d'exploitation |
| Docker    | Conteneurisation       |
| Navidrome | Serveur musical        |
| Pangolin  | Accès distant sécurisé |
| Feishin   | Player interface web   |


---

## 📂 Structure des dossiers

```text
/srv/navidrome/
├── docker-compose.yml
├── data/
/mnt/music
├── music/
```

---

## 🔒 Sécurité

* Reverse Proxy
* HTTPS
* Authentification Navidrome
* Accès distant sécurisé

---

## 🛠️ Maintenance

Mettre à jour le conteneur :

```bash
docker compose pull
docker compose up -d
```

Consulter les logs :

```bash
docker logs -f navidrome
```

---

## 📄 Licence

Projet personnel réalisé dans le cadre de l'auto-hébergement et de l'apprentissage de l'administration système.

Mon instagram au cas ou.

<a href="https://www.instagram.com/nnonno_917/" target="_blank" rel="noopener noreferrer">
    <img src="https://cdn.jsdelivr.net/npm/simple-icons@v11/icons/instagram.svg"
         alt="Instagram"
         width="32"
         height="32">
</a>

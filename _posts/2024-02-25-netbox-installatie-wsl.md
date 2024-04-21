---
title: Installatie van NetBox met Docker en Docker Compose op WSL
date: 2024-02-25 10:15:56 -300
categories: [WSL, Netbox]
tags: [netbox, docker-compose]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-netboxinstall.webp
---
# Aan de slag.

## Instrcuties.

### 1. **Kloon de NetBox Docker-repository**:
   Ga naar je `/path/to-your/projects_volume/netbox` directory in de terminal en voer het volgende commando uit:
   ```
   git clone -b release https://github.com/netbox-community/netbox-docker.git .
   ```

### 2. **Maak een docker-compose.override.yml bestand**:
   Maak binnen de `/path/to-your/projects_volume/netbox` directory een bestand met de naam `docker-compose.override.yml` aan met de volgende inhoud:
   ```yaml
   version: '3.4'
   services:
     netbox:
       ports:
         - 8000:8080
   ```

### 3. **Trek de Docker-images**:
   Voer het volgende commando uit in dezelfde directory om de benodigde Docker-images op te halen:
   ```
   docker-compose pull
   ```

### 4. **Start de Docker-containers**:
   Start de Docker-containers met het volgende commando:
   ```
   docker-compose up -d
   ```

### 5. **Toegang tot NetBox**:
   Zodra de containers actief zijn, open je webbrowser en ga je naar `http://wsl.localhost:8000`. Je zou de NetBox-startpagina moeten zien.

### 6. **Maak de eerste beheerdersgebruiker aan**:
   Voer het volgende commando uit om de eerste beheerdersgebruiker aan te maken:
   ```
   docker-compose exec netbox /opt/netbox/netbox/manage.py createsuperuser
   ```
   Volg de instructies om het beheerdersgebruikersaccount in te stellen.

Vervang `8000` door een ander poortnummer als het al in gebruik is op je systeem.
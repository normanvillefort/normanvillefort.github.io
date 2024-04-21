---
title: Installatie van Zabbix Server met Docker en Docker Compose op WSL
date: 2024-02-23 10:15:56 -300
categories: [WSL, Zabbix]
tags: [zabbix, docker-compose]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-zabbixinstall.webp
---
# Aan de slag.

## Instructies.

### 1. **Kloon de Zabbix Docker repository**:
   Om te beginnen, kloon de Zabbix Docker repository naar jouw `/path/to-your/projects_volume/zabbix` directory. Voer hiervoor het volgende commando uit in je terminal:
   ```
   git clone -b 6.4 https://github.com/zabbix/zabbix-docker.git /path/to-your/projects_volume/zabbix
   ```
   Met dit commando kloon je de Zabbix Docker repository naar de opgegeven directory.

### 2. **Maak een docker-compose.override.yml bestand**:
   Navigeer naar de `/path/to-your/projects_volume/zabbix` directory en maak daar een `docker-compose.override.yml` bestand aan met de volgende inhoud:
   ```
   version: '3.4'
   services:
     zabbix-server:
       ports:
         - 10051:10051
   ```
   Deze configuratie zorgt ervoor dat poort 10051 op je lokale machine verbonden wordt met poort 10051 van de Docker container.

### 3. **Haal de Docker images op**:
   Ga terug naar de `/path/to-your/projects_volume/zabbix` directory en voer het volgende commando uit om de benodigde Docker images op te halen:
   ```
   docker-compose pull
   ```
   Dit commando haalt alle benodigde onderdelen op die Zabbix nodig heeft om als container op je machine te draaien.

### 4. **Start de Docker containers**:
   Zodra alles is opgehaald, start je de containers op met het volgende commando:
   ```
   docker-compose up
   ```
   Bekijk hoe je Zabbix setup tot leven komt. Na een paar momenten is alles gereed voor gebruik.

### 5. **Toegang tot Zabbix**:
   Om van je kersverse Zabbix setup te genieten, open je een webbrowser en ga je naar `http://wsl.localhost:80`. Daar vind je de Zabbix homepage.

Je kunt de poortnummers aanpassen als `80` al in gebruik is op je systeem. Zorg ervoor dat Docker en Docker Compose correct zijn geïnstalleerd en draaien op je systeem voordat je deze commando's uitvoert.
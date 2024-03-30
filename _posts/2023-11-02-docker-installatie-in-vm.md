---
title: Docker Installatie in Ubuntu VM
date: 2023-11-02 21:11:06 -300
categories: [Virtualisatie, Containerisatie]
tags: [docker, ubuntu, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-dockerubuntuvminstall.webp
---

# Aan de slag

## Instructies

Hier zijn de stappen om Ubuntu Server met Docker te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Download de ISO-image van Ubuntu Server:**
- Ga naar de officiële website van [Ubuntu](https://ubuntu.com/download/server) en download de ISO-image van Ubuntu Server.

### **Stap 2: Upload de ISO naar de Proxmox-server:**
- Log in op de Proxmox webinterface.
- Ga naar de "Storage" sectie en selecteer de opslaglocatie waar je de ISO wilt uploaden.
- Klik op "Upload" en selecteer de gedownloade ISO-image van Ubuntu Server.

### **Stap 3: Maak een nieuwe virtuele machine aan in Proxmox:**
- Ga naar de "Create VM" sectie in de Proxmox webinterface.
- Volg de stappen om een nieuwe virtuele machine te maken:
  - Geef de VM een naam, bijvoorbeeld "ubuntu-server-docker".
  - Kies "Linux" als het besturingssysteem.
  - Kies de juiste versie van Ubuntu Server.
  - Stel de gewenste resources (CPU, geheugen, opslag) in voor de VM.
  - Klik op "Next".

### **Stap 4: Installeer het besturingssysteem op de virtuele machine:**
- Selecteer de net aangemaakte virtuele machine in de Proxmox-interface en klik op "Console" om de console te openen.
- Start de virtuele machine op.
- Volg de instructies om Ubuntu Server te installeren:
  - Selecteer de gewenste taal en kies "Install Ubuntu Server".
  - Volg de installatiewizard om de taal, toetsenbordindeling en netwerkinstellingen te configureren.
  - Kies "Guided - use entire disk" voor het partitie-indelingsschema en selecteer de juiste virtuele harde schijf.
  - Bevestig de partitiewijzigingen en ga verder met de installatie.
  - Configureer gebruikersnaam, wachtwoord en andere instellingen volgens je voorkeuren.
  - Wacht tot de installatie is voltooid en herstart de virtuele machine.

### **Stap 5: Installeer Docker op Ubuntu Server:**
- Na de installatie log je in op de virtuele machine met de gegeven inloggegevens.
- Voer de volgende commando's uit om Docker te installeren:
  ```
  sudo apt update
  sudo apt install -y docker.io
  ```
- Voeg je gebruiker toe aan de Docker-groep om Docker zonder sudo te kunnen gebruiken:
  ```
  sudo usermod -aG docker $USER
  ```

### **Stap 6: Controleer of Docker correct is geïnstalleerd:**
- Voer het volgende commando uit om de Docker-versie te controleren:
  ```
  docker --version
  ```

Nu zou Ubuntu Server met Docker succesvol geïnstalleerd moeten zijn op de virtuele machine in je Proxmox-omgeving. Je kunt nu Docker-containers uitvoeren en beheren op Ubuntu Server. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke vereisten en om de veiligheid van de installatie te waarborgen.
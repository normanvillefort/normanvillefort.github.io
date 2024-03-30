---
title: MeshCentral Installatie
date: 2023-01-27 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [meshcentral, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-meshcentralinstall.webp
---

# Aan de slag

## Instructies 

Hier zijn de stappen om MeshCentral te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "meshcentral".
- Kies het gewenste besturingssysteem (bijvoorbeeld Ubuntu Server) en de versie.
- Stel de gewenste resources (CPU, geheugen, opslag) in voor de VM.
- Klik op "Create" om de VM aan te maken.

### **Stap 2: Installeer het besturingssysteem op de virtuele machine:**
- Start de virtuele machine op en open de console.
- Volg de instructies om het besturingssysteem te installeren (bijvoorbeeld Ubuntu Server).
- Zorg ervoor dat je tijdens de installatie een statisch IP-adres instelt dat overeenkomt met het netwerk van je Proxmox-server (bijvoorbeeld 192.168.0.X).

### **Stap 3: Log in op de virtuele machine en update het systeem:**
- Nadat het besturingssysteem is geïnstalleerd, log je in op de virtuele machine met de gegeven inloggegevens.
- Voer de volgende commando's uit om het systeem bij te werken:
  ```
  sudo apt update
  sudo apt upgrade
  ```

### **Stap 4: Installeer Node.js en npm:**
- Voer de volgende commando's uit om Node.js en npm te installeren:
  ```
  sudo apt install -y nodejs npm
  ```

### **Stap 5: Download en installeer MeshCentral:**
- Maak een map aan voor MeshCentral en navigeer er naartoe:
  ```
  mkdir ~/meshcentral
  cd ~/meshcentral
  ```
- Download het MeshCentral-installatiebestand:
  ```
  wget https://github.com/Ylianst/MeshCentral/releases/download/v0.6.11/MeshCentral-linux-arm64.tar.gz
  ```
  (Opmerking: vervang de URL indien nodig door de juiste URL voor de gewenste versie en architectuur van MeshCentral.)
- Pak het gedownloade bestand uit:
  ```
  tar -xzvf MeshCentral-linux-arm64.tar.gz
  ```

### **Stap 6: Start MeshCentral:**
- Ga naar de MeshCentral-map:
  ```
  cd MeshCentral
  ```
- Start MeshCentral:
  ```
  sudo node meshcentral
  ```

MeshCentral zou nu moeten worden uitgevoerd op de opgegeven IP-adres en poort (standaardpoort is 443). Je kunt het openen via een webbrowser door naar het IP-adres van de virtuele machine te navigeren. Vervolgens kun je MeshCentral configureren en gebruiken voor het beheren van apparaten op afstand. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke behoeften en om de veiligheid van de installatie te waarborgen.
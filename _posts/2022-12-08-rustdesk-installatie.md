---
title: RustDesk Installatie
date: 2022-12-08 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [rustdesk, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-rustdeskinstall.webp
---

# Aan de slag

## Instructies 

Hier zijn de stappen om RustDesk te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "rustdesk".
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

### **Stap 4: Installeer RustDesk:**
- Download de nieuwste versie van RustDesk van de officiële website of GitHub.
- Ga naar de directory waar je RustDesk wilt installeren.
- Pak het gedownloade bestand uit:
  ```
  tar -xzvf rustdesk-linux-x86_64.tar.gz
  ```
  (Pas de bestandsnaam aan aan de versie die je hebt gedownload.)

### **Stap 5: Start RustDesk:**
- Navigeer naar de map waar RustDesk is uitgepakt.
- Start RustDesk met het volgende commando:
  ```
  ./RustDesk
  ```

RustDesk zou nu moeten draaien op de opgegeven IP-adres en poort. Je kunt het openen via een webbrowser door naar het IP-adres van de virtuele machine te navigeren, gevolgd door de poort waarop RustDesk draait (standaardpoort is 8080). Volg de instructies op het scherm om de installatie te voltooien en RustDesk te configureren. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke behoeften en om de veiligheid van de installatie te waarborgen.
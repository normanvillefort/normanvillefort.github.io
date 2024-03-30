---
title: Windows Server 2019 VM Installatie
date: 2022-03-23 11:13:56 -300
categories: [Zelfhosten, Installatie]
tags: [windowsserver, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-windowsservervminstall.webp
---

# Aan de slag

## Instructies

Hier zijn de stappen om Windows Server 2019 te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Download de ISO-image van Windows Server 2019:**
- Ga naar de officiële website van Microsoft of gebruik een vertrouwde bron om de ISO-image van Windows Server 2019 te downloaden.

### **Stap 2: Upload de ISO naar de Proxmox-server:**
- Log in op de Proxmox webinterface.
- Ga naar de "Storage" sectie en selecteer de opslaglocatie waar je de ISO wilt uploaden.
- Klik op "Upload" en selecteer de gedownloade ISO-image van Windows Server 2019.

### **Stap 3: Maak een nieuwe virtuele machine aan in Proxmox:**
- Ga naar de "Create VM" sectie in de Proxmox webinterface.
- Volg de stappen om een nieuwe virtuele machine te maken:
  - Geef de VM een naam, bijvoorbeeld "windows-server".
  - Kies "Microsoft Windows" als het besturingssysteem.
  - Kies de juiste versie van Windows Server 2019.
  - Stel de gewenste resources (CPU, geheugen, opslag) in voor de VM.
  - Klik op "Next".

### **Stap 4: Installeer het besturingssysteem op de virtuele machine:**
- Selecteer de net aangemaakte virtuele machine in de Proxmox-interface en klik op "Console" om de console te openen.
- Start de virtuele machine op.
- Volg de instructies om Windows Server 2019 te installeren:
  - Selecteer de taal, tijdzone en toetsenbordindeling.
  - Klik op "Install Now".
  - Voer de productsleutel in (indien van toepassing).
  - Accepteer de licentievoorwaarden en klik op "Next".
  - Kies de installatietype (bijvoorbeeld "Custom: Install Windows only").
  - Selecteer de juiste virtuele harde schijf en klik op "Next" om de installatie te starten.
  - Volg de verdere instructies om de installatie te voltooien.

### **Stap 5: Configureer Windows Server 2019:**
- Na de installatie volg je de stappen om Windows Server 2019 te configureren, zoals het instellen van een wachtwoord voor de Administrator-account, het instellen van netwerkinstellingen en het voltooien van de installatiewizard.

Nu zou Windows Server 2019 succesvol geïnstalleerd moeten zijn op de virtuele machine in je Proxmox-omgeving. Je kunt nu verdergaan met het configureren van Windows Server voor je specifieke behoeften, zoals het installeren van rollen en functies, het configureren van netwerkinstellingen en het beheren van gebruikers en groepen. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke vereisten en om de veiligheid van de installatie te waarborgen.
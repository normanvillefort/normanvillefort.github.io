---
title: Ubuntu Server Installatie op Fysieke Server
date: 2023-05-05 10:15:56 -300
categories: [Ubuntu Server, Installatie]
tags: [ubuntuserver, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-ubuntuserverinstall.webp
---

# Aan de slag

## Instructies

Hier zijn de stappen om Ubuntu Server te installeren op een HP ProLiant-fysieke server:

### **Stap 1: Download de ISO-image van Ubuntu Server:**
- Ga naar de officiële website van [Ubuntu](https://ubuntu.com/download/server) en download de ISO-image van Ubuntu Server. Zorg ervoor dat je de juiste architectuur kiest (bijvoorbeeld 64-bit) en de versie die je wilt installeren.

### **Stap 2: Maak een opstartbaar medium:**
- Brand de gedownloade ISO-image op een DVD of maak een opstartbare USB-stick met behulp van software zoals Rufus (voor Windows) of dd (voor Linux). Zorg ervoor dat het opstartbare medium klaar is voor gebruik.

### **Stap 3: Plaats het opstartbare medium in de HP ProLiant-server:**
- Plaats de opstartbare DVD of USB-stick in de desbetreffende sleuf of poort van de HP ProLiant-server.

### **Stap 4: Start de HP ProLiant-server op vanaf het opstartbare medium:**
- Start de HP ProLiant-server opnieuw op en ga naar het BIOS of de UEFI-instellingen.
- Stel de opstartvolgorde in zodat de server opstart vanaf het opstartbare medium (DVD of USB-stick).

### **Stap 5: Start de installatie van Ubuntu Server:**
- Zodra de server is opgestart vanaf het opstartbare medium, volg je de instructies op het scherm om Ubuntu Server te installeren.
- Kies de gewenste taal en selecteer "Install Ubuntu Server" in het opstartmenu.
- Doorloop de installatiewizard en configureer de taal, toetsenbordindeling, tijdzone en andere basisconfiguraties.

### **Stap 6: Partitie-indeling en installatie:**
- Kies de gewenste partitie-indeling. Voor de meeste standaardinstallaties kun je de optie "Guided - use entire disk" selecteren.
- Selecteer de juiste schijf waarop je Ubuntu Server wilt installeren.
- Bevestig de partitiewijzigingen en ga verder met de installatie.

### **Stap 7: Configuratie van gebruikers en instellingen:**
- Tijdens de installatie wordt je gevraagd om een gebruikersnaam, wachtwoord en hostnaam in te stellen.
- Volg de instructies op het scherm om de installatie te voltooien en wacht tot Ubuntu Server is geïnstalleerd.

### **Stap 8: Herstart de HP ProLiant-server:**
- Nadat de installatie is voltooid, herstart je de HP ProLiant-server en verwijder je het opstartbare medium (DVD of USB-stick).

Nu zou Ubuntu Server succesvol geïnstalleerd moeten zijn op de HP ProLiant-fysieke server. Je kunt nu verdergaan met het configureren van Ubuntu Server en het installeren van Docker volgens de eerder verstrekte instructies. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke vereisten en om de veiligheid van de server te waarborgen.
---
title: Proxmox Virtual Environment &#58 Installatie
date: 2022-02-07 14:33:56 -300
categories: [Virtualisatie, Server]
tags: [proxmox, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-proxinstall.webp
---

# Aan de slag

Proxmox Virtual Environment (Proxmox VE) biedt een complete open-source oplossing voor ondernemingsvirtualisatie. Hieronder vind je een stapsgewijze gids voor het installeren en instellen van Proxmox VE op een pc of server, samen met enkele aanbevelingen en pre-requisieten.

### Benodigheden:

- Een pc of server die voldoet aan de standaard aanbevolen hardwarevereisten.
- Een USB-stick van 8GB of groter voor het opstarten van het installatieproces.

## Voorbereidingen:

1. Download de Proxmox VE Installer van de officiële website [van Proxmox](https://proxmox.com/en/downloads).
2. Gebruik Rufus (voor Windows) of Etcher (voor Macs) om de opstartbare USB-drive te maken met de Proxmox VE Installer.

## Installatie:

1. Steek de opstartbare USB-drive in de pc of server waarop je Proxmox wilt installeren en start de pc op.
2. Volg de instructies op het scherm van de Proxmox installer.
3. Ga akkoord met de End User License Agreement (EULA) als je akkoord gaat.
4. Selecteer de harde schijf waarop je Proxmox wilt installeren.
5. Selecteer je land, tijdzone en toetsenbordindeling.
6. Stel het root wachtwoord en het e-mailadres in.
7. Configureer het netwerk voor het beheer: 
    * selecteer het netwerk management interface, 
    * voer in de hostname (FQDN), 
    * het gewenste IP-adres, 
    * het gewenste netmask, 
    * de gateway en 
    * de DNS-server.
8. Wacht tot de installatie is voltooid en je het bericht "Installatie succesvol" ziet.

## Volgende stappen:

1. Reboot de pc of server.
2. Open een webbrowser op een ander werkstation en ga naar het gekozen IP-adres op poort 8006.

Dit opent de Proxmox VE webinterface, waar je verder kunt gaan met het configureren en beheren van je virtuele omgeving.

> Zorg ervoor dat je [de officiële documentatie](https://pve.proxmox.com/pve-docs/chapter-sysadmin.html) van Proxmox VE raadpleegt voor eventuele updates.
{: .prompt-tip }
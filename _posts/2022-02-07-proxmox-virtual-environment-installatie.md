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


### Eerste login

Voordat we beginnen met het configureren van Proxmox, is het belangrijk om enkele best practices te bespreken met betrekking tot netwerkconfiguratie. Voor een efficiënte en veilige werking van je Proxmox-omgeving is het aan te raden om gebruik te maken van private IP-adressen binnen een betrouwbaar IP-bereik, zoals gedefinieerd in RFC 1918. Overweeg om de volgende IP-bereiken te gebruiken:

- WAN-interface: Je kunt een publiek IP-adres toewijzen dat is verstrekt door je internetprovider. Als je een privénetwerk gebruikt voor de WAN-interface, kies dan een IP-adres uit het publieke IP-bereik dat niet overlapt met IP-adressen die door andere netwerken worden gebruikt.
- LAN-interface: Voor het LAN-netwerk kun je een privé IP-range uit de volgende RFC 1918-adresruimtes gebruiken:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

Zorg ervoor dat je subnetmaskers toepast die geschikt zijn voor je netwerkvereisten en vermijd het gebruik van IP-adressen die mogelijk conflicteren met andere apparaten in je netwerk.

### Aanmaken van een storage pool

Bij het aanmaken van een storage pool voor je Proxmox-omgeving is het belangrijk om rekening te houden met de geplande implementaties van een firewall, en additionele Windows Servers en Linux Servers. Hier zijn enkele suggesties en best practices:

1. **Grootte van de storage pool:** Overweeg de totale opslagvereisten van je virtuele machines (firewall, Windows Server en Linux Server), inclusief besturingssysteem, toepassingen en gegevens. Houd ook rekening met toekomstige groei en reserveer voldoende ruimte om aan je behoeften te voldoen.
2. **Opslagtype:** Afhankelijk van je prestatie- en betrouwbaarheidseisen kun je verschillende opslagtypen overwegen, zoals ZFS, LVM of Ceph. ZFS biedt bijvoorbeeld geavanceerde functies zoals gegevensintegriteitscontrole en snapshots, terwijl LVM flexibiliteit biedt bij het beheren van volumes.
3. **RAID-configuratie:** Implementeer indien mogelijk een redundantie-oplossing zoals RAID om gegevensbescherming en fouttolerantie te garanderen.
4. **Schaalbaarheid:** Plan voor de toekomst en zorg ervoor dat je storage pool schaalbaar is om gemakkelijk capaciteit toe te voegen wanneer dat nodig is.

Door deze suggesties te volgen, kun je een robuuste en schaalbare storage pool creëren die voldoet aan de behoeften van je Proxmox-omgeving.

### Aanmaken van een VM (Windows Server)

Het creëren van een virtuele machine (VM) voor een Windows Server op Proxmox vereist zorgvuldige planning en configuratie. Hier zijn enkele best practices om te volgen bij het aanmaken van een Windows Server VM:

1. Navigeer naar het Proxmox-dashboard en klik op de knop "Create VM" bovenaan het scherm.

2. Voer in het pop-upvenster een naam in voor de virtuele machine (bijvoorbeeld "Windows Server") en selecteer de gewenste opties voor CPU, geheugen en opslag. Klik vervolgens op "Next".


3. Kies het gewenste besturingssysteem voor de virtuele machine. Selecteer in dit geval "Microsoft Windows" en de juiste versie (bijvoorbeeld "Windows Server 2019"). Klik op "Next" om door te gaan.


4. Stel de grootte van de harde schijf in voor de Windows Server-VM. Voer de gewenste grootte in GB in en klik op "Next".


5. Configureer de netwerkinstellingen voor de Windows Server-VM. Wijs de juiste netwerkinterface toe aan de VM en selecteer het gewenste netwerkmodel (bijvoorbeeld "bridge" voor een rechtstreekse verbinding met het LAN-netwerk). Klik op "Next" om door te gaan.


6. Controleer de samenvatting van de configuratie voor de Windows Server-VM en klik op "Finish" om het aanmaken van de VM te voltooien.


7. De Windows Server-VM wordt nu aangemaakt en verschijnt in de lijst met virtuele machines op het Proxmox-dashboard. Klik op de VM om de details te bekijken en start de VM vervolgens door op de knop "Start" te klikken.


8. Wacht tot de VM is opgestart en voltooi de Windows Server-installatie door de instructies op het scherm te volgen. Je kunt de ISO van Windows Server uploaden naar de Proxmox-server en deze toewijzen aan de VM als installatiemedia.

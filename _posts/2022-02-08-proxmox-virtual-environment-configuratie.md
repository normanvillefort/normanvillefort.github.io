---
title: Proxmox Virtual Environment &#58 Configuratie
date: 2022-02-08 10:15:56 -300
categories: [Virtualisatie, Server]
tags: [proxmox, configuratie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-proxconfig.webp
---

# Aan de slag

Na een nieuwe installatie van Proxmox VE, volg de onderstaande stappen om je virtuele omgeving in te stellen en te configureren via de webinterface.

## Toegang tot de Webinterface:

1. Na de reboot van de Proxmox server, open een webbrowser op een andere pc en ga naar het IP-adres van je Proxmox-server op poort `8006`.
2. Log in met de gebruikersnaam 'root' en het wachtwoord dat je hebt ingesteld tijdens het installatieproces.
3. Klik op "OK" om de "No valid subscription" popup te sluiten.

## Datacenter Overzicht:

1. In de webinterface zie je het Datacenter-scherm met een hierarchisch overzicht van alle nodes.
2. Bij de eerste installatie zie je slechts één node genaamd 'pve' in het linkerdeel van het scherm.
3. Als je de node 'pve' uitvouwt, krijg je de opslag te zien.
4. Met de 'datacenter' geselecteerd, heb je op het scherm toegang tot alles op het datacenter niveau, zoals de opties summary, cluster, ceph, options, storage, backup, replication, permission (waaronder je users, API-tokens, groups, pools, roles en authentication hebt), HA, ACME en firewall.
5. Met de node 'pve' geselecteerd, heb je op het scherm toegang tot alles op het node niveau, zoals de opties summary, notes, shell, system (waaronder je network, certificates, DNS, hosts, time, en de syslog te zien krijgt), updates, firewall, (waaronder je options en log hebt), disks (waaronder je LVM, LVM-thin, directory, en ZFS hebt), ceph, replication, task history en subscription.


## Eerste Stappen:

### Updates Inschakelen:

1. SSH naar je Proxmox-server.
    1. Ga naar de sources.list met de commando `nano ect/apt/sources.list` en pas het aan met de volgende stappen
        - voeg de code voor de non-production updates van Proxmox.  
            ```
            # security updates
            deb http://security.debian.org buster-updates main-contrib

            # not for production use
            deb http://download.proxmox.com/debian buster pve-no-subscription
            ```
    2. Ga naar de pve-enterprise.list met de commando `nano ect/apt/sources.list.d/pve-enterprise.list` en pas het aan met de volgende stappen
        - comment out de volgende code als je geen subscription heb. `# deb http://enterprise.proxmox.com/debian/pve buster pve-enterprise`. Dit doen we om foutmeldingen te voorkomen bij het updaten. 
    3. Update de list met de commando `apt-get update`
    4. Voer een distributie-upgrade uit met `apt dist-upgrade` 
    5. Reboot de Proxmox server
    
> Notitie: als je de upgrade niet wilt uitvoeren via SSH, kun je dat ook doen vanuit de GUI in de Datacenter onder 'Updates'.
{: .prompt-tip }

### Opslag Configureren:

1. Selecteer de node 'pve'.
    - Ga naar storage, waar alle harde schijven in een lijst staan
    - Creëer een nieuwe ZFS pool
        - ga naar ZFS
        - ga naar 'create ZFS'
            - geef je pool een naam
            - selecteer je RAID level
            - houd je 'compression' op 'on'
            - houd je 'ashift' op '12'
            - selecteer de gewenste harde schijf of alle harde schijven 
            - klik op 'create'
    - Ga na als 'smart monitoring' is aangeschakeld. Dit kun je ook checken in de terminal, gebruik deze commando `smartctl -a <DEVICENAME>`. Device name is de naam van de harde schijf.

### IOMMU Inschakelen:

> Opmerking: Alleen mogelijk als de processor en moederbord de IOMMU ondersteunen en als deze is ingeschakeld in de BIOS van het moederbord. **Manufacturers geven de PCI Pass Through (IOMMU) technologie vaak andere namen. Check welke naam jouw moederbord manufacturer gebruikt.**
{: .prompt-tip }

1. SSH naar de Proxmox-server.
    1. Ga naar de GRUB met de commando `nano ect/default/grub` en pas het aan met de volgende stappen
        - comment out de code `GRUB_CMDLINE_LINUX_DEFAULT="quiet"` door de # aan het begin toe te voegen 
        - voeg de code `GRUB_CMDLINE_LINUX_DEFAULT="quiet" intel_iommu=on` door de # aan het begin te verwijderen (Note: voor AMD Processor maak er `amd_iommu=on` ip plaats van `intel_iommu=on`)
        - sla de aanpassingen op
    2. Update de GRUB-configuratie met `update-grub`
    3. Ga naar de modules met de commando `nano /ect/modules` en pas het aan met de volgende stappen
        - voeg de volgende code toe 
            ```
            vfio
            vfio_iommu_type1
            vfio_pci
            vfio_virqfd
            ``` 
        - sla de aanpassingen op
    4. Reboot de Proxmox server met de commando `reboot`

### VLAN Aware Inschakelen:

1. Selecteer de node 'pve'.
2. Ga naar 'Netwerk' en selecteer de brug.
3. Vink 'VLAN Aware' aan en klik op 'OK'.

### NFS Shares Toevoegen:

1. Klik op 'Datacenter' 
    1. ga naar Storage
    2. ga naar 'add NFS'  
        - geef de NFS share een naam bijv. 'backups' 
        - voer de IP van de NAS server in 
        - selecteer de content type voor de NFS share (meervoudige selectie is mogelijk)
        - klik 'Create' 

### Backups Plannen:

1. Klik op datacenter
    1. Navigeer naar 'Backup'
    2. klik 'Add' om een backup job toe te voegen
        - selecteer de node
        - selecteer de storage
        - selecteer de dag van de week (meervoudige selectie is mogelijk)
        - kies de starttijd
        - voer in je e-mail adres
        - kies ZSTD (fast en good) voor de compression 
        - selecteer de gewenste virtuele machines
        - klik 'Create'
    
> Initieer zo snel als mogelijk de eerste backup van de VMs.
{: .prompt-warning }

### KVM Drivers Disk en ISOs Uploaden:

1. Upload de VirtIO drivers disk naar de opslag.
    - download de [latest stable VirtIO drivers](https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers)
    - upload ze naar storage (NFS share)
2. Upload Windows ISOs en Linux distros naar de opslag
    - download de meest recente Windows 10 en Windows 11 ISOs van Microsoft's website
    - download de meest stabliele Linux Ubuntu distro 
    - upload ze allemaal naar storage (NFS share)

### NIC Team voor Failover Maken:

> Dit is alleen mogelijk wanneer er 2 of meer netwerk interface kaarten zijn geinstalleerd in de Proxmox server.
{: .prompt-warning }

1. SSH naar de Proxmox-server.
    1. Navigeer naar de network interfaces met de commando `nano /ect/network/interfaces`
        -  ga na als je de netwerk interfaces ziet. Bijv. `iface eno1 inet manual` en `iface eno2 inet manual`
        -  ga na als je de bridge ziet met een static IP bijv. ..
            ```
            auto vmbr0
            iface vmbr0 inet static
                address <SERVER IP>
                gateway <SERVER GATEWAY>
                bridge-ports eno1
                bridge-stp off
            ```  
        -  comment out de bestaande code voor de bridge, als hier onder geïllustreerd, door de # aan het begin van elke regel te zetten
            ```
            #auto vmbr0
            #iface vmbr0 inet static
            #    address <SERVER IP/NETMASK>
            #    gateway <SERVER GATEWAY>
            #    bridge-ports eno1
            #    bridge-stp off
            #    bridge-fd 0 
            #    bridge-vlan-aware yes 
            #    bridge-vids 2-4094 
            ```  
        -  maak de NIC team met de volgende code entries
            ```
            iface bond0 inet manual
                bond-slaves eno1 eno2
                bond-miimon 100
                bond-mode 802.3ad
                bond-xmit-has-policy layer2+3
            ```  
        -  maak een nieuwe bridge aan met de volgende code entries
            ```
            auto vmbr0
            iface vmbr0 inet static
                address <SERVER IP/NETMASK>
                gateway <SERVER GATEWAY>
                bridge-ports bond0
                bridge-stp off
                bridge-fd 0 
                bridge-vlan-aware yes 
                bridge-vids 2-4094 
            ```  
            > Opmerking: alleen de waarde van `bridge-ports` is aangepast van `eno1` naar `bond0`.
            {: .prompt-tip }
        -  sla de aangebrachte aanpassingen op in de netwerk interfaces
    2.  Reboot de Proxmox server


### Virtuele Machine Template Maken:

1. Zorg ervoor dat de virtuele machine is uitgeschakeld.
    - rechtermuis klik op de VM
    - selecteer 'Convert to template'
    - klik op 'Yes' om de handeling te bevestigen

> Nadat de VM is converted naar een template, kun je het niet meer als een VM gebruiken.
{: .prompt-warning }

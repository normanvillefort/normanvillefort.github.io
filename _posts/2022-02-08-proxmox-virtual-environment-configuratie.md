---
title: Proxmox Virtual Environment &#58 Configuratie
date: 2022-02-08 10:15:56 -300
categories: [Virtualisatie, Server]
tags: [proxmox, configuratie]     # TAG names should always be lowercase
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
2. Bewerk het bestand `/etc/apt/sources.list` om de non-production updates van Proxmox toe te voegen.
3. Bewerk het bestand `/etc/apt/sources.list.d/pve-enterprise.list` en commentarieer de code uit om foutmeldingen te voorkomen.
4. Update de pakketlijst met `apt-get update`.
5. Voer een distributie-upgrade uit met `apt dist-upgrade`.
6. Herstart de Proxmox-server.

### Opslag Configureren:

1. Selecteer de node 'pve'.
2. Ga naar 'Opslag' en maak een nieuwe ZFS-pool.
3. Controleer of 'smart monitoring' is ingeschakeld voor de harde schijven.

### IOMMU Inschakelen:

1. SSH naar de Proxmox-server.
2. Bewerk het bestand `/etc/default/grub` om de IOMMU in te schakelen.
3. Voeg modules toe aan `/etc/modules`.
4. Update de GRUB-configuratie met `update-grub`.
5. Herstart de Proxmox-server.

### VLAN Bewustzijn Inschakelen:

1. Selecteer de node 'pve'.
2. Ga naar 'Netwerk' en selecteer de brug.
3. Vink 'VLAN Aware' aan en klik op 'OK'.

### NFS Shares Toevoegen:

1. Ga naar 'Datacenter' > 'Opslag'.
2. Klik op 'NFS toevoegen' en configureer de NFS share.

### Backups Plannen:

1. Klik op 'Datacenter'.
2. Ga naar 'Backup' en voeg een backup job toe voor virtuele machines.

### KVM Drivers Disk en ISOs Uploaden:

1. Upload de VirtIO drivers disk en ISOs naar de opslag.

### NIC Team voor Failover Maken:

1. SSH naar de Proxmox-server.
2. Bewerk de netwerkinterfaces en maak een NIC team voor failover.

### Virtuele Machine Template Maken:

1. Zorg ervoor dat de virtuele machine is uitgeschakeld.
2. Klik met de rechtermuisknop op de virtuele machine en selecteer 'Converteren naar template'.


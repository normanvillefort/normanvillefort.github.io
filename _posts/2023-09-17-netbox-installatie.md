---
title: Netbox Installatie
date: 2023-09-17 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [netbox, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-netboxinstall.webp
---

# Aan de slag

## Instructies 

Hier zijn de stappen om NetBox te installeren op een Proxmox virtuele omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "netbox".
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

### **Stap 4: Installeer de vereiste software en afhankelijkheden:**
- Voer de volgende commando's uit om de vereiste software en afhankelijkheden voor NetBox te installeren:
  ```
  sudo apt install -y python3 python3-pip python3-venv git libpq-dev python3-dev build-essential libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev node-less
  ```

### **Stap 5: Clone het NetBox GitHub-repository:**
- Clone het NetBox GitHub-repository naar de virtuele machine met het volgende commando:
  ```
  git clone -b master --depth 1 https://github.com/netbox-community/netbox.git /opt/netbox
  ```

### **Stap 6: Maak een Python virtual environment aan en installeer de benodigde packages:**
- Navigeer naar de NetBox-directory:
  ```
  cd /opt/netbox
  ```
- Maak een Python virtual environment aan en activeer deze:
  ```
  python3 -m venv venv
  source venv/bin/activate
  ```
- Installeer de benodigde Python packages:
  ```
  pip install -r requirements.txt
  ```

### **Stap 7: Configureer de NetBox-instellingen:**
- Kopieer het voorbeeldconfiguratiebestand en bewerk het:
  ```
  cp /opt/netbox/netbox/netbox/configuration.example.py /opt/netbox/netbox/netbox/configuration.py
  nano /opt/netbox/netbox/netbox/configuration.py
  ```
- Bewerk het configuratiebestand om de vereiste instellingen in te stellen, zoals databaseverbinding en geheime sleutel.

### **Stap 8: Initialiseer de database en verzamel statische bestanden:**
- Voer het initialisatiecommando uit om de database te maken en de statische bestanden te verzamelen:
  ```
  sudo /opt/netbox/venv/bin/python3 /opt/netbox/netbox/manage.py migrate
  sudo /opt/netbox/venv/bin/python3 /opt/netbox/netbox/manage.py collectstatic --no-input
  ```

### **Stap 9: Maak een supergebruiker aan:**
- Maak een supergebruiker aan voor de NetBox-beheerdersinterface:
  ```
  sudo /opt/netbox/venv/bin/python3 /opt/netbox/netbox/manage.py createsuperuser
  ```

### **Stap 10: Voer de NetBox development server uit:**
- Voer het volgende commando uit om de NetBox development server te starten:
  ```
  sudo /opt/netbox/venv/bin/python3 /opt/netbox/netbox/manage.py runserver 0.0.0.0:8000
  ```

Nu zou NetBox moeten draaien op de virtuele machine. Je kunt het openen via een webbrowser op het opgegeven IP-adres en poort (bijvoorbeeld http://192.168.0.X:8000/) en inloggen met de eerder aangemaakte supergebruiker. Vergeet niet om in een productieomgeving een reverse proxy en een WSGI-server te configureren voor NetBox.
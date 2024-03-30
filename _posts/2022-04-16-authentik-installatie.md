---
title: Authentik Installatie
date: 2022-04-16 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [authentik, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-authentikinstall.webp
---

# Aan de slag

## Instructies

Hier zijn de instructies om Authentik te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "authentik".
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

### **Stap 4: Installeer Docker en Docker Compose:**
- Voer de volgende commando's uit om Docker en Docker Compose te installeren:
  ```
  sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  sudo apt update
  sudo apt-get install -y docker-ce docker-ce-cli containerd.io
  sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  ```

### **Stap 5: Clone de Authentik GitHub-repository:**
- Clone het Authentik GitHub-repository naar de virtuele machine met het volgende commando:
  ```
  git clone https://github.com/goauthentik/authentik.git
  ```

### **Stap 6: Configureer Authentik:**
- Navigeer naar de gekloonde Authentik-map:
  ```
  cd authentik
  ```
- Kopieer het voorbeeldconfiguratiebestand en hernoem het naar `config.yaml`:
  ```
  cp config.yaml.example config.yaml
  ```
- Open het `config.yaml` bestand en configureer de gewenste instellingen, zoals domeinnaam en databaseverbinding.

### **Stap 7: Start Authentik:**
- Gebruik Docker Compose om Authentik te starten:
  ```
  sudo docker-compose up -d
  ```

Nu zou Authentik moeten draaien op het opgegeven IP-adres en poort. Je kunt het openen via een webbrowser door naar het IP-adres van de virtuele machine te navigeren. Volg de instructies op het scherm om de installatie van Authentik te voltooien en begin met het gebruik van de identity provider. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke behoeften en om de veiligheid van de installatie te waarborgen.
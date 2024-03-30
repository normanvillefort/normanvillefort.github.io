---
title: UV Desk Installatie
date: 2023-02-03 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [uvdesk, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-uvdeskinstall.webp
---

# Aan de slag

## Instructies 

Hier zijn de stappen om UV Desk te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "uvdesk".
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

### **Stap 4: Installeer Apache, MySQL en PHP:**
- Voer de volgende commando's uit om Apache, MySQL en PHP te installeren:
  ```
  sudo apt install -y apache2 mysql-server php libapache2-mod-php php-mysql php-imap php-intl php-xml php-gd php-curl php-zip unzip
  ```

### **Stap 5: Creëer een database en gebruiker voor UV Desk:**
- Log in op de MySQL-server:
  ```
  sudo mysql -u root -p
  ```
- Maak een nieuwe database en gebruiker aan:
  ```
  CREATE DATABASE uvdesk_db;
  CREATE USER 'uvdesk_user'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON uvdesk_db.* TO 'uvdesk_user'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```

### **Stap 6: Download en installeer UV Desk:**
- Maak een map aan voor UV Desk en navigeer er naartoe:
  ```
  sudo mkdir -p /var/www/html/uvdesk
  cd /var/www/html/uvdesk
  ```
- Download UV Desk van GitHub:
  ```
  sudo wget https://github.com/uvdesk/community/releases/download/v1.0.16/uvdesk-community-v1.0.16.tar.gz
  ```
- Pak het gedownloade bestand uit:
  ```
  sudo tar -xvzf uvdesk-community-v1.0.16.tar.gz
  ```

### **Stap 7: Configureer Apache voor UV Desk:**
- Maak een nieuwe Apache-configuratiebestand aan voor UV Desk:
  ```
  sudo nano /etc/apache2/sites-available/uvdesk.conf
  ```
- Voeg de volgende configuratie toe aan het bestand:
  ```
  <VirtualHost *:80>
      ServerAdmin admin@example.com
      DocumentRoot /var/www/html/uvdesk/public
      ServerName your_domain.com

      <Directory /var/www/html/uvdesk/>
          Options FollowSymLinks
          AllowOverride All
          Require all granted
      </Directory>

      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>
  ```
- Sla het bestand op en sluit het.

### **Stap 8: Activeer de Apache-configuratie en herstart Apache:**
  ```
  sudo a2ensite uvdesk.conf
  sudo systemctl restart apache2
  ```

### **Stap 9: Voltooi de installatie via de webinterface:**
- Open een webbrowser en ga naar het IP-adres van de virtuele machine (bijvoorbeeld http://192.168.0.X).
- Volg de instructies op het scherm om de installatie van UV Desk te voltooien.
- Configureer de databaseverbinding met de eerder aangemaakte database (uvdesk_db) en gebruiker (uvdesk_user).
- Voltooi de installatie en log in op UV Desk met de aangemaakte beheerdersaccount.

Nu zou UV Desk succesvol geïnstalleerd moeten zijn op de virtuele machine. Je kunt inloggen op de UV Desk webinterface en beginnen met het configureren van het ticketings- en supportsysteem. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke behoeften en om de veiligheid van de installatie te waarborgen.
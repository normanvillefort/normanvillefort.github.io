---
title: Invoice Ninja Installatie
date: 2023-07-18 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [invoice ninja, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-invoiceninjainstall.webp
---

# Aan de slag

## Instructies

Hier zijn de stappen om Invoice Ninja te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "invoiceninja".
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
  sudo apt install -y apache2 mysql-server php libapache2-mod-php php-mysql php-curl php-json php-mbstring php-gd php-xml php-zip
  ```

### **Stap 5: Maak een database en gebruiker voor Invoice Ninja:**
- Log in op de MySQL-server:
  ```
  sudo mysql -u root -p
  ```
- Maak een nieuwe database en gebruiker aan:
  ```
  CREATE DATABASE invoiceninja_db;
  CREATE USER 'invoiceninja_user'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON invoiceninja_db.* TO 'invoiceninja_user'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```

### **Stap 6: Download en installeer Invoice Ninja:**
- Download de nieuwste versie van Invoice Ninja van de officiële website of GitHub.
- Ga naar de directory waar je Invoice Ninja wilt installeren.
- Download en pak het installer.zip-bestand uit:
  ```
  wget https://download.invoiceninja.com/installer -O installer.zip
  unzip installer.zip
  ```
  
### **Stap 7: Voer de installatiewizard uit:**
- Ga naar de installer directory:
  ```
  cd installer
  ```
- Voer de installatiewizard uit:
  ```
  php ninja.php install
  ```
- Volg de instructies op het scherm om de installatie te voltooien en de instellingen voor de databaseverbinding in te stellen.

### **Stap 8: Configureer Apache voor Invoice Ninja:**
- Creëer een nieuw Apache-configuratiebestand voor Invoice Ninja:
  ```
  sudo nano /etc/apache2/sites-available/invoiceninja.conf
  ```
- Voeg de volgende configuratie toe aan het bestand:
  ```
  <VirtualHost *:80>
      ServerName your_domain.com
      DocumentRoot /var/www/html/invoiceninja/public

      <Directory /var/www/html/invoiceninja>
          AllowOverride All
      </Directory>
      
      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>
  ```
  (Vervang "your_domain.com" door het daadwerkelijke domein of IP-adres van de virtuele machine.)

### **Stap 9: Activeer de Apache-configuratie en herstart Apache:**
  ```
  sudo a2ensite invoiceninja.conf
  sudo systemctl restart apache2
  ```

Invoice Ninja zou nu moeten draaien op de opgegeven IP-adres en poort. Je kunt het openen via een webbrowser door naar het IP-adres van de virtuele machine te navigeren. Volg de instructies op het scherm om de configuratie van Invoice Ninja te voltooien en begin met het gebruik van de factureringssoftware. Vergeet niet om eventuele aanvullende configuraties uit te voeren op basis van je specifieke behoeften en om de veiligheid van de installatie te waarborgen.
---
title: Zabbix Installatie
date: 2023-02-06 10:15:56 -300
categories: [Zelfhosten, Installatie]
tags: [zabbix, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-zabbixinstall.webp
---

# Aan de slag

## Instructies 

Hier zijn de stappen om Zabbix te installeren op een virtuele machine in een Proxmox-omgeving:

### **Stap 1: Maak een nieuwe virtuele machine aan in Proxmox:**
- Log in op de Proxmox webinterface.
- Klik op "Create VM" en volg de stappen om een nieuwe virtuele machine te maken.
- Geef de VM een geschikte naam, zoals "zabbix".
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

### **Stap 4: Installeer Zabbix server en frontend pakketten:**
- Voer de volgende commando's uit om Zabbix server en frontend te installeren:
  ```
  sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
  ```

### **Stap 5: Configureer de database voor Zabbix:**
- Maak een nieuwe database aan voor Zabbix en een gebruiker met de juiste machtigingen. Vervang 'zabbix_db', 'zabbix_user' en 'password' door de gewenste database-, gebruikersnaam- en wachtwoordwaarden:
  ```
  sudo mysql -u root -p
  CREATE DATABASE zabbix_db character set utf8 collate utf8_bin;
  CREATE USER 'zabbix_user'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON zabbix_db.* TO 'zabbix_user'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  quit;
  ```
  
### **Stap 6: Importeer Zabbix database schema:**
- Importeer het Zabbix database schema in de eerder aangemaakte database:
  ```
  sudo zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | sudo mysql -u zabbix_user -p zabbix_db
  ```

### **Stap 7: Configureer Zabbix server:**
- Bewerk het Zabbix server configuratiebestand:
  ```
  sudo nano /etc/zabbix/zabbix_server.conf
  ```
- Stel de databaseverbinding in:
  ```
  DBHost=localhost
  DBName=zabbix_db
  DBUser=zabbix_user
  DBPassword=password
  ```

### **Stap 8: Start Zabbix server en agent:**
- Start de Zabbix server en agent services:
  ```
  sudo systemctl restart zabbix-server zabbix-agent apache2
  sudo systemctl enable zabbix-server zabbix-agent apache2
  ```

### **Stap 9: Configureer Zabbix frontend:**
- Open een webbrowser en ga naar het IP-adres van de Zabbix-server (bijvoorbeeld http://192.168.0.X/zabbix).
- Volg de installatiewizard om de Zabbix frontend te configureren:
  - Klik op "Next step".
  - Controleer of alle vereisten zijn vervuld.
  - Voer de gegevens in voor de eerder geconfigureerde database.
  - Klik op "Next step" en voltooi de installatiewizard.

Nu zou Zabbix succesvol geïnstalleerd moeten zijn op de virtuele machine. Je kunt inloggen op de Zabbix frontend met de standaard gebruikersnaam "Admin" en wachtwoord "zabbix". Vergeet niet om het wachtwoord na de eerste login te wijzigen.
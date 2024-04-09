---
title: Pretix installatie op AWS
date: 2023-12-18 06:11:06 -300
categories: [Opensource, Zelfhosten]
tags: [aws, pretix, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-pretixawsinstall.webp
---

Pretix is een open-source ticketverkoopsoftware die organisatoren van evenementen helpt bij het beheren van ticketverkoop, registratie en deelnemersbeheer voor diverse soorten evenementen, zoals conferenties, festivals, concerten, workshops en meer. Het biedt een uitgebreid platform waarmee organisatoren een naadloze en efficiënte ervaring kunnen bieden aan zowel deelnemers als organisatoren.

### Kenmerken van Pretix:
1. **Ticketverkoop:** Pretix stelt organisatoren in staat om aangepaste tickettypen, prijzen, kortingen en promotiecodes te maken en te beheren.
2. **Registratie:** Deelnemers kunnen zich eenvoudig registreren voor evenementen via een gebruiksvriendelijke online registratie-interface.
3. **Betalingen:** Pretix ondersteunt diverse betalingsgateways voor veilige en naadloze betalingstransacties, waaronder PayPal, Stripe, creditcards en meer.
4. **Deelnemersbeheer:** Organisatoren kunnen deelnemersgegevens beheren, bijhouden en analyseren, inclusief aanwezigheidsstatus, ticketinformatie en communicatie met deelnemers.
5. **Aanpasbaarheid:** Pretix biedt een reeks aanpasbare opties en thema's, zodat organisatoren de look en feel van hun ticketverkooppagina's kunnen aanpassen aan hun merkidentiteit.

### Use Case:
Stel je voor dat je een conferentie organiseert met meerdere tracks, workshops en lezingen. Met Pretix kun je eenvoudig verschillende soorten tickets maken, zoals dagpassen, workshop-tickets en VIP-tickets. Deelnemers kunnen zich registreren voor het evenement, tickets kopen en hun schema aanpassen door zich in te schrijven voor specifieke sessies en workshops. Organisatoren kunnen de ticketverkoop en registratie in realtime volgen, betalingsgegevens beheren en deelnemersinformatie analyseren om betere beslissingen te nemen voor toekomstige evenementen. Met Pretix kunnen zowel organisatoren als deelnemers genieten van een soepele en georganiseerde evenementervaring.

# Aan de slag

Ja! Als je het nog niet wist, je kunt AWS (Amazon Web Services) gebruiken om Pretix zelf te hosten. AWS biedt een breed scala aan cloudservices en infrastructuurproducten die geschikt zijn voor het hosten van verschillende soorten applicaties, waaronder webapplicaties zoals Pretix. Hier zijn de stappen die je zou kunnen volgen om Pretix op AWS te hosten:

## Deel 1: Voorbereiding op AWS

### Stap 1: Maak een AWS-account aan:

1. Ga naar de AWS-website [https://aws.amazon.com/](https://aws.amazon.com/) en klik op "Create an AWS Account".
2. Volg de instructies om je account aan te maken en in te loggen op de AWS Management Console.

### Stap 2: Start een nieuwe EC2-instance:

1. Navigeer naar de EC2-service in de AWS Management Console.
2. Klik op "Launch Instance" om een nieuwe EC2-instance te starten.
3. Selecteer een Amazon Machine Image (AMI) voor je EC2-instance. Je kunt bijvoorbeeld kiezen voor een Ubuntu Server AMI.
4. Kies een instantietype, zoals t2.micro, afhankelijk van je vereisten en budget.
5. Configureer de details van de instantie, zoals het aantal instanties, subnet en beveiligingsgroepen.
6. Maak een nieuwe beveiligingsgroep aan en voeg regels toe om SSH (poort 22) en HTTP/HTTPS (poort 80/443) verkeer toe te staan.
7. Lanceer de EC2-instance en sla de sleutelpaar (.pem-bestand) op om later verbinding te kunnen maken via SSH.

### Stap 3: Maak een nieuwe RDS-database aan:

1. Navigeer naar de RDS-service in de AWS Management Console.
2. Klik op "Create database" om een nieuwe database aan te maken.
3. Kies het database-engine (bijvoorbeeld PostgreSQL), en configureer de database-instellingen zoals het type en de grootte van de database.
4. Configureer de beveiligingsgroepen om toegang tot de database te beperken tot specifieke IP-adressen indien nodig.
5. Start de RDS-database en onthoud de verbindingsgegevens voor later gebruik.

## Deel 2: Installatie van Pretix

### Stap 4: Verbind met je EC2-instance via SSH:

1. Gebruik een terminalvenster op je lokale computer en navigeer naar de locatie waar je het .pem-sleutelpaar hebt opgeslagen.
2. Gebruik het volgende commando om verbinding te maken met je EC2-instance via SSH:
   ```bash
   ssh -i your-key.pem ubuntu@your-instance-public-ip
   ```
   Vervang "your-key.pem" door de naam van je .pem-sleutelpaar en "your-instance-public-ip" door het openbare IP-adres van je EC2-instance.

### Stap 5: Installeer de benodigde software op de EC2-instance:

1. Update de pakketlijsten en installeer de benodigde software:
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip python3-venv postgresql nginx
   ```
2. Maak een nieuwe virtuele omgeving aan voor Pretix:
   ```bash
   python3 -m venv pretix-env
   source pretix-env/bin/activate
   ```

### Stap 6: Download en installeer Pretix:

1. Download de nieuwste versie van Pretix van GitHub:
   ```bash
   git clone https://github.com/pretix/pretix.git
   ```
2. Navigeer naar de map met de gedownloade Pretix-broncode:
   ```bash
   cd pretix
   ```
3. Installeer Pretix en zijn afhankelijkheden met behulp van pip:
   ```bash
   pip install -r requirements.txt
   ```

### Stap 7: Configureer Pretix:

1. Kopieer het voorbeeldconfiguratiebestand en rename het naar `config.yml`:
   ```bash
   cp src/pretix/settings.py.example src/pretix/settings.py
   ```
2. Bewerk het configuratiebestand `settings.py` en configureer de instellingen zoals vereist, inclusief de databaseverbinding.

### Stap 8: Initialiseer de database:

1. Initialiseer de PostgreSQL-database voor Pretix en voer migraties uit om de database te maken:
   ```bash
   python src/manage.py migrate
   ```

### Stap 9: Start de Pretix-server:

1. Start de Pretix-server met het volgende commando:
   ```bash
   python src/manage.py runserver 0.0.0.0:8000
   ```

### Stap 10: Toegang tot Pretix:

1. Open een webbrowser en ga naar het openbare IP-adres van je EC2-instance, gevolgd door poort 8000 (bijvoorbeeld http://jouw-domein-public-ip:8000).
2. Je zou de Pretix-webinterface moeten zien en je kunt beginnen met het configureren en gebruiken van Pretix voor het beheren van je evenementen.

Dit zijn de basisstappen om Pretix te installeren en configureren op een AWS EC2-instance
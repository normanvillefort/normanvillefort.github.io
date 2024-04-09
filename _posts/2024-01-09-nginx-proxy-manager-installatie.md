---
title: Nginx Proxy Manager Installatie
date: 2024-01-09 12:26:06 -300
categories: [Opensource, Installatie]
tags: [nginxproxymanager, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-nginxproxymngrinstall.webp
---

Nginx Proxy Manager is een open-source applicatie die wordt gebruikt voor het beheren van proxy hosts en reverse proxy's via een gebruiksvriendelijke webinterface. Het biedt een eenvoudige manier om meerdere domeinen en subdomeinen naar verschillende interne services te routeren, waardoor het gemakkelijk is om externe toegang te bieden tot verschillende webapplicaties en services die op je netwerk worden gehost. Het belangrijkste doel van Nginx Proxy Manager is om het proces van het configureren en beheren van Nginx-reverse proxy's te vereenvoudigen, zelfs voor gebruikers zonder diepgaande kennis van Nginx-configuratiebestanden.

## Belangrijkste kenmerken van Nginx Proxy Manager:

1. **Gebruiksvriendelijke webinterface:** Nginx Proxy Manager wordt geleverd met een intuïtieve webinterface waarmee gebruikers eenvoudig proxy hosts en reverse proxy's kunnen beheren via een grafische gebruikersinterface (GUI).
2. **Ondersteuning voor meerdere domeinen:** Gebruikers kunnen meerdere domeinen en subdomeinen toevoegen aan Nginx Proxy Manager en deze naar verschillende interne services routeren, waardoor het gemakkelijk wordt om toegang te bieden tot verschillende webapplicaties en services.
3. **SSL-certificaatbeheer:** Nginx Proxy Manager biedt ingebouwde ondersteuning voor SSL-certificaten, waardoor gebruikers gemakkelijk SSL-certificaten kunnen genereren, importeren en beheren voor hun gehoste domeinen en services.
4. **Automatische configuratie van Nginx:** De wijzigingen die in Nginx Proxy Manager worden aangebracht, worden automatisch toegepast op de Nginx-configuratie, waardoor gebruikers zich geen zorgen hoeven te maken over het handmatig bewerken van Nginx-configuratiebestanden.
5. **Logging en monitoring:** Nginx Proxy Manager biedt logging- en monitoringfuncties waarmee gebruikers toegang hebben tot gedetailleerde logboeken en statistieken van het verkeer dat door de reverse proxy wordt verwerkt.

## Gebruiksscenario van Nginx Proxy Manager:

Een bedrijf host verschillende interne webapplicaties en services op hun server en wil externe toegang bieden tot deze applicaties via het internet. Hier is een specifiek gebruiksscenario:

*Externe toegang tot interne services:* Het bedrijf gebruikt Nginx Proxy Manager om externe toegang te bieden tot verschillende interne webapplicaties en services die op hun server worden gehost. Ze configureren Nginx Proxy Manager om meerdere domeinen en subdomeinen te routeren naar de juiste interne services met behulp van reverse proxy-regels.
Dit stelt externe gebruikers in staat om eenvoudig toegang te krijgen tot verschillende webapplicaties en services door simpelweg het relevante domein of subdomein in hun webbrowser in te voeren.

Nginx Proxy Manager biedt, kort gezegd, een eenvoudige en gebruiksvriendelijke oplossing voor het beheren van proxy hosts en reverse proxy's, waardoor het gemakkelijk is om externe toegang te bieden tot interne webapplicaties en services zonder gedoe met handmatige configuratie van Nginx.

# Aan de slag

Om Nginx Proxy Manager te installeren op je Proxmox-server, kun je de volgende stappen volgen:

## Stap 1: Maak een nieuwe Ubuntu Server VM:
1. Log in op de Proxmox-UI.
2. Navigeer naar de gewenste opslaglocatie waar je de VM wilt maken.
3. Klik op "Create VM" om een nieuwe virtuele machine te maken.
4. Geef de VM een naam, bijvoorbeeld "Nginx Proxy Manager".
5. Kies de juiste resources (CPU, geheugen, opslag) voor je VM, afhankelijk van je behoeften.
6. Selecteer "OS" en kies "Ubuntu" als het besturingssysteem.
7. Klik op "Next".

## Stap 2: Installeer Ubuntu Server:

1. Mount het Ubuntu Server ISO-image op de nieuw gemaakte VM.
2. Start de VM en boot vanaf het Ubuntu Server ISO-image.
3. Volg de installatie-instructies op het scherm om Ubuntu Server te installeren op de VM.
4. Tijdens de installatie configureer je de netwerkinterfaces volgens je netwerkomgeving, gebruikmakend van de verstrekte IP-adressen, gateway en DNS-server.

## Stap 3: Installeer Nginx Proxy Manager:

1. Zodra Ubuntu Server is geïnstalleerd en je bent ingelogd, open je een terminalvenster.
2. Voer de volgende commando's uit om de benodigde packages te installeren:
   ```bash
   sudo apt update
   sudo apt upgrade
   sudo apt install -y curl gnupg2
   ```
3. Voeg de Nginx-repository toe aan je systeem en installeer Nginx:
   ```bash
   curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -
   sudo add-apt-repository "deb https://nginx.org/packages/ubuntu/ $(lsb_release -cs) nginx"
   sudo apt update
   sudo apt install -y nginx
   ```
4. Voeg de Nginx Proxy Manager-repository toe en installeer Nginx Proxy Manager:
   ```bash
   sudo curl -fsSL https://nginxproxymanager.com/keys/nginxproxymanager_signing.key | sudo apt-key add -
   sudo add-apt-repository "deb https://nginxproxymanager.com/debian $(lsb_release -cs) stable"
   sudo apt update
   sudo apt install -y nginx-proxy-manager
   ```
5. Start Nginx Proxy Manager en stel het in om automatisch te starten bij het opstarten:
   ```bash
   sudo systemctl enable --now nginx
   sudo systemctl enable --now nginx-proxy-manager
   ```

## Stap 4: Toegang tot Nginx Proxy Manager:

1. Nadat Nginx Proxy Manager is geïnstalleerd, open je een webbrowser en ga je naar het IP-adres van je server gevolgd door poort 81 (bijvoorbeeld http://192.168.0.23:81).
2. Je wordt doorgestuurd naar de Nginx Proxy Manager-webinterface, waar je de configuratie kunt beheren.

Dit zijn de basisstappen om Nginx Proxy Manager te installeren op je Proxmox-server. Vergeet niet de officiële documentatie van Nginx Proxy Manager te raadplegen voor meer gedetailleerde instructies en geavanceerde configuraties.

---

Om een reverse proxy te configureren in Nginx Proxy Manager, volg je deze stappen:

## Stap 1: Toegang tot Nginx Proxy Manager:

1. Open een webbrowser en ga naar het IP-adres van je server gevolgd door poort 81 (bijvoorbeeld http://192.168.0.23:81).
2. Log in op de Nginx Proxy Manager-webinterface met je gebruikersnaam en wachtwoord.

## Stap 2: Maak een Host aan:

1. Klik op "Hosts" in de navigatiebalk aan de linkerkant.
2. Klik op de knop "Add Host" in de rechterbovenhoek.
3. Vul de volgende informatie in:
   - **Domain Names**: Voer de domeinnaam in voor je reverse proxy (bijv. example.com).
   - **Scheme**: Kies het gewenste protocol (HTTP of HTTPS).
   - **Forward Hostname/IP**: Voer het interne IP-adres of hostname in van de service waarnaar je wilt doorverwijzen.
   - **Forward Port**: Voer de poort in waarop de interne service luistert.
4. Klik op "Save" om de host toe te voegen.

## Stap 3: Maak een Proxy Host aan:

1. Klik op "Proxy Hosts" in de navigatiebalk aan de linkerkant.
2. Klik op de knop "Add Proxy Host" in de rechterbovenhoek.
3. Vul de volgende informatie in:
   - **Domain Names**: Voer de domeinnaam in voor je reverse proxy (bijv. example.com).
   - **Destination**: Selecteer de host die je eerder hebt aangemaakt in de vervolgkeuzelijst.
   - **HTTP Protocol**: Selecteer het gewenste protocol (HTTP of HTTPS).
   - **SSL Certificate**: Kies het SSL-certificaat dat je wilt gebruiken (optioneel als je HTTPS gebruikt).
4. Klik op "Save" om de proxy host toe te voegen.

## Stap 4: Configureer SSL (optioneel):

1. Als je HTTPS hebt ingeschakeld, kun je SSL-certificaten toevoegen en configureren onder "SSL Certificates" in de navigatiebalk.
2. Klik op de knop "Add SSL Certificate" om een nieuw certificaat toe te voegen en volg de instructies op het scherm.

## Stap 5: Test de configuratie:

1. Nadat je de reverse proxy hebt geconfigureerd, test je de configuratie door de domeinnaam in je webbrowser in te voeren en te controleren of je correct wordt doorgestuurd naar de interne service.

Dat zijn de standaard stappen om een reverse proxy te configureren in Nginx Proxy Manager. Je kunt meer geavanceerde configuraties toepassen, zoals het toevoegen van aangepaste headers, het configureren van SSL-ciphers en meer, afhankelijk van je specifieke behoeften en vereisten. Raadpleeg de officiële documentatie van Nginx Proxy Manager voor meer gedetailleerde informatie en geavanceerde configuratie-opties.
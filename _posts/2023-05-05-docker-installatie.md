---
title: Docker Installatie
date: 2023-05-05 21:11:06 -300
categories: [Docker, Installatie]
tags: [docker, installatie]     # TAG names should always be lowercase
image:
 path: /assets/img/headers/hero-dockerinstall.webp
---

# Aan de slag

Docker is een platform voor het ontwikkelen, leveren en uitvoeren van applicaties in gecontaineriseerde omgevingen. Het biedt de mogelijkheid om applicaties en hun afhankelijkheden te verpakken in containers, waardoor ze geïsoleerd en draagbaar zijn over verschillende systemen.

## Introductie

Hier is een beknopte uitleg van wat Docker is en waar het voor gebruikt wordt, samen met een use case:

### **Wat is Docker?**
- Docker is een containerisatieplatform waarmee ontwikkelaars applicaties kunnen bouwen, testen en implementeren in geïsoleerde omgevingen, bekend als containers.
- Containers zijn lichtgewicht, draagbaar en zelfstandig uitvoerbare eenheden die alle benodigde software, bibliotheken en instellingen bevatten om een specifieke applicatie uit te voeren.
- Docker maakt gebruik van containerisatietechnologie om een consistente omgeving te bieden voor het ontwikkelen en implementeren van applicaties, ongeacht het onderliggende besturingssysteem of de infrastructuur.

### **Waar wordt Docker voor gebruikt?**
1. Applicatieontwikkeling en -tests: Ontwikkelaars gebruiken Docker om applicaties te bouwen, te testen en te debuggen in een geïsoleerde omgeving die dezelfde configuratie heeft als de productieomgeving. Dit helpt bij het verminderen van compatibiliteitsproblemen en zorgt voor een consistente ontwikkelingsworkflow.
2. Microservices-architectuur: Organisaties gebruiken Docker om applicaties op te splitsen in kleinere, onafhankelijke services, bekend als microservices. Deze services worden elk in hun eigen container uitgevoerd, waardoor ze gemakkelijk kunnen worden geschaald, bijgewerkt en vervangen zonder verstoring van andere services.
3. Continu levering en implementatie (CI/CD): Docker maakt het gemakkelijk om applicaties automatisch te bouwen, te testen en te implementeren met behulp van CI/CD-pijplijnen. Ontwikkelaars kunnen Docker-images maken die alle benodigde code en afhankelijkheden bevatten, en deze images vervolgens implementeren op elke omgeving met behulp van geautomatiseerde implementatietools.
4. Cloud-native ontwikkeling: Docker wordt veel gebruikt in cloud-native ontwikkeling, waarbij applicaties worden gebouwd met schaalbare, gedistribueerde architecturen die zijn ontworpen voor de cloud. Docker-containers kunnen gemakkelijk worden geïmplementeerd en beheerd in cloudomgevingen zoals AWS, Azure en Google Cloud Platform.

### **Use Case:**
Een bedrijf wil een webapplicatie ontwikkelen die schaalbaar, betrouwbaar en gemakkelijk te implementeren is. Ze besluiten Docker te gebruiken voor de ontwikkeling van de applicatie vanwege de voordelen van containerisatie.
- Ontwikkelaars gebruiken Docker om de webapplicatie en al zijn afhankelijkheden in containers te verpakken. Dit zorgt voor een consistente ontwikkelingsomgeving en vereenvoudigt het delen van code tussen teamleden.
- Na de ontwikkeling testen de ontwikkelaars de applicatie lokaal in Docker-containers om ervoor te zorgen dat deze goed werkt en compatibel is met andere componenten.
- Zodra de applicatie gereed is voor implementatie, maken de ontwikkelaars Docker-images van de applicatie en implementeren deze op een Kubernetes-cluster in de cloud. Dit stelt het bedrijf in staat om de applicatie gemakkelijk te schalen, te beheren en bij te werken in een productieomgeving.

Al met al biedt Docker een flexibele en krachtige oplossing voor het ontwikkelen, implementeren en schalen van moderne applicaties in uiteenlopende omgevingen.

## Installatie instructies

Hier zijn de stappen om Docker te installeren op een HP ProLiant-fysieke server met Ubuntu Server als het besturingssysteem:

### **Stap 1: Update het systeem:**
- Voordat je Docker installeert, is het een goede gewoonte om ervoor te zorgen dat je systeem up-to-date is. Voer de volgende opdrachten uit om je pakketlijsten bij te werken en eventuele beschikbare updates te installeren:
   ```
   sudo apt update
   sudo apt upgrade
   ```

### **Stap 2: Installeer Docker:**
1. Verwijder eventuele oudere versies van Docker die mogelijk zijn geïnstalleerd:
   ```
   sudo apt remove docker docker-engine docker.io containerd runc
   ```
2. Installeer de benodigde pakketten om Docker vanuit de officiële Docker-repository te kunnen installeren:
   ```
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```
3. Voeg de Docker GPG-sleutel toe aan het systeem voor het verifiëren van de pakketbron:
   ```
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```
4. Voeg de Docker APT-pakketrepository toe aan de pakketbronnen van je systeem:
   ```
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```
5. Werk de pakketlijsten opnieuw bij nu de Docker-pakketrepository is toegevoegd:
   ```
   sudo apt update
   ```
6. Installeer Docker door het volgende commando uit te voeren:
   ```
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```

### **Stap 3: Controleer of Docker correct is geïnstalleerd:**
- Voer het volgende commando uit om de Docker-versie te controleren:
   ```
   docker --version
   ```
   Dit zou de geïnstalleerde versie van Docker moeten weergeven.

### **Optionele stap: Gebruiker toevoegen aan de Docker-groep:**
- Om Docker-opdrachten zonder sudo uit te kunnen voeren, kun je de huidige gebruiker toevoegen aan de Docker-groep met het volgende commando:
   ```
   sudo usermod -aG docker $USER
   ```
   Log daarna uit en log opnieuw in om de wijzigingen door te voeren.

Nu zou Docker succesvol geïnstalleerd moeten zijn op de HP ProLiant-fysieke server met Ubuntu Server als het besturingssysteem. Je kunt nu containers maken, uitvoeren en beheren op deze server. Vergeet niet om Docker-containers te configureren en te beheren op basis van je specifieke behoeften en om de veiligheid van de server en containers te waarborgen.
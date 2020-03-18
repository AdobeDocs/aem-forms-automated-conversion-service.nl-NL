---
title: Inleiding
description: 'Afdrukformulieren sneller omzetten in aangepaste formulieren '
translation-type: tm+mt
source-git-commit: ceff5cb56aa9896a28004628c5e26c262b7918bd

---


# Inleiding {#introduction-to-automated-forms-conversion-service}

De service voor automatische conversie van formulieren helpt de digitalisering en modernisering van het vastleggen van gegevens te versnellen door de automatische conversie van PDF-formulieren naar adaptieve formulieren. De service, aangedreven door Adobe Sensei, converteert uw PDF-formulieren automatisch naar apparaatvriendelijke, responsieve en op HTML5 gebaseerde adaptieve formulieren. Tijdens het gebruik van de bestaande investeringen in PDF-formulieren en XFA past de service tijdens de conversie ook de juiste validaties, opmaak en indeling toe op adaptieve formuliervelden. De service helpt:

* Sla afdrukformulieren handmatig op om ze om te zetten in aangepaste formulieren
* Past patronen en aangewezen bevestigingen tijdens omzetting toe
* Document van record genereren tijdens conversie
* Veelvoorkomende velden groeperen in herbruikbare formulierfragmenten
* Adobe Analytics inschakelen tijdens conversie

![Het is eenvoudig. U geeft ons gewoon de bronformulieren en laat alles aan ons over. We zullen je prachtige adaptieve vormen aanbieden. Natuurlijk, zult u met de output aan uw tevredenheid kleven. ](assets/pdf-to-adaptive-form-gitx50.gif)

## On-boarding {#onboarding}

De service is gratis beschikbaar voor klanten op locatie met AEM 6.4 Forms en AEM 6.5 Forms en Adobe Managed Service Enterprise-klanten. U kunt contact opnemen met het verkoopteam van Adobe of uw Adobe-vertegenwoordiger om toegang tot de service te vragen.

Adobe biedt uw organisatie toegang tot deze gegevens en verleent de persoon die in uw organisatie als beheerder is aangewezen de vereiste bevoegdheden. De beheerder kan toegang tot uw ontwikkelaars (gebruikers) van Vormen AEM van uw organisatie verlenen om met de dienst te verbinden. Zie De service [Automated Forms Conversion](configure-service.md) configureren voor meer informatie.

## Ondersteunde PDF-formulieren en -talen {#supported-languages-and-pdf-forms}

De service ondersteunt niet-interactieve PDF-formulieren, formulieren die zijn gemaakt met Adobe Acrobat, bekend als AcroForms, en op XFA gebaseerde formulieren die zijn gemaakt met AEM Forms of Adobe LiveCycle.

De service kan alleen Engelstalige formulieren converteren naar adaptieve formulieren. U kunt de gegenereerde adaptieve formulieren naar een andere taal vertalen met behulp van de [AEM-vertaalworkflow](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).

## Conversieworkflow {#conversion-workflow}

De service Automated Forms Conversion wordt uitgevoerd op Adobe Cloud. U verbindt uw AEM-instantie met de service, uploadt formulieren naar uw AEM-instantie en start de conversie. Het volledige conversieproces wordt hieronder weergegeven:

![Workflow](assets/conversion-workflow.png)

### 1. De omgeving instellen {#set-up-the-environment}

De service Automated Forms Conversion wordt uitgevoerd op Adobe Cloud. [Configureer de Adobe I/O-account van uw organisatie en verbind uw lokale AEM-instantie](configure-service.md) met de conversieservice die wordt uitgevoerd op Adobe Cloud.

### 2. PDF-formulieren converteren naar adaptieve formulieren {#use-the-conversion-service}

Nadat de AEM Forms-omgeving is geconfigureerd, kunt u PDF-formulieren naar adaptieve formulieren converteren door PDF-formulieren [te](convert-existing-forms-to-adaptive-forms.md) uploaden naar uw AEM-exemplaar en de conversie [te](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)starten. Overweeg het volgende voordat u de formulieren uploadt:

* Upload de beveiligde formulieren niet. De service converteert formulieren die met een wachtwoord zijn beveiligd en versleuteld niet.
* Upload geen gescande, gekleurde, niet-Engelse taal en ingevulde formulieren. Dergelijke formulieren worden niet ondersteund.
* Upload geen PDF-formulieren met spaties in de bestandsnaam.
* Upload geen [PDF-portfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). De service converteert een PDF-portfolio niet naar adaptieve formulieren.
* Breng de voorgestelde wijzigingen aan in PDF-formulieren die worden beschreven in het artikel met [aanbevolen procedures en overwegingen](styles-and-pattern-considerations-and-best-practices.md) .
* Lees het [artikel Bekende problemen](known-issues.md) om valkuilen te voorkomen.

### 3. Omgezette formulieren controleren {#review-converted-forms}

In werkelijkheid kunnen formulieren complexe vereisten voor gegevensvastlegging hebben op het gebied van veldindeling, naamgeving of impliciete suggesties die mogelijk niet nauwkeurig worden vastgelegd door op AI/ML gebaseerde detectielogica. Zodra de geautomatiseerde omzetting is voltooid, kunt u de redacteur [van het](review-correct-ui-edited.md) Overzicht en van het Correct gebruiken om omgezette vorm te herzien en noodzakelijke updates te maken en een verbeterde output dichter aan gewenste ervaring te produceren. Nadat u de vereiste wijzigingen hebt aangebracht, verzendt u het formulier opnieuw voor de conversie.

De tijd die nodig is voor geautomatiseerde conversie is afhankelijk van verschillende factoren, zoals de grootte van het invoerformulier, de complexiteit van het formulier, de lening in de verwerkingswachtrij van de service. De gebruiker wordt regelmatig op de hoogte gebracht van de voortgang via statusindicator in map/bestand. Wanneer de conversie is voltooid, wordt ook een e-mailmelding verzonden naar het geconfigureerde e-mailadres.

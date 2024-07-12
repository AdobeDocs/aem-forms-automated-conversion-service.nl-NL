---
title: Inleiding tot automatede form conversion (AFCS)
description: Printformulieren sneller converteren naar adaptieve formulieren
solution: Experience Manager Forms
feature: Adaptive Forms, Foundation Components
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: edabeac8-cd66-48ca-a99f-9643a1c184cf
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 52%

---

# Automatede form conversion (AFCS) {#introduction-to-automated-forms-conversion-service}

De service automatede form conversion (AFCS) helpt de digitalisering en modernisering van de ervaring op het gebied van gegevensvastlegging te versnellen door de automatische conversie van PDF forms naar adaptieve formulieren. De service, mogelijk gemaakt door Adobe Sensei, converteert uw PDF-formulieren automatisch naar apparaatvriendelijke, responsieve en op HTML5 gebaseerde adaptieve formulieren. De service maakt gebruik van de bestaande investeringen in PDF Forms en XFA, maar past tijdens de conversie ook de juiste validaties, styling en lay-out toe op adaptieve formuliervelden. De service helpt om:

* Benodigde inspanning te besparen om printformulieren om te zetten in adaptieve formulieren
* Patronen en geschikte validaties toe te passen tijdens conversie
* Document van record te genereren tijdens conversie
* Veelvoorkomende velden groeperen in herbruikbare formulierfragmenten
* Adobe Analytics in te schakelen tijdens conversie

![Het is eenvoudig. U geeft ons de bronformulieren en laat alles aan ons over. We bieden je prachtige adaptieve vormen. U kunt altijd naar wens met de uitvoer tikken. ](assets/pdf-to-adaptive-form-gitx50.gif)

## Onboarding {#onboarding}

De service is gratis beschikbaar voor AEM 6.4 Forms en AEM 6.5 Forms On-Premise-term klanten en Adobe-Managed Service Enterprise-klanten. U kunt het team van de Verkoop van de Adobe of uw vertegenwoordiger van de Adobe contacteren om toegang tot de dienst te verzoeken. De service is ook gratis en vooraf ingeschakeld voor AEM Forms as a Cloud Service klanten.

Adobe maakt toegang voor uw organisatie mogelijk en biedt de vereiste rechten aan de persoon die is aangewezen als beheerder in uw organisatie. De beheerder kan toegang verlenen aan de AEM Forms-ontwikkelaars (gebruikers) van uw organisatie om verbinding te maken met de service. Raadpleeg [De service voor automatische conversie van formulieren configureren](configure-service.md) voor meer informatie.

## Ondersteunde PDF forms en talen {#supported-languages-and-pdf-forms}

De service ondersteunt niet-interactieve PDF-formulieren, formulieren die zijn gemaakt met Adobe Acrobat (AcroForms) en op XFA gebaseerde formulieren die zijn gemaakt met AEM Forms of Adobe LiveCycle.

De service biedt ook ondersteuning voor PDF forms die geschikt zijn voor Adobe Sign. Als het PDF-bronformulier Adobe Sign-tekstcodes heeft, behoudt de service tijdens de conversie alle aan Adobe Sign gerelateerde informatie en worden de ondertekenaargegevens in de PDF van de bron gekoppeld aan de bijbehorende adaptieve formuliervelden. De functie is alleen beschikbaar voor AcroForms.

De service kan formulieren in het Engels, Frans, Duits, Spaans, Italiaans en Portugees omzetten in aangepaste formulieren. U kunt de geproduceerde adaptieve vormen aan een andere taal ook vertalen gebruikend [ AEM vertaalwerkschema ](https://helpx.adobe.com/nl/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).

## Conversieworkflow  {#conversion-workflow}

AFCS (automatede form conversion Service) wordt uitgevoerd op Adobe Cloud. U verbindt uw AEM-instantie aan de service, uploadt formulieren naar uw AEM-instantie en start de conversie. Het volledige conversieproces is zoals hieronder vermeld:

![Workflow](assets/conversion-workflow.png)

### 1. De omgeving instellen {#set-up-the-environment}

AFCS (automatede form conversion Service) wordt uitgevoerd op Adobe Cloud. [Configureer het Adobe I/O-account van uw organisatie en verbind uw lokale AEM-instantie](configure-service.md) met de conversieservice die wordt uitgevoerd op Adobe Cloud.

### 2. PDF forms omzetten in adaptieve formulieren {#use-the-conversion-service}

Nadat uw AEM Forms-omgeving is geconfigureerd, [uploadt u uw PDF-formulieren](convert-existing-forms-to-adaptive-forms.md) naar uw AEM-instantie en [start u de conversie ](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) om uw PDF-formulieren te converteren naar adaptieve formulieren. Houd rekening met het volgende voordat u de formulieren uploadt:

* Upload de beveiligde formulieren niet. De service converteert geen met een wachtwoord beveiligde en versleutelde formulieren.
* Upload geen gescande, gekleurde, ingevulde formulieren en formulieren in een andere taal dan Engels, Frans, Duits, Spaans, Italiaans en Portugees. Dergelijke formulieren worden niet ondersteund.
* Upload geen PDF-formulieren met spaties in de bestandsnaam.
* Upload geen [PDF-portfolio&#39;s](https://helpx.adobe.com/nl/acrobat/using/overview-pdf-portfolios.html). De service zet een PDF-Portfolio niet om in een adaptieve vorm.
* Breng de voorgestelde wijzigingen in PDF-formulieren aan. Deze worden beschreven in het artikel [Best practices en overwegingen](styles-and-pattern-considerations-and-best-practices.md).
* Lees het artikel [Bekende problemen](known-issues.md) om valkuilen te vermijden.

### 3. Omgezette formulieren controleren {#review-converted-forms}

In werkelijkheid kunnen formulieren complexe vereisten voor gegevensvastlegging hebben op het gebied van veldindeling, naamgeving of impliciete suggesties die mogelijk niet nauwkeurig worden vastgelegd door op AI/ML gebaseerde detectielogica. Zodra de automatische conversie is voltooid, kunt u de [editor voor controleren en corrigeren](review-correct-ui-edited.md) gebruiken om geconverteerde formulieren te controleren, waar nodig bij te werken en verbeterde resultaten produceren die dichter bij gewenste ervaring liggen. Nadat u de wijzigingen heeft aangebracht, stuurt u het formulier opnieuw voor conversie.

De tijd die nodig is voor automatische conversie is afhankelijk van verschillende factoren, zoals de grootte van het invoerformulier, de complexiteit van het formulier, de lening in de verwerkingswachtrij van de service. De gebruiker wordt regelmatig op de hoogte gebracht van de voortgang via de statusindicator in de map/het bestand. Wanneer de conversie is voltooid, wordt er ook een melding verstuurd naar het geconfigureerde e-mailadres.

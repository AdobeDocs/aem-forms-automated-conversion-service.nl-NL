---
title: Wat is nieuw? Opmerkingen bij de release - Automated Forms Conversion Service
description: 'Meer informatie over de nieuwste functies en oplossingen voor Automated Forms Conversion Service '
translation-type: tm+mt
source-git-commit: 01dfd20951314017d47713bfb1a2a5f2d563f434

---


# Automated Forms Conversion Service: Opmerkingen bij de release

De geautomatiseerde Dienst van de Omzetting van Vormen ontvangt voortdurende verbeteringen. Om up-to-date te blijven met de meest recente ontwikkelingen, bezoek deze pagina regelmatig. Op deze pagina vindt u informatie over:

* Laatste versies
* Nieuwe functies
* Bugfixes
* Verouderde functionaliteit
* Speciale instructies
* Toekomstige plannen voor wijzigingen

Deze pagina wordt elke maand bijgewerkt, dus maak regelmatig een nieuwe pagina.

## 20 maart 2020 (AFC-2020.03.1)

### Nieuwe functies

**Logische secties in een formulier automatisch detecteren**

Standaard maakt de service een apart bovenste venster voor elke pagina van een invoer-PDF-formulier. Nu kunt u de **[!UICONTROL Auto-detect logical sections]** optie selecteren om het idee van het maken van een afzonderlijk bovenste venster voor elke PDF-pagina te verwijderen en logische secties automatisch te detecteren. De dienstclubs verwant gebieden van een vorm aan een logische sectie. Alle velden die bijvoorbeeld betrekking hebben op het factuuradres, worden in één sectie opgenomen en alle velden die betrekking hebben op het verzendadres, worden in een andere sectie opgenomen. De service maakt ook een apart bovenste deelvenster voor elke automatisch gedetecteerde logische sectie.

### Verbeterde functies

**Verbeteringen in lijstdetectie**

De service is nu efficiënter voor het detecteren van lijsten met opsommingstekens en nummers. Het kan nu gemakkelijk lijsten op meerdere niveaus ontdekken.

### Speciale instructies

**Installeer het pakket Automated Forms Conversion Service Connector**

U hebt het aansluitpakket 1.1.38 of hoger nodig als u de nieuwste kenmerken en verbeteringen van de release AFC-2020.03.1 wilt gebruiken. U kunt het aansluitingspakket downloaden van [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN).

Als u al beschikt over een servicemilieu voor automatische Forms Conversion die de nieuwste functies van de conversieservice kan gebruiken, installeert u het meest recente servicepakket, het nieuwste invoegpakket voor AEM Forms en het nieuwste aansluitingspakket in de aangegeven volgorde. Voor gedetailleerde instructies, zie het [Configure het Geautomatiseerde de dienstartikel](configure-service.md) van de Omzetting van Vormen.

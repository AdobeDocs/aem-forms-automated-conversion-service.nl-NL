---
title: Wat is nieuw? Opmerkingen bij de release - Automated Forms Conversion Service
description: 'Meer informatie over de nieuwste functies en oplossingen voor Automated Forms Conversion Service '
translation-type: tm+mt
source-git-commit: dc17dfcb331df6144b8a7ce3c9c9d840b1182a95

---


# Automated Forms Conversion Service: Opmerkingen bij de release

De geautomatiseerde Dienst van de Omzetting van Vormen ontvangt voortdurende verbeteringen. Om up-to-date te blijven met de meest recente ontwikkelingen, bezoek deze pagina regelmatig. Op deze pagina vindt u informatie over:

* Vroege toegang
* Laatste versies
* Nieuwe functies
* verbeteringen
* Bugfixes
* Verouderde functionaliteit
* Speciale instructies
* Toekomstige plannen voor wijzigingen

## 20 maart 2020 (AFC-2020.03.1)

### Vroege toegang

**Logische secties in een formulier automatisch detecteren**

AFC-2020.03.1-release biedt vroege toegang tot de **[!UICONTROL Auto-detect logical sections]** functie.

Standaard maakt de service een apart bovenste venster voor elke pagina van een PDF-formulier. Nu kunt u met de **[!UICONTROL Auto-detect logical sections]** optie deelvensters op paginaniveau (op paginanummers gebaseerde deelvensters) neerzetten en alleen logische deelvensters maken.  De velden die niet tot een sectie met een voorgaande logische sectie behoren, en velden van een logische sectie die zich over twee aangrenzende pagina&#39;s uitstrekken, worden in één logische sectie samengevoegd. Als sommige velden van een logische sectie zich bijvoorbeeld aan het einde van pagina 1 bevinden en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden opgenomen in één logische sectie.

U hebt het schakelaarpakket 1.1.38 of hierboven nodig om de **[!UICONTROL Auto-detect logical sections]** eigenschap te gebruiken. U kunt het aansluitingspakket downloaden van [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1).

### Verbeterde functies

**Verbeteringen in lijstdetectie**

De service is nu efficiënter voor het detecteren van lijsten met opsommingstekens en nummers.
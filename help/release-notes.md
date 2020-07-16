---
title: Wat is er nieuw? Releaseopmerkingen - Service voor automatische conversie van formulieren
description: 'Kom meer te weten over de nieuwste functies en bugfixes voor de service voor automatische conversie van formulieren '
translation-type: tm+mt
source-git-commit: caa019d1a7dd1968a52df5ec5be4755e1c6c4ee6
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 94%

---


# Release-opmerkingen

De service voor automatische conversie van formulieren wordt voortdurend verbeterd. Bezoek deze pagina regelmatig om op de hoogte te blijven van de meest recente ontwikkelingen. Op deze pagina vindt u informatie over:

* Vroegtijdige toegang
* Laatste releases
* Nieuwe functies
* Verbeteringen
* Bugfixes
* Afgekeurde functionaliteit
* Speciale instructies
* Geplande wijzigingen


## 16 juli 2020 (AFC-2020.07.0)

### Wat is er verbeterd?

Verbeteringen in de automatische conversie van tekst-, formulier- en keuzegroepen naar overeenkomende adaptieve formuliercomponenten.

## 20 maart 2020 (AFC-2020.03.1)

### Vroegtijdige toegang

**Automatisch logische secties in een formulier detecteren**

De service creëert standaard een aparte, bovenliggende laag voor elke pagina van een PDF-formulier. Nu kunt u de optie **[!UICONTROL Auto-detect logical sections]** gebruiken om de lagen op paginaniveau (de op paginanummer gebaseerde lagen) te laten vallen en alleen logische lagen te maken. Hierbij worden ook de velden die niet bij een sectie met een voorafgaande logische sectie horen en de velden van een logische sectie die verspreid zijn over twee aangrenzende pagina&#39;s samengevoegd tot één enkele logische sectie. Als sommige velden van een logische sectie bijvoorbeeld aan het einde van pagina 1 staan en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden samengevoegd tot één enkele logische sectie.

### Wat is er verbeterd?

**Verbeterde detectie van lijsten**

De service kan nu efficiënter lijsten met opsommingstekens en genummerde lijsten detecteren.

### Speciale instructies

**Connectorpakket voor de service voor automatische conversie van formulieren installeren**

U hebt het connectorpakket 1.1.38 of hoger nodig om de nieuwste functies en verbeteringen van de release AFC-2020.03.1 te gebruiken. U kunt het connectorpakket downloaden via [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1).

Wanneer u al een goed werkende omgeving voor de service voor automatische conversie van formulieren hebt, installeert u eerst het nieuwste servicepakket, dan de meest recente add-on van AEM Forms en tot slot het laatste connectorpakket om de nieuwste functies van de conversieservice te gebruiken. Lees het artikel [De service voor automatische conversie van formulieren configureren](configure-service.md) voor gedetailleerde instructies.
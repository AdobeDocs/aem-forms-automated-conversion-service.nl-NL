---
title: Wat is er nieuw? Releaseopmerkingen - Service voor automatische conversie van formulieren
description: Kom meer te weten over de nieuwste functies en bugfixes voor de service voor automatische conversie van formulieren
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: fccafbc9-28c1-4736-922c-24d675b25213
source-git-commit: e95b4ed35f27f920b26c05f3398529f825948f1f
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 66%

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

## 24 feb. 2022 (AFC-2022.02.0) {#feb-2022}

* Extra mogelijkheden aan [secties automatisch omzetten in fragmenten](convert-existing-forms-to-adaptive-forms.md) om de weergavesnelheid van geconverteerde formulieren te verbeteren en het gemakkelijker te maken om grote formulieren in een adaptieve formuliereditor te laden.

## 29 aug. 2021 (AFC-2021.08.0) {#aug-2021}

* Toegevoegde mogelijkheid om PDF forms in het Italiaans en het Portugees om te zetten in een adaptieve vorm.

## 29 juli 2021 (AFC-2021.07.2) {#july-2021}

* Mogelijkheid toegevoegd om een PDF-formulier in het Frans, Duits en Spaans om te zetten in een adaptieve vorm.

## 24 juni 2021 (AFC-2021.06.2) {#june-2021}

### Wat is er verbeterd? {#june-2021-improvements}

Verbeterde nauwkeurigheid voor het automatisch detecteren van logische secties in de bronformulieren en het converteren van deze secties naar overeenkomstige adaptieve formulierdeelvensters.

## 03 mrt. 2021 (AFC-2021.02.2) {#mar-2021}

### Wat is er verbeterd? {#march-2021-improvements}

Verbeteringen in het ordenen van formulierinhoud in keuzegroepen en velden terwijl een bronformulier wordt geconverteerd naar een adaptief formulier.

## 20 februari 2021 (AFC-2021.01.2) {#feb-2021}

### Wat is er verbeterd? {#feb-2021-improvements}

Verbeteringen in het ordenen van formulierinhoud in deelvensters en het genereren van titels voor deelvensters tijdens het omzetten van een bronformulier in een adaptief formulier.

## 16 juli 2020 (AFC-2020.07.2) {#jul-2020}

### Wat is er nieuw? {#whats-new-jul-2020-}

Ondersteuning toegevoegd voor het converteren van gekleurde PDF-formulieren naar adaptieve formulieren.

### Wat is er verbeterd? {#jul-2020-improvements}

Verbeteringen voor automatische conversie van tekst-, formulier- en keuzegroepvelden naar overeenkomende componenten voor adaptieve formulieren.

## 20 maart 2020 (AFC-2020.03.1) {#mar-2020}

### Vroegtijdige toegang {#early-access}

**Automatisch logische secties in een formulier detecteren**

De service creëert standaard een aparte, bovenliggende laag voor elke pagina van een PDF-formulier. Nu kunt u de optie **[!UICONTROL Auto-detect logical sections]** gebruiken om de lagen op paginaniveau (de op paginanummer gebaseerde lagen) te laten vallen en alleen logische lagen te maken. Hierbij worden ook de velden die niet bij een sectie met een voorafgaande logische sectie horen en de velden van een logische sectie die verspreid zijn over twee aangrenzende pagina&#39;s samengevoegd tot één enkele logische sectie. Als sommige velden van een logische sectie bijvoorbeeld aan het einde van pagina 1 staan en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden samengevoegd tot één enkele logische sectie.

### Wat is er verbeterd? {#mar-2020-improvements}

**Verbeterde detectie van lijsten**

De service kan nu efficiënter lijsten met opsommingstekens en genummerde lijsten detecteren.

### Speciale instructies {#special-instructions}

**Connectorpakket voor de service voor automatische conversie van formulieren installeren**

U hebt het aansluitpakket 1.1.38 of hoger nodig als u de nieuwste kenmerken en verbeteringen van de release AFC-2020.03.1 wilt gebruiken.

Wanneer u al een goed werkende omgeving voor de service voor automatische conversie van formulieren hebt, installeert u eerst het nieuwste servicepakket, dan de meest recente add-on van AEM Forms en tot slot het laatste connectorpakket om de nieuwste functies van de conversieservice te gebruiken. Lees het artikel [De service voor automatische conversie van formulieren configureren](configure-service.md) voor gedetailleerde instructies.

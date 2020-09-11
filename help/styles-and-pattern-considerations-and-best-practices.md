---
title: 'Best practices en overwegingen '
seo-title: 'Best practices en overwegingen '
description: Tips en trucs voor de Automated Forms Conversion-service
seo-description: Lijst met stijlen en patronen in PDF forms bron die door de Automated Forms Conversion-service moeilijk te identificeren zijn
uuid: e24773a2-be14-4184-a168-48aa976d459a
topic-tags: introduction
discoiquuid: 79f2026e-73a5-4bd1-b041-d1399b4ad23e
translation-type: tm+mt
source-git-commit: e2298422e0af9b1c678e7604be3efb6da377d7dd
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 3%

---


# Aanbevolen werkwijzen en bekende complexe patronen {#Best-practices-and-considerations2}

Dit document bevat richtlijnen en aanbevelingen die beheerders, auteurs en ontwikkelaars van formulieren kunnen gebruiken wanneer ze met werken [!DNL Automated Forms Conversion service]. Hierin worden de beste werkwijzen besproken, van het voorbereiden van bronformulieren tot het corrigeren van complexe patronen die enige extra inspanning vereisen voor automatische conversie. Deze beste praktijken dragen collectief aan de algemene prestaties en de output van [!DNL Automated Forms Conversion service]bij.

## Aanbevolen procedures

De conversieservice converteert PDF forms die beschikbaar zijn op uw AEM- [!DNL Forms] exemplaar naar adaptieve formulieren. Met de onderstaande aanbevolen procedures kunt u de conversiesnelheid en nauwkeurigheid verbeteren. Bovendien helpen deze beste praktijken u tijd besparen die aan na omzettingsactiviteiten wordt doorgebracht.

### Voordat u de bron uploadt

U kunt alle PDF forms tegelijk uploaden of, indien nodig, gefaseerd. Houd rekening met het volgende voordat u de formulieren uploadt:

* Houd het aantal formulieren in een map kleiner dan 15 en houd het totale aantal pagina&#39;s in een map kleiner dan 50.
* Houd de map kleiner dan 10 MB. Bewaar formulieren niet in submappen.
* Houd het aantal pagina&#39;s in een formulier kleiner dan 15.
* Indelen van brondocumenten in een batch van 8-15 documenten. Bronformulieren met algemene adaptieve formulierfragmenten in één batch bewaren.
* Upload de beveiligde formulieren niet. De service converteert formulieren die met een wachtwoord zijn beveiligd niet.
* Do not upload the [PDF Portfolios](https://helpx.adobe.com/nl/acrobat/using/overview-pdf-portfolios.html). De service converteert een PDF-Portfolio niet naar een adaptief formulier.
* Upload geen gescande, niet-Engelse taal en ingevulde formulieren. Dergelijke formulieren worden niet ondersteund.
* Upload geen bronformulieren met spaties in de bestandsnaam. Verwijder de ruimte uit de naam van het bestand voordat u de formulieren uploadt.

Wanneer u een XDP-formulier gebruikt voor conversie, voert u de volgende stappen uit voordat u de XDP-bronformulieren uploadt:

* Analyseer het XDP-formulier en los visuele problemen op. Zorg ervoor dat het brondocument de beoogde besturingselementen en structuren gebruikt. Het bronformulier kan bijvoorbeeld selectievakjes hebben in plaats van keuzerondjes voor één selectie. Schakel selectievakjes in op keuzerondjes om een adaptief formulier met de gewenste onderdelen te maken.
* [Voeg bindingen aan het XDP-formulier](http://www.adobe.com/go/learn_aemforms_designer_65) toe voordat u de conversie start. Wanneer bindingen beschikbaar zijn in het XDP-bronformulier, past de service tijdens de conversie automatisch bindingen toe op de bijbehorende adaptieve formuliervelden. Hiermee bespaart u de tijd die nodig is om de bindingen handmatig toe te passen.
* [Voeg Adobe Sign-tags](https://helpx.adobe.com/sign/using/text-tag.html) toe aan het XDP-bestand. De service converteert Adobe Sign-tags automatisch naar overeenkomende aangepaste formuliervelden. Adaptieve Forms ondersteunt een beperkt aantal Adobe Sign-velden. Zie Adobe Sign [gebruiken in een aangepaste formulierdocumentatie](https://docs.adobe.com/content/help/en/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html) voor de volledige lijst met ondersteunde velden.
* Complexe tabellen in XDP-documenten indien mogelijk omzetten in eenvoudige tabellen. Een tabel met formuliervelden in tabelcellen, cellen met een oneven grootte, cellen met een rij- of kolombereik, samengevoegde cellen, gedeeltelijke randen of geen zichtbare rand wordt als een complexe tabel beschouwd. Een tabel met een van de bovenstaande items wordt als een complexe tabel beschouwd.
<!-- * Use sub-forms in XDP documents to create panels in adaptive forms. Service converts each sub-form to one or more adaptive form panels during conversion. -->

### Voordat u de conversie start

* Aangepaste formuliersjablonen maken. Sjablonen helpen u bij het opgeven van een uniforme structuur voor de vormen van uw organisatie of afdeling.
* Geef de kop- en voettekst op in de aangepaste formuliersjablonen. De service negeert de voettekst voor de koptekst van brondocumenten en gebruikt de voettekst voor de koptekst die is opgegeven in de adaptieve formuliersjabloon.
* Maak adaptieve formulierthema&#39;s. Thema&#39;s zorgen voor een uniforme vormgeving van uw organisatie of afdeling.
* Formuliergegevensmodel configureren voor opslaan en ophalen van een gegevensbron. Maak en configureer lees- en schrijfservices voor het formuliergegevensmodel.
* Maak adaptieve formulierfragmenten en configureer de service voor het gebruik van adaptieve formulierfragmenten.
* Gemeenschappelijke workflowmodellen voorbereiden voor de formulieren die automatisering van bedrijfsprocessen vereisen.
* Indien nodig Adobe Analytics configureren


## Leer complexe patronen

AEM [!DNL Forms Automated Conversion service] gebruikt kunstmatige intelligentie en machine het leren algoritmen om de lay-out en de gebieden van de bronvorm te begrijpen. Elke computerleerservice leert voortdurend van brongegevens en produceert een verbeterde uitvoer bij elke klus. Deze diensten leren van ervaringen als mensen.

[!DNL Automated Forms Conversion service] is opgeleid voor een groot aantal formulieren. Het identificeert gemakkelijk gebieden in een bronvorm en produceert adaptieve vormen. Er zijn echter enkele velden en stijlen in PDF forms die gemakkelijk zichtbaar zijn voor het oog, maar moeilijk te begrijpen zijn voor de service. De service kan verschillende veldtypen of deelvensters toewijzen aan bepaalde velden of stijlen. Alle dergelijke veld- en stijlpatronen worden hieronder weergegeven.

De dienst zou beginnen correcte gebieden of panelen aan deze patronen te identificeren en toe te wijzen aangezien het het leren van de brongegevens houdt. Voorlopig kunt u de [redacteur van het Overzicht en van het Correct](review-correct-ui-edited.md) gebruiken om dergelijke kwesties te bevestigen. Voordat u de problemen gaat verhelpen of verder gaat lezen, moet u vertrouwd zijn met [adaptieve formuliercomponenten](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html).

### Algemene patronen {#general}

| Patroon | Voorbeeld |
|--- |--- |
| **Patroonservice** <br>zet gevulde PDF forms niet om in een adaptief formulier. <br><br>**Resolutie** <br>Gebruik lege adaptieve formulieren. | ![Formulier invullen](assets/best-practice-filled-forms.png) |
| **De Patroonservice** <br>kan tekst en velden in een dicht formulier niet herkennen. <br><br>**Resolutie**<br> Vergroot de breedte tussen tekst en velden van een dicht formulier voordat u begint met omzetten. |  |
| **Patroonservice** <br>ondersteunt gescande formulieren niet. <br><br>**Resolutie** gebruikt <br>geen gescande formulieren. | ![Gescande vorm](assets/scanned-forms.png) |
| **Met de Patroonservice** <br>worden geen afbeeldingen en tekst in afbeeldingen geëxtraheerd. <br><br>**Resolutie**<br> voegt handmatig afbeeldingen of tekst toe aan geconverteerde formulieren. | ![Afbeelding met tekstformulier](assets/best-practice-image-with-text.png) |
| **Patroontabellen** <br>met gestippelde of onduidelijke randen en randen worden niet omgezet. <br><br>**Resolutie** : tabellen <br>gebruiken met duidelijke expliciete grenzen en randen. ondersteund. | ![Niet-duidelijk tabelformulier](assets/best-practice-table-dotted-non-clear.png) |
| **Patroonadaptieve** <br> formulieren ondersteunen geen verticale tekst uit het vak. De service zet verticale tekst dus niet om in de bijbehorende adaptieve Forms-tekst. <br><br>**Resolutie**<br> Gebruik indien nodig een adaptieve formuliereditor om verticale tekst toe te voegen. | ![Niet-duidelijk tabelformulier](assets/vertical-text.png) |



### Keuzegroep  {#choice-group}

| Patroon | Resolutie |
|--- |--- |
| **Opties voor de groep Patroonkeuze** <br> met andere vormen dan kader of cirkel worden niet omgezet in overeenkomende adaptieve formuliercomponenten. <br><br>**Resolutie**<br> Wijzig de keuzeopties in een vak of cirkel of gebruik de revisie en de correctiefunctie om de vormen te identificeren. | ![Keuzelijsten ](assets/best-practice-choice-group-options.png) |

### Form fields {#form-fields}

| Patroon | Resolutie |
|--- |--- |
| **De Patroonservice** <br> herkent geen velden zonder duidelijke randen. <br><br>**Revisie en redacteur voor resolutie**<br> gebruiken om dergelijke velden te identificeren. | ![velden met niet-duidelijke grenzen](assets/best-practice-fields-without-clear-borders.png) |
| **Patroonservice** <br> herkent mogelijk niet alle formuliervelden van een keuzegroep met bijschriften aan de onder- of rechterkant van een formulier. <br><br>**Resolutie** <br> van de redacteur van het Gebruik van de Controle en van het Correcte Gebruik om dergelijke gebieden te identificeren | ![Keuzelijsten](assets/best-practice-caption-bottom-right.png) |
| **Patroonservice** <br> voegt een verkeerd type samen of wijst een verkeerd type toe aan formuliervelden die zeer dicht bij elkaar zijn geplaatst of geen duidelijke randen hebben. <br><br>**Revisie en redacteur voor resolutie**<br> gebruiken om dergelijke velden te identificeren. | ![Keuzelijsten](assets/best-practice-placed-very-near.png) |
| **De Patroonservice** <br> herkent mogelijk geen velden met veraf gelegen bijschriften of een stippellijn tussen het bijschrift en het invoerveld. <br><br>**Resolutie** <br> : gebruik formuliervelden met duidelijke grenzen of gebruik Revisie en Correcte editor om dergelijke problemen op te lossen. | ![Velden ver weg of stippellijn tussen bijschriftvelden](assets/best-practice-far-away-captions-or-a-dotted-line.png) |

### Lijsten {#lists}

| Patroon | Resolutie |
|--- |--- |
| **Patroonlijsten** die formuliervelden bevatten, worden samengevoegd of niet geconverteerd naar de bijbehorende aangepaste <br>resolutie <br><br>**van formuliercomponenten Formuliervelden met duidelijke grenzen** <br>gebruiken of Revisie en Correctie gebruiken om dergelijke problemen op te lossen. | ![lijsten met keuzegroepen](assets/best-practice-lists-containing-form-fields.png) |
| **De** Dienst van het patroon <br>kan een paar genestelde lijsten onbepaalde <br><br>**Resolutie** <br> van het Gebruik van het Overzicht en van de Correcte redacteur verlaten om dergelijke kwesties te bevestigen. | ![lijsten met keuzegroepen](assets/best-practice-nested-lists.png) |
| **De Dienst van het patroon**<br> voegt sommige lijsten samen die keuzesegroepen met elkaar de Herziening en Correcte redacteur van het Gebruik van de <br><br>**Resolutie** <br> bevatten om dergelijke kwesties te bevestigen. | ![lijsten met keuzegroepen](assets/best-practice-check-box-in-table-cells.png) |

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fields without borders are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->

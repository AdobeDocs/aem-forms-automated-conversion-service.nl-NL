---
title: 'Best practices en overwegingen '
description: NIET PUBLICEREN
seo-description: NIET PUBLICEREN
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
translation-type: tm+mt
source-git-commit: b2d29c22a275f2dc6a82593cf5e441c8da0bba13
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 7%

---


# Best practices en overwegingen {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms Automated Conversion-service converteert een PDF-formulier naar een adaptief formulier. De service gebruikt kunstmatige intelligentie en computerleeralgoritmen om de indeling en velden van het bronformulier te begrijpen. Elke computerleerservice leert voortdurend van brongegevens en produceert een verbeterde uitvoer bij elke klus. Deze diensten leren van ervaringen als mensen.

De service automatede form conversion is opgeleid voor een groot aantal formulieren. Het identificeert gemakkelijk gebieden in een bronvorm en produceert adaptieve vormen. Er zijn echter enkele velden en stijlen in PDF forms die gemakkelijk zichtbaar zijn voor het oog, maar moeilijk te begrijpen zijn voor de service. De service kan verschillende veldtypen of deelvensters toewijzen aan bepaalde velden of stijlen. Alle dergelijke veld- en stijlpatronen worden hieronder weergegeven.

De dienst zou beginnen correcte gebieden of panelen aan deze patronen te identificeren en toe te wijzen aangezien het het leren van de brongegevens houdt. Voorlopig kunt u [Revisie en Correct](review-correct-ui-edited.md) redacteur gebruiken om dergelijke problemen op te lossen. Voordat u de problemen gaat verhelpen of verder gaat lezen, moet u bekend zijn met [adaptieve formuliercomponenten](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html).

## Algemeen {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Bekende patronen en resolutie</td> 
   <td width="70%">Voorbeeld</td> 
  </tr>
   <td><p><strong>Patroon</strong></p> <p>Service zet gevulde PDF forms niet om in een adaptieve vorm.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik lege adaptieve formulieren.</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De service kan tekst en velden in een dicht formulier niet herkennen.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Vergroot de breedte tussen tekst en velden in een dicht formulier voordat u de conversie start.</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De service ondersteunt geen gescande formulieren.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik geen gescande formulieren. </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De service extraheert geen afbeeldingen en tekst binnen afbeeldingen. </p> <p> </p> <p><strong>Resolutie</strong></p> <p>Voeg handmatig afbeeldingen of tekst toe aan geconverteerde formulieren.</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>Tabellen met gestippelde of onduidelijke grenzen en randen worden niet omgezet.</p> <p><strong>Resolutie</strong></p> <p>Gebruik tabellen met duidelijke expliciete grenzen en randen. ondersteund.</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## Keuzegroep {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Patroon</td> 
   <td width="70%">Voorbeeld</td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>Opties voor keuzegroepen met andere vormen dan kader of cirkel worden niet omgezet in overeenkomende adaptieve formuliercomponenten. </p> <p> </p> <p><strong>Resolutie</strong></p> <p>Wijzig de keuzeopties in een vak of cirkel of gebruik de revisie en de correctiefunctie om de vormen te identificeren.</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## Formuliervelden {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Patroon</td> 
   <td width="70%">Voorbeeld</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>Patroon</strong></p> <p>De dienst identificeert geen gebieden zonder duidelijke grenzen.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik Revisie en Correcte editor om dergelijke velden te identificeren.</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>Bij de service blijven sommige formuliervelden met bijschriften aan de onderkant of aan de rechterkant onbekend.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>De redacteur van het Overzicht en van de Correctie van het gebruik om dergelijke gebieden te identificeren</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De dienst voegt of wijst een verkeerd type aan sommige vormgebieden toe die zeer dicht bij elkaar worden geplaatst of geen duidelijke grenzen hebben. </p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik Revisie en Correcte editor om dergelijke velden te identificeren.</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De dienst kan er niet in slagen om gebieden met verre titels of een gestippelde lijn tussen de titel en inputgebied te erkennen.</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik formuliervelden met duidelijke grenzen of gebruik Revisie en Correcte editor om dergelijke problemen op te lossen.</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## Lijsten {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Patroon</td> 
   <td width="70%">Voorbeeld</td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>Lijsten met formuliervelden worden samengevoegd of niet geconverteerd naar overeenkomende adaptieve formuliercomponenten</p> <p><strong>Resolutie</strong></p> <p>Gebruik formuliervelden met duidelijke grenzen of gebruik Revisie en Correcte editor om dergelijke problemen op te lossen.</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De dienst kan een paar genestelde lijsten onge??dentificeerd verlaten</p> <p> </p> <p><strong>Resolutie</strong></p> <p>Gebruik de Editor controleren en corrigeren om dergelijke problemen op te lossen.</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>Patroon</strong></p> <p>De dienst voegt sommige lijsten samen die keuzegroepen met elkaar bevatten</p> <p><strong>Resolutie</strong></p> <p>Gebruik de Editor controleren en corrigeren om dergelijke problemen op te lossen.</p> </td> 
   <td><img src="assets/lists-containing-choice-groups.png" /> </td> 
  </tr>
 </tbody>
</table>

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fiields without bordes are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->


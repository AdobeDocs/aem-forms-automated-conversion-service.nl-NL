---
title: Document van record te genereren tijdens conversie
description: Aanbevolen paden om een DoR te genereren op basis van het type bronformulieren dat voor conversie wordt gebruikt.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
page-status-flag: never-activated
contentOwner: khsingh
exl-id: c24313cd-2b9b-4209-9505-a8e14d8dc530
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Aanbevolen workflows om het genereren van documenten voor adaptieve formulieren mogelijk te maken {#recommended-workflows-dor-generation}

Met het Document of Record (DoR) kunt u een record bijhouden van de gegevens die u opgeeft en kunt u deze in een adaptief formulier verzenden, zodat u er later naar kunt verwijzen.
Het DoR gebruikt een basissjabloon om zijn lay-out te bepalen. U kunt een DoR genereren door een standaardsjabloon te gebruiken of een andere sjabloon aan het aangepaste formulier te koppelen.

![ Gegenereerd Document van Verslag ](assets/document_of_record.gif)

Voor meer informatie bij het produceren van aDoR, zie [ Document van Verslag voor adaptieve vormen ](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) produceren.

De [ dienst van de Automatede form conversion (AFCS) ](/help/using/introduction.md) zet de volgende bronvormen in adaptieve vormen om:

* niet-interactieve PDF forms
* Acro Forms
* Op XFA gebaseerde PDF forms

Op basis van het bronformulier dat u gebruikt voor conversie, kunt u een DoR genereren met:

* een standaardsjabloon
* het bronformulier als sjabloon - Als u deze optie selecteert, koppelt de conversieservice het bronformulier automatisch aan het omgezette adaptieve formulier als de DoR-sjabloon.
* andere sjablonen aan het omgezette adaptieve formulier koppelen

De volgende lijst illustreert een voorbeeld van hoe het malplaatje van Dor dat u gebruikt de lay-out van geproduceerde DoR beïnvloedt:

<table> 
 <tbody>
 <tr>
  <td><p><strong>Source-formulier</strong></p></td>
  <td><p><strong>Gegenereerde DoR</strong></p></td> 
   </tr>
  <tr>
   <td><img src="assets/source_xdp_updated.png"/></td>
   <td><p>Als u het standaardmalplaatje gebruikt om DoR te produceren:</br><img src="assets/source_form_default_updated.png"/></td>
   </tr>
   <tr>
   <td></td>
   <td><p>Als u bronvorm als malplaatje gebruikt om DoR te produceren:</br></p><img src="assets/source_form_dor_updated.png"/></td>
   </tr>
  </tbody>
</table>

Als u het bronformulier als sjabloon gebruikt, behoudt het DoR-bestand de indeling van het bronformulier, zoals in de tabel wordt geïllustreerd.
In dit artikel worden de aanbevolen paden beschreven voor het genereren van een DoR op basis van de drie typen bronformulieren.

<table> 
 <tbody> 
  <tr> 
   <th><strong>Source-formulier</strong></th> 
   <th><strong>Methoden om DoR te genereren</strong></th> 
  </tr> 
  <tr> 
   <td><p>Niet-interactieve PDF forms</p></td> 
   <td> 
    <ul> 
     <li><a href="#generate-document-of-record-using-cloud-configuration">genereren van doR inschakelen vóór adaptieve formulierconversie om een doR te genereren met behulp van een standaardsjabloon</a></li> 
     <li><a href="#edit-adaptive-form-properties-generate-document-of-record">Adaptieve formuliereigenschappen bewerken na adaptieve formulierconversie om het genereren van DoR mogelijk te maken met behulp van de standaardinstelling of een andere formuliersjabloon</a></li> 
    </ul> </td> 
  </tr>
  <tr> 
   <td><p>Acro Forms of op XFA gebaseerde PDF forms</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">Het genereren van doR inschakelen vóór de adaptieve formulierconversie om DoR te genereren met het bronformulier als sjabloon</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">Aangepaste formuliereigenschappen bewerken na adaptieve formulierconversie om het genereren van DoR mogelijk te maken met de standaardsjabloon, het bronformulier als sjabloon of een andere formuliersjabloon</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## Document met record genereren voor niet-interactieve PDF forms {#generate-document-of-record-non-interactive-pdf}

Als u een niet-interactief PDF-formulier gebruikt als bronformulier voor AFCS (Automatede form conversion Service), kunt u:

* Schakel het genereren van DoR vóór de adaptieve formulierconversie in om een standaardsjabloon voor DoR te genereren
* of bewerk adaptieve formuliereigenschappen na adaptieve formulierconversie om het genereren van een doR mogelijk te maken met behulp van standaard of een ander formuliersjabloon

### genereren van doR inschakelen vóór conversie om DoR te genereren met de standaardsjabloon {#generate-document-of-record-using-cloud-configuration}

1. Selecteer **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Eigenschappen van de cloudconfiguratie die wordt gebruikt voor conversie > optie **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** .

   ![ produceer Document van Verslag gebruikend wolkenconfiguratie ](assets/generate_dor_cloud_config.gif)

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

1. [ stel de omzetting ](/help/using/convert-existing-forms-to-adaptive-forms.md) in werking. Zorg ervoor dat u de wolkenconfiguratie gebruikt die in stap 1 van deze instructies wordt uitgegeven.
Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met de standaardsjabloon.

### Aangepaste formuliereigenschappen bewerken na conversie om DoR-generatie in te schakelen {#edit-adaptive-form-properties-generate-document-of-record}

Als u het genereren van doR niet inschakelt voordat u het bronformulier omzet in een adaptief formulier, kunt u dit nog steeds doen na de conversie.

1. [ stel de omzetting ](/help/using/convert-existing-forms-to-adaptive-forms.md) op de niet-interactieve vorm van PDF in werking om een adaptieve vorm te produceren.

1. Selecteer het aangepaste formulier in de map **[!UICONTROL output]** en tik op **[!UICONTROL Properties]** .

1. Vouw op het tabblad **[!UICONTROL Form Model]** de sectie **[!UICONTROL Document of Record Template Configuration]** uit en selecteer **[!UICONTROL Generate Document of Record]** .

   ![ produceer Document van Verslag ](assets/generate_dor_af_properties.png)

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met de standaardsjabloon. Als u een andere DoR-sjabloon aan het omgezette adaptieve formulier wilt koppelen, kunt u de optie **[!UICONTROL Associate form template as the Document of Record template]** selecteren.

## Document met record genereren voor Acrobat Forms- of XFA-PDF forms {#generate-document-of-record-acroform-xfaform}

Als u een Acro-formulier of een XFA-gebaseerd PDF formulier gebruikt als bronformulier voor de service Automatede form conversion (AFCS), kunt u:

* Schakel het genereren van DoR vóór de adaptieve formulierconversie in om een DoR te genereren met het bronformulier als sjabloon

* of bewerk adaptieve formuliereigenschappen na adaptieve formulierconversie om het genereren van DoR mogelijk te maken met de standaardsjabloon, het bronformulier als sjabloon of een andere formuliersjabloon

### genereren van doR inschakelen vóór conversie om doR te genereren met behulp van bronformuliersjabloon {#use-input-form-as-template-to-generate-document-of-record}

1. Selecteer **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Eigenschappen van de cloudconfiguratie die wordt gebruikt voor conversie > optie **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** .

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

1. [ stel de omzetting ](/help/using/convert-existing-forms-to-adaptive-forms.md) in werking. Zorg ervoor dat u de wolkenconfiguratie gebruikt die in stap 1 van deze instructies wordt uitgegeven.
De conversieservice koppelt het Acro Form- of XFA-gebaseerde PDF-formulier automatisch aan het geconverteerde adaptieve formulier als de DoR-sjabloon.
U kunt de adaptieve formuliereigenschappen openen om de DoR-sjabloon weer te geven in de sectie **[!UICONTROL Document of Record Template Configuration]** van het tabblad **[!UICONTROL Form Model]** .

   ![ geef adaptieve vormeigenschappen uit om Document van Verslag te produceren ](assets/generate_dor_af_properties_xdp_acro.png)

   Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met behulp van de bronformuliersjabloon.

### Aangepaste formuliereigenschappen bewerken na conversie om DoR-generatie in te schakelen {#edit-adaptive-form-properties-to-generate-document-of-record}

1. [ stel de omzetting ](/help/using/convert-existing-forms-to-adaptive-forms.md) op de niet-interactieve vorm van PDF in werking om een adaptieve vorm te produceren.

1. Selecteer het aangepaste formulier in de map **[!UICONTROL output]** en tik op **[!UICONTROL Properties]** .

1. Vouw op het tabblad **[!UICONTROL Form Model]** de sectie **[!UICONTROL Document of Record Template Configuration]** uit en selecteer **[!UICONTROL Generate Document of Record]** om het genereren van doR in te schakelen met de standaardsjabloon.
U kunt ook de optie **[!UICONTROL Associate form template as the Document of Record template]** selecteren en de sjabloon selecteren om het genereren van een doR-bestand met behulp van een bronformuliersjabloon of een andere formuliersjabloon in te schakelen.

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

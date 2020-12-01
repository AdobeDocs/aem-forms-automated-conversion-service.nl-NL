---
title: Document van record te genereren tijdens conversie
seo-title: Document van record te genereren tijdens conversie
description: Aanbevolen paden om een DoR te genereren op basis van het type bronformulieren dat voor conversie wordt gebruikt.
seo-description: Aanbevolen paden om een DoR te genereren op basis van het type bronformulieren dat voor conversie wordt gebruikt.
page-status-flag: never-activated
uuid: 7f0f5bf3-21be-449a-b23e-5946a9fd7ed4
contentOwner: khsingh
discoiquuid: 75f6e6bc-7636-4b40-919c-8b20a6ccbb1f
translation-type: tm+mt
source-git-commit: 640d72d7961ef0c2393bf0ae6745d918e388a056
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# Aanbevolen workflows om document van recordgeneratie voor adaptieve workflows in te schakelen {#recommended-workflows-dor-generation}

Met het Document of Record (DoR) kunt u een record bijhouden van de gegevens die u opgeeft en kunt u deze in een adaptief formulier verzenden, zodat u er later naar kunt verwijzen.
Het DoR gebruikt een basissjabloon om zijn lay-out te bepalen. U kunt een DoR genereren door een standaardsjabloon te gebruiken of een andere sjabloon aan het aangepaste formulier te koppelen.

![Gegenereerd document van record](assets/document_of_record.gif)

Zie [Document van record genereren voor adaptieve formulieren](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) voor meer informatie over het genereren van een DoR.

De [service Automatede form conversion](../help/introduction.md) converteert de volgende bronformulieren naar adaptieve formulieren:

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
  <td><p><strong>Bronformulier</strong></p></td>
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
   <th><strong>Bronformulier</strong></th> 
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
   <td><p>PDF forms op basis van Acro Forms of XFA</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">Het genereren van doR inschakelen vóór de adaptieve formulierconversie om DoR te genereren met het bronformulier als sjabloon</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">Adaptieve formuliereigenschappen bewerken na adaptieve formulierconversie om het genereren van DoR mogelijk te maken met de standaardsjabloon, het bronformulier als sjabloon of een andere formuliersjabloon</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## Document met record genereren voor niet-interactieve PDF forms {#generate-document-of-record-non-interactive-pdf}

Als u een niet-interactief PDF-formulier gebruikt als bronformulier voor de service Automatede form conversion, kunt u:

* Schakel het genereren van DoR vóór de adaptieve formulierconversie in om een standaardsjabloon voor DoR te genereren
* of bewerk adaptieve formuliereigenschappen na adaptieve formulierconversie om het genereren van een doR mogelijk te maken met behulp van standaard of een ander formuliersjabloon

### Genereren van doR inschakelen vóór conversie om DoR te genereren met de standaardsjabloon {#generate-document-of-record-using-cloud-configuration}

1. Selecteer **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Eigenschappen van cloudconfiguratie die wordt gebruikt voor conversie > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** optie.

   ![Document met record genereren met cloudconfiguratie](assets/generate_dor_cloud_config.gif)

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

1. [Voer de conversie](../help/convert-existing-forms-to-adaptive-forms.md) uit. Zorg ervoor dat u de wolkenconfiguratie gebruikt die in stap 1 van deze instructies wordt uitgegeven.
Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met de standaardsjabloon.

### Aangepaste formuliereigenschappen bewerken na conversie om DoR-generatie {#edit-adaptive-form-properties-generate-document-of-record} in te schakelen

Als u het genereren van doR niet inschakelt voordat u het bronformulier omzet in een adaptief formulier, kunt u dit nog steeds doen na de conversie.

1. [Voer de ](../help/convert-existing-forms-to-adaptive-forms.md) conversie uit op het niet-interactieve PDF-formulier om een adaptief formulier te genereren.

1. Selecteer het aangepaste formulier in de map **[!UICONTROL output]** en tik **[!UICONTROL Properties]**.

1. Vouw op het tabblad **[!UICONTROL Form Model]** de sectie **[!UICONTROL Document of Record Template Configuration]** uit en selecteer **[!UICONTROL Generate Document of Record]**.

   ![Document van record genereren](assets/generate_dor_af_properties.png)

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met de standaardsjabloon. Als u een andere DoR-sjabloon aan het omgezette adaptieve formulier wilt koppelen, kunt u de optie **[!UICONTROL Associate form template as the Document of Record template]** selecteren.

## Document met record genereren voor Acrobat Forms- of XFA-PDF forms {#generate-document-of-record-acroform-xfaform}

Als u een Acro Form- of XFA-gebaseerd PDF-formulier gebruikt als bronformulier voor de service Automatede form conversion, kunt u:

* Schakel het genereren van DoR vóór de adaptieve formulierconversie in om een DoR te genereren met het bronformulier als sjabloon

* of bewerk adaptieve formuliereigenschappen na adaptieve formulierconversie om het genereren van DoR mogelijk te maken met de standaardsjabloon, het bronformulier als sjabloon of een andere formuliersjabloon

### Het genereren van DoR vóór omzetting inschakelen om DoR te genereren met behulp van bronformuliersjabloon {#use-input-form-as-template-to-generate-document-of-record}

1. Selecteer **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Eigenschappen van cloudconfiguratie die wordt gebruikt voor conversie > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** optie.

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

1. [Voer de conversie](../help/convert-existing-forms-to-adaptive-forms.md) uit. Zorg ervoor dat u de wolkenconfiguratie gebruikt die in stap 1 van deze instructies wordt uitgegeven.
De conversieservice koppelt het PDF-formulier op basis van Acro Form of XFA automatisch aan het geconverteerde adaptieve formulier als de DoR-sjabloon.
U kunt de adaptieve formuliereigenschappen openen om de DoR-sjabloon weer te geven in de sectie **[!UICONTROL Document of Record Template Configuration]** van het tabblad **[!UICONTROL Form Model]**.

   ![Aangepaste formuliereigenschappen bewerken om een document met records te genereren](assets/generate_dor_af_properties_xdp_acro.png)

   Bij het verzenden van het geconverteerde adaptieve formulier wordt de DoR automatisch gegenereerd met behulp van de bronformuliersjabloon.

### Aangepaste formuliereigenschappen bewerken na conversie om DoR-generatie {#edit-adaptive-form-properties-to-generate-document-of-record} in te schakelen

1. [Voer de ](../help/convert-existing-forms-to-adaptive-forms.md) conversie uit op het niet-interactieve PDF-formulier om een adaptief formulier te genereren.

1. Selecteer het aangepaste formulier in de map **[!UICONTROL output]** en tik **[!UICONTROL Properties]**.

1. Vouw op het tabblad **[!UICONTROL Form Model]** de sectie **[!UICONTROL Document of Record Template Configuration]** uit en selecteer **[!UICONTROL Generate Document of Record]** om het genereren van doR in te schakelen met de standaardsjabloon.
U kunt ook de optie **[!UICONTROL Associate form template as the Document of Record template]** selecteren en de sjabloon selecteren om het genereren van doR met bronformuliersjabloon of een andere formuliersjabloon in te schakelen.

1. Tik op **[!UICONTROL Save & Close]** om de instellingen op te slaan.

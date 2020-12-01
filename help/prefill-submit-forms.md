---
title: Aanbevolen vooraf ingevulde gegevens gebaseerd op gegevensbron en workflows toevoegen voor adaptieve formulieren
seo-title: Opties voor vooraf invullen en verzenden van aangepaste formulieren
description: Workflows op basis van gegevensbron vooraf invullen en verzenden voor adaptieve formulieren die zijn gegenereerd met de service Automatede form conversion.
seo-description: Workflows op basis van gegevensbron vooraf invullen en verzenden voor adaptieve formulieren die zijn gegenereerd met de service Automatede form conversion.
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
translation-type: tm+mt
source-git-commit: caccb547a5741eb0e70ddf75630a661f8fe75cb3
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 1%

---


# Aanbevolen vooraf ingevulde gegevens gebaseerd op gegevensbron en workflows toevoegen voor adaptieve formulieren {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

U kunt elk van de volgende gegevensbronnen gebruiken met adaptieve formulieren die zijn geconverteerd via de service Automatede form conversion:

* Formuliergegevensmodel, OData of een andere service van derden
* JSON-schema
* XSD-schema

Op basis van de gegevensbron kunt u desgewenst een adaptief formulier genereren met of zonder gegevensmodel.

In dit artikel worden de aanbevolen workflows beschreven voor het vooraf invullen van veldwaarden en verzendopties nadat u een gegevensbron hebt geselecteerd en een adaptief formulier hebt gegenereerd met behulp van de conversieservice.

<table> 
 <tbody> 
  <tr> 
   <th><strong>Gegevensbron</strong></th> 
   <th><strong>Aanbevolen workflow</strong></th> 
  </tr> 
  <tr> 
   <td><p>Formuliergegevensmodel, OData of een andere service van derden</p></td> 
   <td> 
    <p><strong>Optie 1</strong>: U selecteert formuliergegevensmodel, OData of een andere service van derden als gegevensbron. U <a href="#generate-adaptive-forms-with-no-data-binding">genereert een adaptief formulier zonder gegevensbinding</a> met de service Automatede form conversion. U bindt de adaptieve formuliervelden handmatig aan entiteiten van het formuliergegevensmodel en gebruikt de optie Vooraf ingevulde service formuliergegevensmodel om veldwaarden vooraf in te vullen. Met de optie Verzenden met gebruik van het formuliergegevensmodel kunt u het aangepaste formulier verzenden.</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>Optie 2</strong>: U selecteert formuliergegevensmodel, OData of een andere service van derden als gegevensbron. U <a href="#generate-adaptive-forms-with-no-data-binding">genereert een adaptief formulier zonder gegevensbinding</a> met de service Automatede form conversion. U bindt de aangepaste formuliervelden met de regeleditor aan het vooraf invullen van veldwaarden. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>Voor geleidelijke instructies om deze werkschema's uit te voeren, zie <a href="#sqldatasource">Gegevensbestand, OData, of om het even welke derdedienst als gegevensbron gebruiken.</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON Schema</p></td> 
   <td> 
    <p>U selecteert JSON-schema als gegevensbron. Gebaseerd op de geselecteerde gegevensbron:</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Optie 1</strong>: U  <a href="#generate-adaptive-forms-with-no-data-binding">genereert een adaptief formulier zonder </a> gegevensbinding met de service Automatede form conversion en configureert het JSON-schema als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan het JSON-schema en <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">gebruik een van de ondersteunde protocollen</a> om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Zie <a href="#jsondatasource">JSON-schema gebruiken als gegevensbron voor stapsgewijze instructies om de werkstromen uit te voeren.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Optie 2</strong>: U  <a href="#generate-adaptive-forms-with-json-binding">genereert een adaptief formulier met JSON-</a> gegevensbinding via de service Automatede form conversion. De Prefill-service en het verzenden van formulieren werken naadloos. U hebt geen configuratiestappen nodig.</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>Zie <a href="#jsonwithdatabinding">JSON-schema gebruiken als gegevensbron voor stapsgewijze instructies om de workflows uit te voeren.</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD-schema</p></td> 
   <td> 
    <p>U selecteert XSD-schema als gegevensbron. Op basis van de geselecteerde gegevensbron <a href="#generate-adaptive-forms-with-no-data-binding">genereert u een adaptief formulier zonder gegevensbinding</a> met de service Automatede form conversion en configureert u XSD-schema als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan het XSD-schema en <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">gebruik een van de ondersteunde protocollen</a> om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Voor geleidelijke instructies om de werkschema's uit te voeren, zie <a href="#xsddatasource">XSD schema als gegevensbron gebruiken.</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


Raadpleeg de volgende artikelen voor meer informatie over de service Automatede form conversion:

* [Inleiding tot de service voor automatische conversie van formulieren](introduction.md)
* [De service voor automatische conversie van formulieren configureren](configure-service.md)
* [Printformulieren converteren naar adaptieve formulieren](convert-existing-forms-to-adaptive-forms.md)
* [Geconverteerde formulieren controleren en corrigeren](review-correct-ui-edited.md)

De in dit artikel verstrekte informatie is gebaseerd op de veronderstelling dat iedereen die het leest basiskennis heeft van concepten van adaptieve formulieren.

## Voorwaarden {#pre-requisites}

* Een [AEM auteur-instantie](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html) configureren
* [Automatede form conversion-service op de AEM auteur-instantie configureren](configure-service.md)

## Monster van adaptief formulier {#sample-adaptive-form}

Download het volgende voorbeeld-PDF-bestand als u de gebruiksgevallen wilt uitvoeren om veldwaarden vooraf in een adaptief formulier in te vullen en naar de gegevensbron te verzenden.

Voorbeeldformulier voor het aanvragen van een lening

[Bestand ophalen](assets/sample_loan_application_form.pdf)

Het PDF-bestand fungeert als invoer voor de service Automatede form conversion. De service converteert dit bestand naar een adaptief formulier. De volgende afbeelding toont de voorbeeldtoepassing voor leningen in PDF-indeling.

![aanvraagformulier voor een voorbeeldlening](assets/sample_form_new.png)

## Gegevens voorbereiden voor formuliermodel {#prepare-data-for-form-model}

Met AEM Forms Data Integration kunt u verschillende gegevensbronnen configureren en verbinden. Nadat u een adaptief formulier hebt gegenereerd met behulp van het conversieproces, kunt u het formuliermodel definiëren op basis van een formuliergegevensmodel, XSD of een JSON-schema. U kunt een gegevensbestand, de Dynamica van Microsoft, of een andere derdedienst gebruiken om een model van vormgegevens tot stand te brengen.

Deze zelfstudie gebruikt de MySQL-database als bron voor het maken van een formuliergegevensmodel. Maak een **lensschema** in de database en voeg een **aanvrager** tabel toe aan het schema op basis van de velden die beschikbaar zijn in het adaptieve formulier.

![Voorbeeldgegevens mysql](assets/sample_data_mysql.png)

U kunt de volgende verklaring gebruiken DDL om de **aanvrager** lijst in gegevensbestand tot stand te brengen.

```sql
CREATE TABLE `applicant` (
   `name` varchar(45) DEFAULT NULL,
   `address` varchar(45) DEFAULT NULL,
   `phonenumber` int(11) NOT NULL,
   `email` varchar(45) DEFAULT NULL,
   `occupation` varchar(45) DEFAULT NULL,
   `annualsalary` varchar(45) DEFAULT NULL,
   `familymembers` int(11) DEFAULT NULL,
   PRIMARY KEY (`phonenumber`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Als u een XSD-schema gebruikt als formuliermodel voor het uitvoeren van de use cases, maakt u een XSD-bestand met de volgende tekst:

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="http://adobe.com/sample.xsd"
                    xmlns="http://adobe.com/sample.xsd"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema">

<xs:element name="sample" type="SampleType"/>

  <xs:complexType name="SampleType">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
   <xs:element name="address" type="xs:string"/>
   <xs:element name="phonenumber" type="xs:int"/>
   <xs:element name="email" type="xs:string"/>
   <xs:element name="occupation" type="xs:string"/>
   <xs:element name="annualsalary" type="xs:string"/>
   <xs:element name="familymembers" type="xs:string"/>
 </xs:sequence>
  </xs:complexType>

  </xs:schema>
```

Of download het XSD-schema naar het lokale bestandssysteem.

Voorbeeld van XSD-schema voor toepassing van een lening

[Bestand ophalen](assets/loanapplication.xsd)

Zie [Aangepaste formulieren maken met XML-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html) voor meer informatie over het gebruik van XSD-schema als het formuliermodel in adaptieve formulieren.

Als u een JSON-schema gebruikt als formuliermodel voor het uitvoeren van de use cases, maakt u een JSON-bestand met de volgende tekst:

```JSON
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "loanapplication": {
            "type": "object",
            "properties": {
                "name": {
                    "type": "string"
                },
                "address": {
                    "type": "string"
                },
    "phonenumber": {
                    "type": "number"
                },
    "email": {
                    "type": "string"
                },
    "occupation": {
                    "type": "string"
                },
    "annualsalary": {
                    "type": "string"
                },
    "familymembers": {
                    "type": "number"
                }
            }
        }
 },
 "type": "object",
    "properties": {
        "employee": {
            "$ref": "#/definitions/loanapplication"
        }
    }
}
```

U kunt het JSON-schema ook downloaden naar het lokale bestandssysteem.

JSON-schema voor voorbeeldtoepassing

[Bestand ophalen](assets/demo_schema.json)

Zie [Aangepaste formulieren maken met het JSON-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html) voor meer informatie over het gebruik van het JSON-schema als het formuliermodel in adaptieve formulieren.

## Aangepaste formulieren genereren zonder gegevensbinding {#generate-adaptive-forms-with-no-data-binding}

Met de [service Automatede form conversion kunt u ](convert-existing-forms-to-adaptive-forms.md) het [voorbeeldaanvraagformulier voor een lening](#sample-adaptive-form) omzetten in een adaptief formulier zonder gegevensbinding. Schakel het selectievakje **[!UICONTROL Generate adaptive form(s) without data bindings]** in om het adaptieve formulier zonder gegevensbinding te genereren.

![Adaptief formulier zonder gegevensbinding](assets/generate_af_without_binding.png)

Nadat u een adaptief formulier zonder gegevensbinding hebt gegenereerd, selecteert u een gegevensbron voor het adaptieve formulier:

* [Database, OData of een service van derden](#sqldatasource)
* [JSON-schema](#jsondatasource)
* [XSD-schema](#xsddatasource)

>[!NOTE]
> Als het adaptieve formulier dat u met de service Automatede form conversion converteert meerdere velden met dezelfde naam bevat, moet u ervoor zorgen dat deze velden zijn gebonden aan gegevensbronentiteiten om een mogelijk gegevensverlies tijdens de verzending te voorkomen.


### Database, OData of een service van derden gebruiken als gegevensbron {#sqldatasource}

Hoofdlettergebruik: U genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert de MYSQL-database als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan formuliergegevensmodelentiteiten en gebruikt de optie **[!UICONTROL Form Data Model Prefill Service]** om veldwaarden vooraf in te vullen. Met de optie **[!UICONTROL Submit using Form Data Model]** kunt u het aangepaste formulier verzenden.

Voordat u het gebruiksgeval uitvoert:

* [MySQL-database configureren als gegevensbron](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [Het formuliergegevensmodel maken](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

Gebaseerd op het gebruiksgeval, creeer **leenApplication** het model van vormgegevens en bind read de dienstargument aan een **[!UICONTROL Literal]** waarde. De letterlijke waarde van het telefoonaantal moet van één van de verslagen zijn die in het **aanvrager** schema van het gegevensbestand MySQL worden gevormd. De diensten gebruiken de waarde als argument om details van de gegevensbron te halen. U kunt [Kenmerk gebruikersprofiel of Aanvraagkenmerk](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) ook selecteren in de vervolgkeuzelijst **[!UICONTROL Binding To]**

![Formuliergegevensmodel configureren](assets/configure_model_object.png)

>[!NOTE]
>
>Zorg ervoor dat u **get** en **insert** services aan het model met formuliergegevens toevoegt, configureer en test de services voordat u het gebruiksgeval uitvoert.

Voer de volgende stappen uit:

1. Selecteer het geconverteerde **voorbeeldaanvraagformulier voor een lening** dat beschikbaar is in de map **[!UICONTROL output]** en tik **[!UICONTROL Properties]**.
1. Tik op de tab **[!UICONTROL Form Model]**, selecteer **[!UICONTROL Form Data Model]** in de vervolgkeuzelijst **[!UICONTROL Select From]** en tik **[!UICONTROL Select Form Data Model]** om het formuliergegevensmodel **load** te selecteren. Tik **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer het **voorbeeldaanvraagformulier voor leningen** en tik **[!UICONTROL Edit]**.
1. Tik op het tabblad **[!UICONTROL Content]** op het configuratiepictogram:

   ![formuliercontainer configureren](assets/configure_form_container.png)

   1. Selecteer in de sectie **[!UICONTROL Basic]** **[!UICONTROL Form Data Model Prefill service]** in de vervolgkeuzelijst **[!UICONTROL Prefill Service]**.

   1. Selecteer in de sectie **[!UICONTROL Submission]** **[!UICONTROL Submit using Form Data Model]** in de vervolgkeuzelijst **[!UICONTROL Submit Action]**.

   1. Selecteer het gegevensmodel met het veld **[!UICONTROL Data Model to submit]**.
   1. Tik ![voltooid pictogram](assets/save_icon.svg) om de eigenschappen op te slaan.

1. Tik op het tekstvak Naam aanvrager en selecteer ![configure icon](assets/configure_icon.svg) (Configure).

   1. Selecteer **Aanvrager** > **Naam** in het veld Bindverwijzing en tik ![Voltooid pictogram](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)** en **Nee. van afhankelijke familieleden** gebieden met de modelentiteiten van vormgegevens.

   ![Bindverwijzingen](assets/bind_references.png)

1. Tik op **[!UICONTROL Preview]** om de vooraf ingevulde aangepaste waarden voor formuliervelden weer te geven.
1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De veldwaarden worden verzonden naar de MySQL-database. U kunt de **aanvrager** lijst in het gegevensbestand verfrissen om de bijgewerkte waarden in de lijst te bekijken.

**Hoofdlettergebruik:** u genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert de MYSQL-database als gegevensbron. U bindt de aangepaste formuliervelden met de regeleditor aan het vooraf invullen van veldwaarden. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Voer de volgende stappen uit om [regeleditor](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) te gebruiken om de service van het formuliergegevensmodel aan te roepen om velden en vooraf ingevulde waarden in een adaptieve vorm te binden:

1. Selecteer het **voorbeeldaanvraagformulier voor een lening** in de map **[!UICONTROL output]** en tik **[!UICONTROL Edit]**.
1. Tik op het tabblad **[!UICONTROL Content]** op het configuratiepictogram:

   ![formuliercontainer configureren](assets/configure_form_container.png)

   Selecteer in de sectie **[!UICONTROL Basic]** **[!UICONTROL Form Data Model Prefill service]** in de vervolgkeuzelijst **[!UICONTROL Prefill Service]**.

1. Tik op het tekstvak **[!UICONTROL Applicant Name]** en tik **[!UICONTROL Edit Rules]**.

   ![Regels bewerken om gegevensbinding te maken](assets/edit_rules_bind_reference.png)

1. Tik **[!UICONTROL Create]** op de pagina van de Redacteur van de Regel.
1. Op de pagina **[!UICONTROL Rule Editor]**:

   1. Selecteer een status voor het tekstvak Naam aanvrager. Bijvoorbeeld **[!UICONTROL is initialized]**, wat resulteert in uitvoering van **[!UICONTROL Then]** voorwaarde wanneer u de vorm in **[!UICONTROL Preview]** wijze teruggeeft.

   1. Selecteer in de sectie **[!UICONTROL Then]** **[!UICONTROL Invoke Service]** in de vervolgkeuzelijst **[!UICONTROL Select Action]**. Alle services op uw Forms-instantie worden weergegeven in de vervolgkeuzelijst.

   1. Selecteer een **[!UICONTROL Get]**-service in de sectie waarin de modellen met formuliergegevens worden vermeld. In het veld Invoer wordt **phonenumber** weergegeven. Dit is de primaire sleutel die is gedefinieerd voor het **application** gegevensmodel. Het systeem haalt de waarden in het adaptieve formulier voor velden op in de sectie Uitvoer op basis van dit veld en vult deze waarden vooraf in.

   1. Maak een binding voor de adaptieve formuliervelden met de entiteiten van het formuliergegevensmodel met de sectie Uitvoer. Verbind bijvoorbeeld **[!UICONTROL Applicant Name]** adaptief formulierveld met de entiteit **name**.

   1. Tik op **[!UICONTROL Done]**. Tik **[!UICONTROL Done]** nogmaals op de pagina van de Redacteur van de Regel.

   ![Regeleditor om verwijzingen te binden](assets/rule_editor_bind_references.png)

1. Tik op **[!UICONTROL Preview]** om de vooraf ingevulde aangepaste waarden voor formuliervelden weer te geven.

   >[!NOTE]
   >
   >Zorg ervoor dat de eigenschap **[!UICONTROL Return Array]** is ingesteld op OFF voor de service-eigenschap **get** in het formuliergegevensmodel dat is gekoppeld aan het adaptieve formulier.

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### JSON-schema gebruiken als gegevensbron {#jsondatasource}

**Hoofdlettergebruik:** u genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert het JSON-schema als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan het JSON-schema en gebruikt de optie **Voorvertonen met gegevens** om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Controleer voordat u het gebruiksgeval uitvoert of:

* [een geldig JSON-schema dat voldoet aan de JSON-schemastructuur](#prepare-data-for-form-model)
* [een adaptief formulier zonder gegevensbinding](#generate-adaptive-forms-with-no-data-binding)

Voer de volgende stappen uit:

1. Selecteer het geconverteerde **voorbeeldaanvraagformulier voor een lening** beschikbaar in de map **output** en tik **[!UICONTROL Properties]**.
1. Tik op de tab **[!UICONTROL Form Model]**, selecteer **[!UICONTROL Schema]** in de vervolgkeuzelijst **[!UICONTROL Select From]** en tik **[!UICONTROL Select Schema]** om het schema **demo.schema JSON** te uploaden dat is opgeslagen op het lokale bestandssysteem. Tik **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer het **voorbeeldaanvraagformulier voor leningen** en tik **[!UICONTROL Edit]**.
1. Tik op het tekstvak Naam aanvrager en selecteer ![configure icon](assets/configure_icon.svg) (Configure).

   Selecteer **Aanvrager** > **Naam** in het veld Bindverwijzing en tik ![Voltooid pictogram](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)** en **Nee. van afhankelijke familieleden** gebieden met de JSON schemaentiteiten.

1. Selecteer nogmaals het geconverteerde **voorbeeldformulier voor de toepassing van een lening** in de map **[!UICONTROL output]** en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/json_data_file.txt)</br>

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### XSD-schema gebruiken als gegevensbron {#xsddatasource}

**Hoofdlettergebruik:** u genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert het XSD-schema als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan het XSD-schema en gebruikt **Voorvertoning met gegevens** om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Controleer voordat u het gebruiksgeval uitvoert of:

* [een geldig XSD-schema dat compatibel is met de XML-schemastructuur](#prepare-data-for-form-model)
* [een adaptief formulier zonder gegevensbinding](#generate-adaptive-forms-with-no-data-binding)

Voer de volgende stappen uit:

1. Selecteer het geconverteerde **voorbeeldaanvraagformulier voor een lening** dat beschikbaar is in de map **[!UICONTROL output]** en tik **[!UICONTROL Properties]**.
1. Tik op het tabblad **[!UICONTROL Form Model]**, selecteer **[!UICONTROL Schema]** in de vervolgkeuzelijst **[!UICONTROL Select From]** en tik **[!UICONTROL Select Schema]** om het **lende-toepassings** XSD-schema te uploaden dat is opgeslagen op het lokale bestandssysteem. Selecteer basiselement voor het XSD-schema en tik **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer het **voorbeeldaanvraagformulier voor leningen** en tik **[!UICONTROL Edit]**.
1. Tik op het tekstvak Naam aanvrager en selecteer ![configure icon](assets/configure_icon.svg) (Configure).
Selecteer **Aanvrager** > **Naam** in het veld Bindverwijzing en tik ![Gereed pictogram](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)** en **Nee. van afhankelijke familieleden** gebieden met de XSD schemaentiteiten.

1. Selecteer nogmaals het geconverteerde **voorbeeldformulier voor de toepassing van de lening** beschikbaar in de map **output** en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/loan-application-data-xml-data.zip)</br>


1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Aangepaste formulieren genereren met JSON-binding {#generate-adaptive-forms-with-json-binding}

Met de [service Automatede form conversion kunt u ](convert-existing-forms-to-adaptive-forms.md) het [voorbeeldformulier voor de toepassing van een lening](#sample-adaptive-form) converteren naar een adaptief formulier met gegevensbinding. Zorg ervoor dat u het selectievakje **[!UICONTROL Generate adaptive form(s) without data bindings]** niet inschakelt tijdens het genereren van het adaptieve formulier.

![Aangepaste vorm met JSON-binding](assets/generate_af_with_data_bindings.png)

### JSON-schema gebruiken als gegevensbron {#jsonwithdatabinding}

**Hoofdlettergebruik:** u genereert een adaptief formulier met JSON-gegevensbinding via de service Automatede form conversion. De Prefill-service en het verzenden van formulieren werken naadloos. U hebt geen configuratiestappen nodig.

Zorg ervoor dat u [een adaptief formulier hebt met gegevensbinding](#generate-adaptive-forms-with-json-binding) voordat u het gebruiksgeval uitvoert.

Voer de volgende stappen uit:

1. Selecteer nogmaals het geconverteerde **voorbeeldformulier voor de toepassing van een lening** in de map **[!UICONTROL output]** en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/loan_application_data_source_json_data_binding.txt)</br>

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Verzonden aangepaste JSON-formuliergegevens converteren naar XML-indeling {#convert-submitted-adaptive-form-data-to-xml}

Wanneer u waarden invoert in adaptieve formuliervelden en deze verzendt, zijn de gegevens beschikbaar in JSON-indeling in de crx-repository. U kunt de indeling van JSON-gegevens omzetten in XML met de API [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) of de volgende voorbeeldcode:

```
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;
import org.apache.sling.commons.json.xml.XML;
 
public class ConversionUtils {
 
    public static String jsonToXML(String jsonString) throws JSONException {
        //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
        //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
        //Note: Need to extract boundData part before converting to XML
        return XML.toString(new JSONObject(jsonString));
    }
}
```

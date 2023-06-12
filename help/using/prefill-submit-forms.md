---
title: Aanbevolen vooraf ingevulde gegevens gebaseerd op gegevensbron en workflows toevoegen voor adaptieve formulieren
seo-title: Prefill and submit options for adaptive forms
description: Workflows op basis van gegevensbron vooraf invullen en verzenden voor adaptieve formulieren die zijn gegenereerd met de service Automatede form conversion.
seo-description: Data-source based prefill and submit workflows for adaptive forms generated using Automated Forms Conversion Service.
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
exl-id: 5deef8f5-5098-47c1-b696-b2db59e92931
source-git-commit: 298d6c0641d7b416edb5b2bcd5fec0232f01f4c7
workflow-type: tm+mt
source-wordcount: '2437'
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
    <p><strong>Optie 1</strong>: U selecteert formuliergegevensmodel, OData of een andere service van derden als gegevensbron. U <a href="#generate-adaptive-forms-with-no-data-binding">een adaptief formulier zonder gegevensbinding genereren</a> het gebruiken van de dienst van de Automatede form conversion. U bindt de adaptieve formuliervelden handmatig aan entiteiten van het formuliergegevensmodel en gebruikt de optie Vooraf ingevulde service formuliergegevensmodel om veldwaarden vooraf in te vullen. Met de optie Verzenden met gebruik van het formuliergegevensmodel kunt u het aangepaste formulier verzenden.</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>Optie 2</strong>: U selecteert formuliergegevensmodel, OData of een andere service van derden als gegevensbron. U <a href="#generate-adaptive-forms-with-no-data-binding">een adaptief formulier zonder gegevensbinding genereren</a> het gebruiken van de dienst van de Automatede form conversion. U bindt de aangepaste formuliervelden met de regeleditor aan het vooraf invullen van veldwaarden. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>Zie voor stapsgewijze instructies om deze workflows uit te voeren <a href="#sqldatasource">Gebruik gegevensbestand, OData, of om het even welke derdedienst als gegevensbron.</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON Schema</p></td> 
   <td> 
    <p>U selecteert JSON-schema als gegevensbron. Gebaseerd op de geselecteerde gegevensbron:</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Optie 1</strong>: U <a href="#generate-adaptive-forms-with-no-data-binding">een adaptief formulier zonder gegevensbinding genereren</a> het gebruiken van de dienst van de Automatede form conversion en vormen het schema JSON als gegevensbron. U bindt de adaptieve formuliervelden handmatig aan het JSON-schema en <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">gebruik om het even welke gesteunde protocollen</a> om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Voor stapsgewijze instructies voor het uitvoeren van de workflows raadpleegt u <a href="#jsondatasource">Gebruik het JSON-schema als gegevensbron.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Optie 2</strong>: U <a href="#generate-adaptive-forms-with-json-binding">een adaptief formulier genereren met JSON-gegevensbinding</a> het gebruiken van de dienst van de Automatede form conversion. De Prefill-service en het verzenden van formulieren werken naadloos. U hebt geen configuratiestappen nodig.</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>Voor stapsgewijze instructies voor het uitvoeren van de workflows raadpleegt u <a href="#jsonwithdatabinding">Gebruik het JSON-schema als gegevensbron.</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD-schema</p></td> 
   <td> 
    <p>U selecteert XSD-schema als gegevensbron. Op basis van de geselecteerde gegevensbron kunt u <a href="#generate-adaptive-forms-with-no-data-binding">een adaptief formulier zonder gegevensbinding genereren</a> het gebruiken van de dienst van de Automatede form conversion en vormen XSD schema als gegevensbron. U koppelt de adaptieve formuliervelden handmatig aan het XSD-schema en <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">gebruik om het even welke gesteunde protocollen</a> om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Voor stapsgewijze instructies voor het uitvoeren van de workflows raadpleegt u <a href="#xsddatasource">Gebruik XSD-schema als gegevensbron.</a></p>
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

* Een [AEM](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* Configureren [De dienst van de automatede form conversion op de AEM auteursinstantie](configure-service.md)

## Monster van adaptief formulier {#sample-adaptive-form}

Download het volgende voorbeeldbestand voor het PDF om de gebruiksgevallen voor het vooraf invullen van veldwaarden in een adaptief formulier uit te voeren en deze naar de gegevensbron te verzenden.

Voorbeeldformulier voor het aanvragen van een lening

[Bestand ophalen](assets/sample_loan_application_form.pdf)

Het PDF-bestand fungeert als invoer voor de service Automatede form conversion. De service converteert dit bestand naar een adaptief formulier. In de volgende afbeelding wordt de voorbeeldtoepassing met een PDF-indeling weergegeven.

![aanvraagformulier voor een voorbeeldlening](assets/sample_form_new.png)

## Gegevens voorbereiden voor formuliermodel {#prepare-data-for-form-model}

Met AEM Forms Data Integration kunt u verschillende gegevensbronnen configureren en verbinden. Nadat u een adaptief formulier hebt gegenereerd met behulp van het conversieproces, kunt u het formuliermodel definiëren op basis van een formuliergegevensmodel, XSD of een JSON-schema. U kunt een database, Microsoft Dynamics of een andere service van derden gebruiken om een formuliergegevensmodel te maken.

Deze zelfstudie gebruikt de MySQL-database als bron voor het maken van een formuliergegevensmodel. Een **lening** in de database en voeg een **aanvrager** tabel naar het schema op basis van de velden die beschikbaar zijn in het adaptieve formulier.

![Voorbeeldgegevens mysql](assets/sample_data_mysql.png)

U kunt de volgende verklaring gebruiken DDL om tot de **aanvrager** tabel in de database.

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

Zie voor meer informatie over het gebruik van XSD-schema als formuliermodel in adaptieve formulieren [Aangepaste formulieren maken met XML-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html).

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

Ga voor meer informatie over het gebruik van JSON-schema als het formuliermodel in adaptieve formulieren naar [Aangepaste formulieren maken met JSON-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html).

## Aangepaste formulieren zonder gegevensbinding genereren {#generate-adaptive-forms-with-no-data-binding}

Gebruik de [Omzetten van automatede form conversion](convert-existing-forms-to-adaptive-forms.md) de [aanvraagformulier voor een voorbeeldlening](#sample-adaptive-form) op een adaptief formulier zonder gegevensbinding. Zorg ervoor dat u de **[!UICONTROL Generate adaptive form(s) without data bindings]** Schakel het selectievakje in om het adaptieve formulier zonder gegevensbinding te genereren.

![Adaptief formulier zonder gegevensbinding](assets/generate_af_without_binding.png)

Nadat u een adaptief formulier zonder gegevensbinding hebt gegenereerd, selecteert u een gegevensbron voor het adaptieve formulier:

* [Database, OData of een service van derden](#sqldatasource)
* [JSON-schema](#jsondatasource)
* [XSD-schema](#xsddatasource)

>[!NOTE]
> Als het adaptieve formulier dat u met de service Automatede form conversion converteert meerdere velden met dezelfde naam bevat, moet u ervoor zorgen dat deze velden zijn gebonden aan gegevensbronentiteiten om een mogelijk gegevensverlies tijdens de verzending te voorkomen.
>

### Gebruik gegevensbestand, OData, of om het even welke derdedienst als gegevensbron {#sqldatasource}

Hoofdlettergebruik: U genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert de MYSQL-database als gegevensbron. U bindt de aangepaste formuliervelden handmatig aan formuliergegevensmodelentiteiten en gebruikt de opdracht **[!UICONTROL Form Data Model Prefill Service]** gebruiken om veldwaarden vooraf in te vullen. U gebruikt de **[!UICONTROL Submit using Form Data Model]** om het adaptieve formulier in te dienen.

Voordat u het gebruiksgeval uitvoert:

* [MySQL-database configureren als gegevensbron](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [Het formuliergegevensmodel maken](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

Maak op basis van het gebruiksgeval de **lening** formuliergegevensmodel en bind read service argument to a **[!UICONTROL Literal]** waarde. De letterlijke waarde van het telefoonaantal moet van één van de verslagen zijn die in worden gevormd **aanvrager** schema van de MySQL-database. De diensten gebruiken de waarde als argument om details van de gegevensbron te halen. U kunt ook [Kenmerk gebruikersprofiel of aanvraagkenmerk](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) van de **[!UICONTROL Binding To]** vervolgkeuzelijst

![Formuliergegevensmodel configureren](assets/configure_model_object.png)

>[!NOTE]
>
>Zorg ervoor dat u **get** en **insert** de diensten aan het model van vormgegevens, vormen, en testen de diensten alvorens het gebruiksgeval uit te voeren.

Voer de volgende stappen uit:

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **[!UICONTROL output]** map en tik **[!UICONTROL Properties]**.
1. Tik op de knop **[!UICONTROL Form Model]** tab, selecteert u **[!UICONTROL Form Data Model]** van de **[!UICONTROL Select From]** vervolgkeuzelijst en tikken **[!UICONTROL Select Form Data Model]** om de **lening** formuliergegevensmodel. Tikken **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer **aanvraagformulier voor een voorbeeldlening** en tikken **[!UICONTROL Edit]**.
1. In de **[!UICONTROL Content]** tikt u op het configuratiepictogram:

   ![formuliercontainer configureren](assets/configure_form_container.png)

   1. In de **[!UICONTROL Basic]** sectie, selecteert u **[!UICONTROL Form Data Model Prefill service]** van de **[!UICONTROL Prefill Service]** vervolgkeuzelijst.

   1. In de **[!UICONTROL Submission]** sectie, selecteert u **[!UICONTROL Submit using Form Data Model]** van de **[!UICONTROL Submit Action]** vervolgkeuzelijst.

   1. Selecteer het gegevensmodel met de **[!UICONTROL Data Model to submit]** veld.
   1. Tikken ![pictogram klaar](assets/save_icon.svg) om de eigenschappen op te slaan.

1. Tik op het tekstvak Naam aanvrager en selecteer ![Configuratiepictogram](assets/configure_icon.svg) (Configureren).

   1. Selecteer in het veld Bindverwijzing de optie **Aanvrager** > **Naam** en tikken ![pictogram klaar](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor de **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)**, en **Nee. van afhankelijke gezinsleden** velden met entiteiten van het formuliergegevensmodel.

   ![Bindverwijzingen](assets/bind_references.png)

1. Tikken **[!UICONTROL Preview]** om de vooraf ingevulde aangepaste waarden voor formuliervelden weer te geven.
1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De veldwaarden worden verzonden naar de MySQL-database. U kunt de **aanvrager** in de database om de bijgewerkte waarden in de tabel weer te geven.

**Hoofdlettergebruik:** U genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert de MYSQL-database als gegevensbron. U bindt de aangepaste formuliervelden met de regeleditor aan het vooraf invullen van veldwaarden. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Voer de volgende stappen uit om te gebruiken [regeleditor](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) om de service van het formuliergegevensmodel aan te roepen om velden en vooraf ingevulde waarden in een adaptief formulier te binden:

1. Selecteer **aanvraagformulier voor een voorbeeldlening** in de **[!UICONTROL output]** map en tik **[!UICONTROL Edit]**.
1. In de **[!UICONTROL Content]** tikt u op het configuratiepictogram:

   ![formuliercontainer configureren](assets/configure_form_container.png)

   In de **[!UICONTROL Basic]** sectie, selecteert u **[!UICONTROL Form Data Model Prefill service]** van de **[!UICONTROL Prefill Service]** vervolgkeuzelijst.

1. Tik op de knop **[!UICONTROL Applicant Name]** tekstvak en tikken **[!UICONTROL Edit Rules]**.

   ![Regels bewerken om gegevensbinding te maken](assets/edit_rules_bind_reference.png)

1. Tikken **[!UICONTROL Create]** op de pagina Regeleditor.
1. Op de **[!UICONTROL Rule Editor]** pagina:

   1. Selecteer een status voor het tekstvak Naam aanvrager. Bijvoorbeeld: **[!UICONTROL is initialized]**, hetgeen resulteert in de uitvoering van de **[!UICONTROL Then]** voorwaarde wanneer u het formulier weergeeft in **[!UICONTROL Preview]** in.

   1. In de **[!UICONTROL Then]** sectie, selecteert u **[!UICONTROL Invoke Service]** van de **[!UICONTROL Select Action]** vervolgkeuzelijst. Alle services op uw Forms-instantie worden weergegeven in de vervolgkeuzelijst.

   1. Selecteer een **[!UICONTROL Get]** vanuit de sectie met de formuliergegevensmodellen. Het veld Invoer wordt weergegeven **phonenumber**, die de primaire sleutel is die voor de **aanvrager** gegevensmodel. Het systeem haalt de waarden in het adaptieve formulier voor velden op in de sectie Uitvoer op basis van dit veld en vult deze waarden vooraf in.

   1. Maak een binding voor de adaptieve formuliervelden met de entiteiten van het formuliergegevensmodel met de sectie Uitvoer. Bind bijvoorbeeld **[!UICONTROL Applicant Name]** adaptief formulierveld met de **name** entiteit.

   1. Tik op **[!UICONTROL Done]**. Tikken **[!UICONTROL Done]** opnieuw op de pagina van de Redacteur van de Regel.

   ![Regeleditor om verwijzingen te binden](assets/rule_editor_bind_references.png)

1. Tikken **[!UICONTROL Preview]** om de vooraf ingevulde aangepaste waarden voor formuliervelden weer te geven.

   >[!NOTE]
   >
   >Zorg ervoor dat de **[!UICONTROL Return Array]** Eigenschap is ingesteld op UIT voor de **get** service-eigenschap in het formuliergegevensmodel dat aan het adaptieve formulier is gekoppeld.

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### JSON-schema gebruiken als gegevensbron {#jsondatasource}

**Hoofdlettergebruik:** U genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert het JSON-schema als gegevensbron. U bindt de aangepaste formuliervelden handmatig aan het JSON-schema en gebruikt de opdracht **Voorvertonen met gegevens** gebruiken om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Controleer voordat u het gebruiksgeval uitvoert of:

* [een geldig JSON-schema dat voldoet aan de JSON-schemastructuur](#prepare-data-for-form-model)
* [een adaptief formulier zonder gegevensbinding](#generate-adaptive-forms-with-no-data-binding)

Voer de volgende stappen uit:

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **output** map en tik **[!UICONTROL Properties]**.
1. Tik op de knop **[!UICONTROL Form Model]** tab, selecteert u **[!UICONTROL Schema]** van de **[!UICONTROL Select From]** vervolgkeuzelijst en tikken **[!UICONTROL Select Schema]** om het **demo.schema JSON** schema opgeslagen op het lokale bestandssysteem. Tikken **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer **aanvraagformulier voor een voorbeeldlening** en tikken **[!UICONTROL Edit]**.
1. Tik op het tekstvak Naam aanvrager en selecteer ![Configuratiepictogram](assets/configure_icon.svg) (Configureren).

   Selecteer in het veld Bindverwijzing de optie **Aanvrager** > **Naam** en tikken ![pictogram klaar](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor de **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)**, en **Nee. van afhankelijke gezinsleden** velden met de JSON-schema-entiteiten.

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **[!UICONTROL output]** map opnieuw en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/json_data_file.txt)</br>

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### XSD-schema gebruiken als gegevensbron {#xsddatasource}

**Hoofdlettergebruik:** U genereert een adaptief formulier zonder gegevensbinding met de service Automatede form conversion en configureert XSD-schema als gegevensbron. U bindt de aangepaste formuliervelden handmatig aan het XSD-schema en gebruikt de opdracht **Voorvertonen met gegevens** om veldwaarden vooraf in te vullen. Wijzig, indien nodig, de veldwaarden en verzend gegevens naar de crx-repository.

Controleer voordat u het gebruiksgeval uitvoert of:

* [een geldig XSD-schema dat compatibel is met de XML-schemastructuur](#prepare-data-for-form-model)
* [een adaptief formulier zonder gegevensbinding](#generate-adaptive-forms-with-no-data-binding)

Voer de volgende stappen uit:

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **[!UICONTROL output]** map en tik **[!UICONTROL Properties]**.
1. Tik op de knop **[!UICONTROL Form Model]** tab, selecteert u **[!UICONTROL Schema]** van de **[!UICONTROL Select From]** vervolgkeuzelijst en tikken **[!UICONTROL Select Schema]** om het **lening** XSD-schema opgeslagen in het lokale bestandssysteem. Selecteer basiselement voor het XSD-schema en tik op **[!UICONTROL Save & Close]** om het formulier op te slaan.
1. Selecteer **aanvraagformulier voor een voorbeeldlening** en tikken **[!UICONTROL Edit]**.
1. Tik op het tekstvak Naam aanvrager en selecteer ![Configuratiepictogram](assets/configure_icon.svg) (Configureren).
Selecteer in het veld Bindverwijzing de optie **Aanvrager** > **Naam** en tikken ![Gereed pictogram](assets/save_icon.svg) om de eigenschappen op te slaan. Maak op dezelfde manier een gegevensbinding voor de **Adres**, **Telefoonnummer**, **E-mail**, **Beroep**, **Jaarloon (in dollars)**, en **Nee. van afhankelijke gezinsleden** velden met de XSD-schema-entiteiten.

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **output** map opnieuw en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/loan-application-data-xml-data.zip)</br>


1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Aangepaste formulieren genereren met JSON-binding {#generate-adaptive-forms-with-json-binding}

Gebruik de [Omzetten van automatede form conversion](convert-existing-forms-to-adaptive-forms.md) de [aanvraagformulier voor een voorbeeldlening](#sample-adaptive-form) in een adaptief formulier met gegevensbinding. Zorg ervoor dat u de optie **[!UICONTROL Generate adaptive form(s) without data bindings]** selectievakje tijdens het genereren van het adaptieve formulier.

![Aangepaste vorm met JSON-binding](assets/generate_af_with_data_bindings.png)

### JSON-schema gebruiken als gegevensbron {#jsonwithdatabinding}

**Hoofdlettergebruik:** U genereert een adaptief formulier met JSON-gegevensbinding via de service Automatede form conversion. De Prefill-service en het verzenden van formulieren werken naadloos. U hebt geen configuratiestappen nodig.

Controleer voordat u het gebruiksgeval uitvoert of [een adaptief formulier met gegevensbinding](#generate-adaptive-forms-with-json-binding).

Voer de volgende stappen uit:

1. Omgezette selecteren **aanvraagformulier voor een voorbeeldlening** beschikbaar in **[!UICONTROL output]** map opnieuw en selecteer **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Voorbeeldgegevensbestand downloaden</br>

   [Bestand ophalen](assets/loan_application_data_source_json_data_binding.txt)</br>

1. Wijzig, indien nodig, de veldwaarden en verzend het adaptieve formulier. De ingediende gegevens zijn beschikbaar op de volgende locatie in de crx-repository:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Verzonden JSON-formuliergegevens converteren naar XML-indeling {#convert-submitted-adaptive-form-data-to-xml}

Wanneer u waarden invoert in adaptieve formuliervelden en deze verzendt, zijn de gegevens beschikbaar in JSON-indeling in de crx-repository. U kunt de indeling van JSON-gegevens omzetten in XML met behulp van [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) API of de volgende voorbeeldcode:

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

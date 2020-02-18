---
title: Het standaardmetamodel uitbreiden
seo-title: Het standaardmetamodel uitbreiden
description: Het standaardmetamodel uitbreiden om patronen, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service voor automatische formulierconversie wordt uitgevoerd.
seo-description: Het standaardmetamodel uitbreiden om patronen, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service voor automatische formulierconversie wordt uitgevoerd.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: 5d4dba8fea7439b991a7a15872e6f4ed48156ac9

---


# Het standaardmetamodel uitbreiden {#extend-the-default-meta-model}

Met de service Automated Forms Conversion kunt u formulierobjecten herkennen en uitnemen van bronformulieren. Met Semantic-mapper kan de service bepalen hoe de geëxtraheerde objecten in een adaptieve vorm worden weergegeven. Een bronformulier kan bijvoorbeeld vele verschillende soorten representaties van een datum hebben. Met de semantische mapfunctie kunt u alle weergaven van datumformulierobjecten van het bronformulier toewijzen aan datumcomponent van de adaptieve formulieren. Met Semantic mapper kan de service ook validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen vooraf configureren en toepassen op adaptieve formuliercomponenten tijdens conversie.

![](assets/meta-model.gif)

Meta-model is een JSON-schema. Voordat u begint met meta-model, moet u controleren of u goed bent omgedraaid met JSON. U moet ervaring hebben met het maken, bewerken en lezen van gegevens die zijn opgeslagen in de JSON-indeling.

## Standaardmetamodel {#default-meta-model}

De geautomatiseerde dienst van de Omzetting van Vormen heeft een standaardmetamodel. Het is een JSON-schema en bevindt zich in Adobe Cloud met andere componenten van de service Automated Forms Conversion. U kunt een kopie van het metamodel vinden op uw lokale AEM-server op:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json.

Het schema van meta-model wordt afgeleid uit schemaentiteiten in https://schema.org/docs/schemas.html. Het heeft Persoon, PostalAddress, LocalBusiness, en meer entiteiten zoals die op https://schema.org worden bepaald. Elke entiteit van het metamodel volgt het JSON-schemaobjecttype. De volgende code vertegenwoordigt een structuur van een metamodel van het steekproef:

```
   "Entity": {
      "id": "Entity",
      "properties": {
        "name": {
          "type": "string"
        },

        "description": {
          "type": "string",
          "description": "Description of the item"
        }
      }
    }
```

## Het standaardmetamodel downloaden {#download-the-default-meta-model}

Voer de volgende stappen uit om het standaard meta-model aan het lokale dossiersysteem te downloaden:

1. Meld u aan bij de instantie AEM Forms.
1. Navigeer naar de map **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]** .
1. Selecteer het **[!UICONTROL global.schema.json]** bestand en tik op **[!UICONTROL Download]**. Er wordt een dialoogvenster voor downloaden weergegeven. Selecteer de **[!UICONTROL Download asset(s) as binary files]** optie. Tik **[!UICONTROL Download]**. Er wordt een archief gedownload.

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## Het metamodel begrijpen {#understanding-the-meta-model}

Een metamodel verwijst naar een JSON-schemabestand dat entiteiten bevat. Alle entiteiten in het JSON-schemabestand bevatten een naam en een id. Elke entiteit kan meerdere eigenschappen bevatten. De entiteiten en de eigenschappen kunnen variëren op basis van het domein. U kunt een schemabestand met trefwoorden en veldconfiguraties uitbreiden om schema-eigenschappen toe te wijzen aan adaptieve formuliercomponenten.

```
"Event": {
      "id": "Eventid",
      "allOf": [
        {
          "$ref": "#Entity"
        },
        {
          "properties": {
            "startDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the start date and time of the event in ISO 8601 date format."
            },
            "endDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the end date and time of the event in ISO 8601 date format."
            },
            "location": {
              "$ref": "#PostalAddress",
              "description": "Specify the location of the event."
            }
          }
        }
      ]
    }
```

In dit voorbeeld staat **Event** voor de naam van een entiteit met een waarde voor **id** als **Eventid**. De gebeurtenisentiteit bevat meerdere eigenschappen:

* startDate
* endDate
* locatie

De **constructie allOf** in het meta-model maakt overerving tussen entiteiten mogelijk.

Elke eigenschap kan verder het volgende bevatten:

* [Eigenschappen van JSON-schema](#jsonschemaproperties)
* [Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden](#keywordsearch)
* [Aanvullende eigenschappen](#additionalproperties)

![Eigenschappen van het metamodel](assets/meta_model_elements.gif)

Op basis van de trefwoorden waarnaar wordt verwezen met **name:affKeyword**, voert de conversieservice een zoekbewerking uit op de bronformuliervelden. De conversieservice past de eigenschappen van het JSON-schema en aanvullende eigenschappen toe op de velden die aan de zoekcriteria voldoen.

In dit voorbeeld zoekt de conversieservice naar de telefoon, de telefoon, de mobiele telefoon, de werktelefoon, de thuistelefoon, het telefoonnummer, het telefoonnummer en het telefoonnummer van de trefwoorden in het bronformulier. Op basis van de velden die deze trefwoorden bevatten, past de conversieservice het type, het patroon en de naam:afProperties toe op de adaptieve formuliervelden na de conversie.

### JSON-schemaeigenschappen voor gegenereerde adaptieve formuliervelden {#jsonschemaproperties}

Het metamodel ondersteunt de volgende gemeenschappelijke eigenschappen van het JSON-schema voor adaptieve formuliervelden die worden gegenereerd met de service Automated Forms Conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>title</p></td> 
   <td> 
    <p>De tekst die in de eigenschap title in een metamodel wordt genoemd, fungeert als trefwoord voor zoekacties in de gegenereerde adaptieve formuliervelden. U kunt bijvoorbeeld het label van een adaptief formulierveld wijzigen. Zie Het label van een formulierveld <strong></strong> wijzigen in voorbeelden van <a href="#custommetamodelexamples">aangepaste metamodellen voor meer informatie.</a></p> </td> 
  </tr>
  <td><p>beschrijving</p></td> 
   <td> 
    <p>Met de eigenschap description wordt de Help-tekst voor het gegenereerde adaptieve formulierveld ingesteld. Zie Help-tekst <strong>toevoegen aan een formulierveld</strong> in voorbeelden van het <a href="#custommetamodelexamples">aangepaste metamodel voor meer informatie.</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>De eigenschap type definieert het gegevenstype voor het gegenereerde adaptieve formulierveld. De mogelijke waarden voor de eigenschap title zijn:</p>
    <ul> 
     <li>tekenreeks: Hiermee wordt een adaptief formulierveld van het tekstgegevenstype gegenereerd.</li> 
     <li>getal: Hiermee genereert u een adaptief formulierveld met een numeriek gegevenstype.</li>
     <li>integer: Genereert een adaptief formulierveld van een numeriek gegevenstype met subtype ingesteld op geheel getal.</li>
     <li>Booleaans: Genereert een schakeloptie voor adaptieve formulieren.</li>
     </ul><p>Zie <strong>Het type van een formulierveld</strong> wijzigen in <a href="#custommetamodelexamples">aangepaste metamodelvoorbeelden voor meer informatie over het gebruik van de eigenschap type in een metamodel.</a></p></td> 
  </tr>
  <td><p>pattern</p></td> 
   <td> 
    <p>De eigenschap pattern beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een reguliere expressie. De volgende code in het metamodel beperkt bijvoorbeeld de waarde voor het gegenereerde adaptieve formulierveld tot tien cijfers:<br>"patroon": "/\\d{10}/"<br>Op dezelfde manier beperkt de volgende code in het metamodel de waarde van een gebied tot een specifieke datumformaat.<br> "patroon": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>De eigenschap format beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een benoemd patroon in plaats van een reguliere expressie. De mogelijke waarden voor de opmaakeigenschap zijn:<ul><li>e-mail: Hiermee genereert u een adaptieve e-mailformuliercomponent.</li><li>hostnaam: Hiermee genereert u een adaptief tekstvak-formuliercomponent.</li></ul>Zie <strong>De indeling van een formulierveld</strong> wijzigen in <a href="#custommetamodelexamples">Aangepaste metamodelvoorbeelden voor meer informatie over het gebruik van de indelingseigenschap in een metamodel.</a></p> </td> 
  </tr>
  <td><p>enum en enumNames</p></td> 
   <td> 
    <p>De eigenschappen enum en enumNames beperken de waarden van drop-down, controledoos, of radioknoopgebieden tot een vaste reeks. Waarden die in enumNames worden vermeld, worden weergegeven in de gebruikersinterface. De waarden die worden vermeld gebruikend het enum bezit worden gebruikt voor berekening.<br>Zie Een formulierveld <strong>converteren naar meerkeuzevakken in het adaptieve formulier</strong>, een tekstveld <strong>converteren naar vervolgkeuzelijst in het adaptieve formulier</strong>en aanvullende opties <strong>toevoegen aan de vervolgkeuzelijst</strong> in voorbeelden van <a href="#custommetamodelexamples">aangepaste metamodellen.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden {#keywordsearch}

De geautomatiseerde dienst van de Omzetting van Vormen voert een sleutelwoordonderzoek op het bronvorm tijdens omzetting uit. Nadat de velden die aan de zoekcriteria voldoen, zijn gefilterd, past de conversieservice de eigenschappen die voor die velden in het metamodel zijn gedefinieerd toe op de gegenereerde adaptieve formuliervelden.

Er wordt naar trefwoorden verwezen met de eigenschap **name:affKeyword** .

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

In dit voorbeeld gebruikt de conversieservice de tekst binnen **name:affKeyword** als een zoekwoord. Nadat de tekst van het **bankrekeningnummer** in het formulier is opgehaald, converteert de conversieservice het veld naar een **getaltype** met behulp van de eigenschap **type** .

### Aanvullende eigenschappen voor gegenereerde adaptieve formuliervelden {#additionalproperties}

Met de eigenschap **name:afProperties** in het meta-model kunt u de volgende aanvullende eigenschappen definiëren voor adaptieve formuliervelden die worden gegenereerd met de service Automated Forms Conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiline</p></td> 
   <td> 
    <p>Met de eigenschap multiline wordt een bronformulierveld na conversie omgezet in een veld met meerdere regels in het adaptieve formulier. Zie Een tekenreeksveld <strong>omzetten in een veld</strong> met meerdere regels in voorbeelden van <a href="#custommetamodelexamples">aangepaste metamodellen voor meer informatie.</a></p> </td> 
  </tr>
  <td><p>mandatory</p></td> 
   <td> 
    <p>Met de eigenschap mandatory wordt de invoer voor een adaptief formulierveld na conversie als verplicht ingesteld.<br>Zie Validaties <strong>toevoegen aan adaptieve formuliervelden</strong> in voorbeelden van het <a href="#custommetamodelexamples">aangepaste metamodel voor meer informatie.</a></p>
    </td> 
  </tr>
  <td><p>jcr:titel</p></td> 
   <td> 
    <p>Met de eigenschap jcr:title, met de eigenschap JSON-schema voor de titel, kunt u het label van een adaptief formulierveld wijzigen na conversie.<br>Zie Het label van een formulierveld <strong></strong> wijzigen in voorbeelden van <a href="#custommetamodelexamples">aangepaste metamodellen voor meer informatie.</a><br>Zie Aangepaste formulieren <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">maken met het JSON-schema</a> voor informatie over meer eigenschappen die u met het JSON-schema op adaptieve formuliervelden kunt toepassen.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType en guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType en guideNodeClass eigenschappen laten u toe om een vormgebied aan een overeenkomstige adaptieve vormcomponent in kaart te brengen.<br>Zie Een formulierveld <strong>converteren naar meerkeuzevakken in het adaptieve formulier</strong> en een tekstveld <strong>converteren naar vervolgkeuzelijst in het adaptieve formulier</strong> in <a href="#custommetamodelexamples">aangepaste metamodelvoorbeelden voor meer informatie.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>Met de eigenschap validatePictureClause wordt een validatie ingesteld voor de indeling die is toegestaan in het adaptieve formulierveld na conversie.<br>Zie Validaties <strong>toevoegen aan adaptieve formuliervelden</strong> in voorbeelden van het <a href="#custommetamodelexamples">aangepaste metamodel voor meer informatie.</p> </td> 
  </tr>
 </tbody> 
</table>

## Aangepaste formuliervelden wijzigen met behulp van een aangepast metamodel {#modify-adaptive-form-fields-using-custom-meta-model}

Uw organisatie kan patronen en bevestigingen naast die hebben die in het standaard meta-model worden vermeld. U kunt het standaardmetamodel uitbreiden om een patroon, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie. De service voor automatische conversie van formulieren past het aangepaste metamodel toe op de formuliervelden tijdens de conversie. U kunt het metamodel blijven bijwerken aangezien de nieuwe patronen, de bevestigingen, en de entiteiten specifiek voor uw organisatie worden ontdekt.

De service Automated Forms Conversion gebruikt een standaardmetamodel dat op de volgende locatie is opgeslagen om bronformuliervelden tijdens de conversie toe te wijzen aan de aangepaste formuliervelden:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

U kunt echter een aangepast metamodel opslaan in een map en de eigenschappen van de conversieservice wijzigen om tijdens de conversie het aangepaste metamodel te gebruiken.

### Aangepast metamodel gebruiken tijdens conversie {#use-custom-meta-model-during-conversion}

Voer de volgende stappen uit om een aangepast meta-model tijdens omzetting te gebruiken:

1. Maak een map in **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** en upload het JSON-schemabestand met het aangepaste metamodel naar de map.
1. Open de eigenschappen van de conversieservice met:

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]**> **&lt;** Eigenschappen van geselecteerde configuratie **>**

1. Geef op het **[!UICONTROL Basic]** tabblad de locatie van het aangepaste metamodel op in het **[!UICONTROL Custom Meta-model]** veld en tik op **[!UICONTROL Save & Close]**.
1. [Voer de conversie](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) uit om het aangepaste metamodel toe te passen op het conversieproces.

### Voorbeelden van aangepaste metamodel {#custommetamodelexamples}

Enkele voorbeelden die vaak worden gebruikt om aangepaste eigenschappen voor formuliervelden te wijzigen, zijn:

* Het label van een formulierveld wijzigen
* Het type van een formulierveld wijzigen
* Help-tekst toevoegen aan een formulierveld
* Een formulierveld converteren naar keuzerondjes met meerdere keuzerondjes in het adaptieve formulier
* De indeling van een formulierveld wijzigen
* Validaties toevoegen aan adaptieve formuliervelden
* Een formulierveld converteren naar opties voor vervolgkeuzelijsten in het aangepaste formulier
* Aanvullende opties toevoegen aan de vervolgkeuzelijst
* Een tekenreeksveld omzetten in een veld met meerdere regels

#### Het label van een formulierveld wijzigen {#modify-the-label-of-a-form-field}

**** Voorbeeld: Wijzig het bankrekeningnummer in het formulier in het aangepaste formulier na de conversie.

In dit aangepaste metamodel gebruikt de conversieservice de eigenschap **title** als een zoekwoord. Nadat de tekst van het **bankrekeningnummer** in het formulier is opgehaald, vervangt de conversieservice de tekst door de tekenreeks **Customer account number** die wordt vermeld met de eigenschap **jcr:title** in de sectie **aem:afProperties** .

```
{
  "numberfields": {
      "type": "number",
   "title": "Bank account number",
   "aem:afProperties" : {
    "jcr:title" : "Customer account number"
   }
   }
}
```

#### Het type van een formulierveld wijzigen {#modify-the-type-of-a-form-field}

**Voorbeeld**: Wijzig het veld **Bankrekeningnummer** van het teksttype in het formulier vóór de conversie naar een nummerveld in het adaptieve formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice de tekst binnen **name:affKeyword** als een zoekwoord. Nadat de tekst van het **bankrekeningnummer** in het formulier is opgehaald, converteert de conversieservice het veld naar een getaltype met behulp van de eigenschap **type** .

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Help-tekst toevoegen aan een formulierveld {#add-help-text-to-a-form-field}

**Voorbeeld**: Voeg Help-tekst toe aan het veld **Bankrekeningnummer** van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice de tekst binnen **name:affKeyword** als een zoekwoord. Nadat de tekst van het **bankrekeningnummer** in het formulier is opgehaald, voegt de conversieservice de Help-tekst toe aan het aangepaste formulierveld met behulp van de eigenschap **description** .

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### Een formulierveld converteren naar meerkeuzevakken in het adaptieve formulier {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**Voorbeeld**: Converteer het **landveld** van het type tekenreeks in het formulier voordat u het converteert naar selectievakjes in het adaptieve formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als een zoekwoord. Nadat de **landtekst** in het formulier is opgehaald, converteert de conversieservice het veld naar de volgende selectievakjes met de eigenschap **enum** :

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:resourceType** en **guideNodeClass** eigenschappen wijzen een vormgebied aan de controledoos adaptieve vormcomponent toe.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### De indeling van een formulierveld wijzigen {#modify-the-format-of-a-form-field}

**Voorbeeld**: Wijzig de indeling van het veld **E-mailadres** in een e-mailindeling.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als een zoekwoord. Nadat de tekst van het **e-mailadres** in het formulier is opgehaald, converteert de conversieservice het veld naar een e-mailindeling met de **indelingseigenschap** .

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### Validaties toevoegen aan adaptieve formuliervelden {#add-validations-to-adaptive-form-fields}

**** Voorbeeld 1: Voeg een validatie toe aan het veld **Postcode** van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als zoektrefwoord. Nadat de tekst van de **postcode** in het formulier is opgehaald, voegt de conversieservice een validatie toe aan het veld met de eigenschap **validatePictureClause** die is gedefinieerd in de sectie **ame:afProperties** . Op basis van de validatie moet de invoer die u opgeeft voor het veld **Postcode** in het adaptieve formulier na conversie zes tekens bevatten.

```
{
   "postalCode" : {
      "aem:affKeyword": ["Postal Code"],
      "type" : "string",
      "aem:afProperties" : {
        "validatePictureClause" : "\\d{6}"
      } 
   }
}
```

**** Voorbeeld 2: Voeg een validatie toe aan het veld **Bankrekeningnummer** van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als zoektrefwoord. Nadat de tekst van het **bankrekeningnummer** in het formulier is opgehaald, voegt de conversiedienst een validatie toe aan het veld met behulp van de **verplichte** eigenschap die is gedefinieerd in de sectie **name:afProperties** . Op basis van de validatie moet u een waarde voor het veld **Bankrekeningnummer** opgeven voordat u het formulier na conversie verzendt.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "aem:afProperties" : {
        "mandatory": "true"
      }   
   }
}
```

#### Een tekstveld omzetten in een vervolgkeuzelijst in het aangepaste formulier {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**Voorbeeld**: Zet het **landveld** van het type tekenreeks in het formulier om vóór de conversie naar vervolgkeuzemogelijkheden in het adaptieve formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als zoektrefwoord. Nadat de **landtekst** in het formulier is opgehaald, converteert de conversieservice het veld naar de volgende opties in de vervolgkeuzelijst met behulp van de eigenschap **enum** :

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:resourceType** en **guideNodeClass** eigenschappen wijzen een vormgebied aan de drop-down adaptieve vormcomponent toe.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidedropdownlist",
      "guideNodeClass": "guideDropDownlist"
    }
  }
}
```

#### Aanvullende opties toevoegen aan de vervolgkeuzelijst {#add-additional-options-to-the-drop-down-list}

**** Voorbeeld: Voeg **Sri Lanka** als extra optie aan een bestaande drop-down lijst toe gebruikend een douane meta-model.

Als u een extra optie wilt toevoegen, werkt u de **opsommingseigenschap** bij met de nieuwe optie. In dit voorbeeld werkt u de **enum** -eigenschap bij met **Sri Lanka** als een extra optie. Waarden die worden vermeld in de **opsommingseigenschap** enum worden weergegeven in de vervolgkeuzelijst.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand",
   "Sri Lanka"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### Een tekenreeksveld omzetten in een veld met meerdere regels {#convert-a-string-field-to-a-multi-line-field}

**** Voorbeeld: Zet het veld **Adres** van het type tekenreeks om in een veld met meerdere regels in het formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **name:affKeyword** als zoektrefwoord. Nadat de tekst van het **Adres** in de vorm wordt teruggewonnen, zet de dienst het tekstgebied in een multi-line gebied gebruikend het **multiline** bezit dat in de **a.afProperties** sectie wordt bepaald.

```
{
 "multiline" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiline": "true"
    }
  }
}
```

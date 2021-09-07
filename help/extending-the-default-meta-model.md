---
title: Het standaard metamodel uitbreiden
seo-title: Extend the default meta-model
description: Het standaardmetamodel uitbreiden om patronen, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service Automatede form conversion wordt uitgevoerd.
seo-description: Extend the default meta-model to add pattern, validations, and entities specific to your organization and apply configurations to adaptive form fields while running the Automated Forms Conversion service.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: 47261710e6616c27c210ac53bffcc2387a06ea7a
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 1%

---

# Het standaard metamodel uitbreiden {#extend-the-default-meta-model}

Met de service automatede form conversion kunt u formulierobjecten herkennen en uitnemen van bronformulieren. Met Semantic-mapper kan de service bepalen hoe de geëxtraheerde objecten in een adaptieve vorm worden weergegeven. Een bronformulier kan bijvoorbeeld vele verschillende soorten representaties van een datum hebben. Met de semantische mapfunctie kunt u alle weergaven van datumformulierobjecten van het bronformulier toewijzen aan datumcomponent van de adaptieve formulieren. Met Semantic mapper kan de service ook validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen vooraf configureren en toepassen op adaptieve formuliercomponenten tijdens conversie.

![](assets/meta-model.gif)

Meta-model is een JSON-schema. Voordat u begint met meta-model, moet u controleren of u goed bent omgedraaid met JSON. U moet ervaring hebben met het maken, bewerken en lezen van gegevens die zijn opgeslagen in de JSON-indeling.

## Standaardmetamodel {#default-meta-model}

De dienst van de automatede form conversion heeft een standaard meta-model. Het is een JSON-schema en bevindt zich op Adobe Cloud met andere onderdelen van de service Automatede form conversion. U kunt een exemplaar van het metamodel op uw lokale AEM server vinden bij: http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`. U kunt ook [hier ](assets/en.globalschema.json) klikken om tot het Engelse taalschema toegang te hebben of te downloaden. Het metamodel voor [Franstalig](assets/fr.globalschema.json), [Duits](assets/de.globalschema.json) [Spaans](assets/es.globalschema.json), [Italiaans](assets/it.globalschema.json) en [Portugees](assets/pt_br.globalschema.json) talen zijn ook beschikbaar voor downloaden.

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

1. Meld u aan bij uw AEM Forms-exemplaar.
1. Navigeer naar de map **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **** **[!UICONTROL Meta Model]**.
1. Selecteer het **[!UICONTROL global.schema.json]** bestand en tik **[!UICONTROL Download]**. Er wordt een dialoogvenster voor downloaden weergegeven. Selecteer de optie **[!UICONTROL Download asset(s) as binary files]**. Tik op **[!UICONTROL Download]**. Er wordt een archief gedownload.

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

In dit voorbeeld vertegenwoordigt **Event** de naam van een entiteit met een waarde voor **id** als **Eventid**. De gebeurtenisentiteit bevat meerdere eigenschappen:

* startDate
* endDate
* locatie

De **allOf** constructie in het meta-model laat overerving onder entiteiten toe.

Elke eigenschap kan verder het volgende bevatten:

* [Eigenschappen van JSON-schema](#jsonschemaproperties)
* [Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden](#keywordsearch)
* [Aanvullende eigenschappen](#additionalproperties)

![Eigenschappen van het metamodel](assets/meta_model_elements.gif)

Op basis van de trefwoorden waarnaar wordt verwezen met **name:affKeyword**, voert de conversieservice een zoekbewerking uit op de bronformuliervelden. De conversieservice past de eigenschappen van het JSON-schema en aanvullende eigenschappen toe op de velden die aan de zoekcriteria voldoen.

In dit voorbeeld zoekt de conversieservice naar de telefoon, de telefoon, de mobiele telefoon, de werktelefoon, de thuistelefoon, het telefoonnummer, het telefoonnummer en het telefoonnummer van de trefwoorden in het bronformulier. Op basis van de velden die deze trefwoorden bevatten, past de conversieservice het type, het patroon en de naam:afProperties toe op de adaptieve formuliervelden na de conversie.

### JSON-schemaeigenschappen voor gegenereerde adaptieve formuliervelden {#jsonschemaproperties}

Het metamodel ondersteunt de volgende gemeenschappelijke eigenschappen van het JSON-schema voor adaptieve formuliervelden die worden gegenereerd met behulp van de service Automatede form conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>title</p></td> 
   <td> 
    <p>De tekst die in de eigenschap title in een metamodel wordt genoemd, fungeert als trefwoord voor zoekacties in de gegenereerde adaptieve formuliervelden. U kunt bijvoorbeeld het label van een adaptief formulierveld wijzigen. Zie <strong>Het label van een formulierveld wijzigen</strong> in <a href="#custommetamodelexamples">Aangepaste voorbeelden van het metamodel.</a></p> </td> 
  </tr>
  <td><p>beschrijving</p></td> 
   <td> 
    <p>Met de eigenschap description wordt de Help-tekst voor het gegenereerde adaptieve formulierveld ingesteld. Zie <strong>Help-tekst toevoegen aan een formulierveld</strong> in <a href="#custommetamodelexamples">Aangepaste voorbeelden van metamodel.</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>De eigenschap type definieert het gegevenstype voor het gegenereerde adaptieve formulierveld. De mogelijke waarden voor de eigenschap title zijn:</p>
    <ul> 
     <li>tekenreeks: Hiermee wordt een adaptief formulierveld van het tekstgegevenstype gegenereerd.</li> 
     <li>getal: Hiermee genereert u een adaptief formulierveld met een numeriek gegevenstype.</li>
     <li>integer: Genereert een adaptief formulierveld van een numeriek gegevenstype met subtype ingesteld op geheel getal.</li>
     <li>Booleaans: Genereert een schakeloptie voor adaptieve formulieren.</li>
     </ul><p>Zie <strong>Het type van een formulierveld wijzigen</strong> in <a href="#custommetamodelexamples">Aangepaste metamodelvoorbeelden.</a> voor meer informatie over het gebruik van de eigenschap type in een metamodel.</p></td> 
  </tr>
  <td><p>pattern</p></td> 
   <td> 
    <p>De eigenschap pattern beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een reguliere expressie. De volgende code in het metamodel beperkt bijvoorbeeld de waarde voor het gegenereerde adaptieve formulierveld tot tien cijfers:<br>"patroon": "/\\d{10}/"<br>Op dezelfde manier beperkt de volgende code in het metamodel de waarde van een gebied tot een specifiek datumformaat.<br> "patroon": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>De eigenschap format beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een benoemd patroon in plaats van een reguliere expressie. De mogelijke waarden voor de opmaakeigenschap zijn:<ul><li>e-mail: Hiermee genereert u een adaptieve e-mailformuliercomponent.</li><li>hostnaam: Hiermee genereert u een adaptief tekstvak-formuliercomponent.</li></ul>Zie <strong>De indeling van een formulierveld wijzigen</strong> in <a href="#custommetamodelexamples">Aangepaste voorbeelden van metamodel.</a> voor meer informatie over het gebruik van de indelingseigenschap in een metamodel.</p> </td> 
  </tr>
  <td><p>enum en enumNames</p></td> 
   <td> 
    <p>De eigenschappen enum en enumNames beperken de waarden van drop-down, controledoos, of radioknoopgebieden tot een vaste reeks. Waarden die in enumNames worden vermeld, worden weergegeven in de gebruikersinterface. De waarden die worden vermeld gebruikend het enum bezit worden gebruikt voor berekening.<br>Zie Een formulierveld  <strong>converteren naar meerkeuzevakken in het adaptieve formulier</strong>, een tekstveld  <strong>converteren naar vervolgkeuzelijst in het adaptieve formulier</strong> en aanvullende opties  <strong>toevoegen aan de vervolgkeuzelijst </strong> Aangepaste  <a href="#custommetamodelexamples">metamodelvoorbeelden.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden {#keywordsearch}

De dienst van de automatede form conversion voert een sleutelwoordonderzoek op de bronvorm tijdens omzetting uit. Nadat de velden die aan de zoekcriteria voldoen, zijn gefilterd, past de conversieservice de eigenschappen die voor die velden in het metamodel zijn gedefinieerd toe op de gegenereerde adaptieve formuliervelden.

Er wordt naar trefwoorden verwezen met de eigenschap **name:affKeyword**.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

In dit voorbeeld gebruikt de conversieservice de tekst binnen **aem:affKeyword** als een zoekwoord. Nadat de **Bankrekeningnummer** tekst in het formulier is opgehaald, converteert de conversieservice het veld naar een **nummer** type met behulp van de eigenschap **type**.

### Aanvullende eigenschappen voor gegenereerde adaptieve formuliervelden {#additionalproperties}

Met de eigenschap **aem:afProperties** in het metamodel kunt u de volgende aanvullende eigenschappen definiëren voor adaptieve formuliervelden die worden gegenereerd met behulp van de service Automatede form conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>Met de eigenschap multiLine wordt een bronformulierveld na conversie omgezet in een veld met meerdere regels in het adaptieve formulier. Zie <strong>Een tekenreeksveld omzetten in een veld met meerdere regels</strong> in <a href="#custommetamodelexamples">Aangepaste voorbeelden van metamodel.</a></p> </td> 
  </tr>
  <td><p>mandatory</p></td> 
   <td> 
    <p>Met de eigenschap mandatory wordt de invoer voor een adaptief formulierveld na conversie als verplicht ingesteld.<br>Zie Validaties  <strong>toevoegen aan adaptieve formuliervelden </strong> in voorbeelden van  <a href="#custommetamodelexamples">aangepaste metamodel voor meer informatie.</a></p>
    </td> 
  </tr>
  <td><p>jcr:titel</p></td> 
   <td> 
    <p>Met de eigenschap jcr:title, met de eigenschap JSON-schema voor de titel, kunt u het label van een adaptief formulierveld wijzigen na conversie.<br>Zie Het label van een formulierveld  <strong>wijzigen </strong> in voorbeelden van  <a href="#custommetamodelexamples">aangepaste metamodellen voor meer informatie.</a><br>Zie Aangepaste formulieren  <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">maken met JSON-</a> schema voor informatie over meer eigenschappen die u met JSON-schema op adaptieve formuliervelden kunt toepassen.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType en guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType en guideNodeClass eigenschappen laten u toe om een vormgebied aan een overeenkomstige adaptieve vormcomponent in kaart te brengen.<br>Zie Een formulierveld  <strong>converteren naar meerkeuzevakken in het aangepaste </strong> formulier en een tekstveld  <strong>converteren naar vervolgkeuzelijst in de voorbeelden van het aangepaste </strong> formiemodel  <a href="#custommetamodelexamples">Aangepast.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>Met de eigenschap validatePictureClause wordt een validatie ingesteld voor de indeling die is toegestaan in het adaptieve formulierveld na conversie.<br>Zie Validaties  <strong>toevoegen aan adaptieve formuliervelden </strong> in voorbeelden van  <a href="#custommetamodelexamples">aangepaste metamodel voor meer informatie.</p> </td> 
  </tr>
 </tbody> 
</table>

## Een aangepast model in uw eigen taal maken{#language-specific-meta-model}

U kunt een taalspecifiek metamodel maken. Een dergelijk metamodel helpt u toewijzingsregels te maken in de taal van uw keuze. Met de service automatede form conversion kunt u metamodellen maken in de volgende talen:

* Engels(en)
* Frans(fr)
* Duits(de)
* Spaans
* Italiaans(it)
* Portugees (pt-br)

Voeg de metatag *aem:Language* toe aan de bovenkant van een metamodel om zijn taal te specificeren. Bijvoorbeeld,

```JSON
"metaTags": {
        "aem:Language": "fr"
    }
```

Wanneer geen taal wordt gespecificeerd, is de dienst van mening dat meta-model in het Engels taal is.

### Overwegingen bij het maken van een taalspecifiek metamodel

* Zorg ervoor dat elke sleutel in het Engels heet. Bijvoorbeeld emailAddress.
* Zorg ervoor dat alle entiteitverwijzingen en vooraf gedefinieerde waarden van alle id-sleutel alleen ASCII-tekens bevatten. Bijvoorbeeld &quot;id&quot;: &quot;ContactPoint&quot; / &quot;$ref&quot;: &quot;#ContactPoint&quot;.
* Zorg ervoor dat alle waarden die overeenkomen met de volgende toetsen zich in de opgegeven taal van het metamodel bevinden:
   * aem:affKeyword
   * titel
   * beschrijving
   * enumNames
   * shortDescription
   * validatePictureClauseMessage

   Wanneer de taal van het metamodel bijvoorbeeld Frans is (&quot;aem:Language&quot;: &quot;fr&quot;), moet u ervoor zorgen dat alle beschrijvingen en berichten in het Frans zijn gesteld.

* Zorg ervoor dat alle [JSON-schemaeigenschappen](#jsonschemaproperties) alleen ondersteunde waarden gebruiken. De eigenschap type kan bijvoorbeeld alleen geselecteerde waarden van String, Number, Integer en Boolean omvatten.

In de volgende afbeelding ziet u voorbeelden van het metamodel voor de Engelse taal en het overeenkomstige metamodel voor de Franse taal:

![](assets/language-specific-meta-model-comparison.png)

## Aangepaste formuliervelden wijzigen met behulp van een aangepast metamodel {#modify-adaptive-form-fields-using-custom-meta-model}

Uw organisatie kan patronen en bevestigingen naast die hebben die in het standaard meta-model worden vermeld. U kunt het standaardmetamodel uitbreiden om een patroon, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie. Tijdens de conversie past de service automatede form conversion het aangepaste metamodel toe op de formuliervelden. U kunt het metamodel blijven bijwerken aangezien de nieuwe patronen, de bevestigingen, en de entiteiten specifiek voor uw organisatie worden ontdekt.

De service automatede form conversion gebruikt een standaardmetamodel dat op de volgende locatie is opgeslagen om bronformuliervelden tijdens de conversie toe te wijzen aan de aangepaste formuliervelden:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

U kunt echter een aangepast metamodel opslaan in een map en de eigenschappen van de conversieservice wijzigen om tijdens de conversie het aangepaste metamodel te gebruiken.

### Aangepast metamodel gebruiken tijdens conversie {#use-custom-meta-model-during-conversion}

Voer de volgende stappen uit om een aangepast meta-model tijdens omzetting te gebruiken:

1. Maak een map in **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** en upload het aangepaste JSON-schemabestand naar het metamodel in de map.
1. Open de eigenschappen van de conversieservice met:

   **[!UICONTROL Tools]** >  **[!UICONTROL Cloud Services]** >  **[!UICONTROL Automated Forms Conversion Configuration]**>  **&lt;>Eigenschappen van geselecteerde configuratie**>****

1. Geef op het tabblad **[!UICONTROL Basic]** de locatie van het aangepaste metamodel op in het veld **[!UICONTROL Custom Meta-model]** en tik **[!UICONTROL Save & Close]**.
1. [Voer de ](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) conversie uit om het aangepaste metamodel toe te passen op het conversieproces.

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

**Voorbeeld:** Wijzig het label Bankrekeningnummer in het formulier in Aangepast rekeningnummer in het adaptieve formulier na de conversie.

In dit aangepaste metamodel gebruikt de conversieservice de eigenschap **title** als een zoekwoord. Nadat de tekst van **Bankrekeningnummer** in het formulier is opgehaald, vervangt de conversieservice de tekst door de tekenreeks **Klantaccountnummer** die wordt vermeld met de eigenschap **jcr:title** in de sectie **aem:afProperties**.

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

**Voorbeeld**: Wijzig het  **tekstveld voor het** bankrekeningnummer van het formulier vóór de conversie naar een nummerveld in het adaptieve formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice de tekst binnen **aem:affKeyword** als een zoekwoord. Nadat de **Bankrekeningnummer** tekst in het formulier is opgehaald, converteert de conversieservice het veld naar een getaltype met behulp van de eigenschap **type**.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Help-tekst toevoegen aan een formulierveld {#add-help-text-to-a-form-field}

**Voorbeeld**: Voeg Help-tekst toe aan het  **veld voor het nummer van de** bankrekening van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice de tekst binnen **aem:affKeyword** als een zoekwoord. Nadat de **Bankrekeningnummer** tekst in het formulier is opgehaald, voegt de conversieservice de Help-tekst toe aan het aangepaste formulierveld met behulp van de eigenschap **description**.

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

**Voorbeeld**: Converteer het  **** landveld van het type tekenreeks in het formulier voordat u het converteert naar selectievakjes in het adaptieve formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als een zoekwoord. Nadat de **Country** tekst in het formulier is opgehaald, converteert de conversieservice het veld naar de volgende selectievakjes met behulp van de eigenschap **enum**:

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:** resourceType en  **** guideNodeClassproperties wijzen een formulierveld toe aan het selectievakje adaptieve formuliercomponent.

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

**Voorbeeld**: Wijzig de indeling van het veld  **E-** mailadres in een e-mailindeling.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als een zoekwoord. Nadat de **e-mailadres** tekst in het formulier is opgehaald, converteert de conversieservice het veld naar een e-mailindeling met de eigenschap **format**.

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

**Voorbeeld 1:** Voeg een validatie toe aan het veld  **Postal** Codefield van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als zoektrefwoord. Nadat de **Postal Code**-tekst in het formulier is opgehaald, voegt de conversieservice een validatie toe aan het veld met de eigenschap **validatePictureClause** die is gedefinieerd in de sectie **aem:afProperties**. Op basis van de validatie moet de invoer die u opgeeft voor het veld **Postcode** in het adaptieve formulier na conversie zes tekens bevatten.

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

**Voorbeeld 2:** Voeg een validatie toe aan het veld  **Bankrekeningnummer** van het adaptieve formulier.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als zoektrefwoord. Nadat de **Bankrekeningnummer** tekst in het formulier is opgehaald, voegt de conversieservice een validatie toe aan het veld met behulp van de **mandatory**-eigenschap die is gedefinieerd in de sectie **aem:afProperties**. Op basis van de validatie moet u een waarde opgeven voor het veld **Bankrekeningnummer** voordat u het formulier na conversie verzendt.

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

**Voorbeeld**: Zet het  **** landveld van het type tekenreeks in het formulier om voordat u het formulier converteert naar vervolgkeuzemogelijkheden in het aangepaste formulier na conversie.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als zoektrefwoord. Nadat de **Country** tekst in het formulier is opgehaald, converteert de conversieservice het veld naar de volgende vervolgkeuzelijstopties met behulp van de eigenschap **enum**:

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:** resourceType en  **** guideNodeClassproperties wijzen een formulierveld toe aan de drop-down adaptieve formuliercomponent.

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

**Voorbeeld:** Voeg  **Sri** Kanalen als extra optie aan een bestaande drop-down lijst toe gebruikend een douane meta-model.

Als u een extra optie wilt toevoegen, werkt u de eigenschap **enum** bij met de nieuwe optie. In dit voorbeeld werkt u de eigenschap **enum** bij met **Sri Lanka** als een extra optie. Waarden vermeld in **enum** bezitsvertoning in de drop-down lijst.

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

**Voorbeeld:** Zet het  **** adressveld van het type tekenreeks na conversie om in een veld met meerdere regels in het formulier.

In dit aangepaste metamodel gebruikt de conversieservice tekst binnen **aem:affKeyword** als zoektrefwoord. Nadat de **Address** tekst in het formulier is opgehaald, converteert de service het tekstveld naar een veld met meerdere regels met behulp van de eigenschap **multiLine** die is gedefinieerd in de sectie **aem:afProperties**.

```
{
 "multiLine" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiLine": "true"
    }
  }
}
```

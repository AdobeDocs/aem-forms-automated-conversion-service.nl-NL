---
title: Het standaardmetamodel uitbreiden
description: Breid het standaardmetamodel uit om een patroon, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service Automatede form conversion (AFCS) wordt uitgevoerd.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 0%

---

# Het standaardmetamodel uitbreiden {#extend-the-default-meta-model}

Met AFCS (automatede form conversion Service) kunt u formulierobjecten herkennen en uitnemen van bronformulieren. Met Semantic-mapper kan de service bepalen hoe de geëxtraheerde objecten in een adaptieve vorm worden weergegeven. Een bronformulier kan bijvoorbeeld vele verschillende soorten representaties van een datum hebben. Met de semantische mapfunctie kunt u alle weergaven van datumformulierobjecten van het bronformulier toewijzen aan datumcomponent van de adaptieve formulieren. Met Semantic mapper kan de service ook validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen vooraf configureren en toepassen op adaptieve formuliercomponenten tijdens conversie.

![](assets/meta-model.gif)

Meta-model is een JSON-schema. Voordat u begint met meta-model, moet u controleren of u goed bent omgedraaid met JSON. U moet ervaring hebben met het maken, bewerken en lezen van gegevens die zijn opgeslagen in de JSON-indeling.

## Standaardmetamodel {#default-meta-model}

De dienst van de automatede form conversion (AFCS) heeft een standaardmetamodel. Het is een JSON-schema en bevindt zich op de Adobe Cloud met andere onderdelen van de AFCS (Automatede form conversion Service). U kunt een exemplaar van het meta-model op uw lokale AEM server bij vinden: http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`. U kunt ook [ hier ](assets/en.globalschema.json) klikken om tot het Engelse taalschema toegang te hebben of te downloaden. Het meta-model voor [ Frans ](assets/fr.globalschema.json), [ Duits ](assets/de.globalschema.json) [ Spaans ](assets/es.globalschema.json), [ Italiaans ](assets/it.globalschema.json), en [ Portugese ](assets/pt_br.globalschema.json) talen zijn ook beschikbaar voor download.

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
1. Navigeer naar de map **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]** .
1. Selecteer het **[!UICONTROL global.schema.json]** -bestand en tik op **[!UICONTROL Download]** . Er wordt een dialoogvenster voor downloaden weergegeven. Selecteer de optie **[!UICONTROL Download asset(s) as binary files]** . Tik op **[!UICONTROL Download]**. Er wordt een archief gedownload.

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

In dit voorbeeld, **vertegenwoordigt de Gebeurtenis** de naam van een entiteit met een waarde voor **identiteitskaart** als **Uitgezochte**. De gebeurtenisentiteit bevat meerdere eigenschappen:

* startDate
* endDate
* locatie

**allOf** aannemer in meta-model laat overerving onder entiteiten toe.

Elke eigenschap kan verder het volgende bevatten:

* [Eigenschappen van JSON-schema](#jsonschemaproperties)
* [Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden](#keywordsearch)
* [Aanvullende eigenschappen](#additionalproperties)

![ meta-model eigenschappen ](assets/meta_model_elements.gif)

Gebaseerd op de sleutelwoorden van verwijzingen voorzien gebruikend **naam:affKeyword**, voert de omzettingsdienst een onderzoeksverrichting op de bronvormgebieden uit. De conversieservice past de eigenschappen van het JSON-schema en aanvullende eigenschappen toe op de velden die aan de zoekcriteria voldoen.

In dit voorbeeld zoekt de conversieservice naar de telefoon, de telefoon, de mobiele telefoon, de werktelefoon, de thuistelefoon, het telefoonnummer, het telefoonnummer en het telefoonnummer van de trefwoorden in het bronformulier. Op basis van de velden die deze trefwoorden bevatten, past de conversieservice het type, het patroon en de naam:afProperties toe op de adaptieve formuliervelden na de conversie.

### JSON-schemaeigenschappen voor gegenereerde adaptieve formuliervelden {#jsonschemaproperties}

Het metamodel ondersteunt de volgende gemeenschappelijke eigenschappen van het JSON-schema voor adaptieve formuliervelden die zijn gegenereerd met de Automatede form conversion-service (AFCS):

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>titel</p></td> 
   <td> 
    <p>De tekst die in de eigenschap title in een metamodel wordt genoemd, fungeert als trefwoord voor zoekacties in de gegenereerde adaptieve formuliervelden. U kunt bijvoorbeeld het label van een adaptief formulierveld wijzigen. Voor meer informatie, zie <strong> het etiket van een vormgebied </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden wijzigen.</a></p> </td> 
  </tr>
  <td><p>beschrijving</p></td> 
   <td> 
    <p>Met de eigenschap description wordt de Help-tekst voor het gegenereerde adaptieve formulierveld ingesteld. Voor meer informatie, zie <strong> de tekst van de Hulp aan een vormgebied </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden toevoegen.</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>De eigenschap type definieert het gegevenstype voor het gegenereerde adaptieve formulierveld. De mogelijke waarden voor de eigenschap title zijn:</p>
    <ul> 
     <li>tekenreeks: genereert een adaptief formulierveld met tekstgegevenstype.</li> 
     <li>Getal: genereert een adaptief formulierveld met een numeriek gegevenstype.</li>
     <li>geheel getal: genereert een adaptief formulierveld van een numeriek gegevenstype met subtype ingesteld op geheel getal.</li>
     <li>Boolean: genereert een schakelbare adaptieve formuliercomponent.</li>
     </ul><p>Voor meer informatie bij het gebruiken van het typebezit in a meta-model, zie <strong> het type van een vormgebied </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden wijzigen.</a></p></td> 
  </tr>
  <td><p>patroon</p></td> 
   <td> 
    <p>De eigenschap pattern beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een reguliere expressie. Bijvoorbeeld, beperkt de volgende code in meta-model de waarde voor het geproduceerde adaptieve vormgebied tot tien cijfers:<br> "patroon": "/\ \ d \ {10 \}/"<br> Op dezelfde manier, beperkt de volgende code in meta-model de waarde van een gebied tot een specifiek datumformaat.<br> "pattern": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>De eigenschap format beperkt de waarde voor het gegenereerde adaptieve formulierveld op basis van een benoemd patroon in plaats van een reguliere expressie. De mogelijke waarden voor de opmaakeigenschap zijn:<ul><li>E-mail: Hiermee genereert u een adaptieve e-mailformuliercomponent.</li><li>hostnaam: genereert een tekstvak adaptieve formuliercomponent.</li></ul>Voor meer informatie bij het gebruiken van het formaatbezit in a meta-model, zie <strong> het formaat van een vormgebied </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden wijzigen.</a></p> </td> 
  </tr>
  <td><p>enum en enumNames</p></td> 
   <td> 
    <p>De eigenschappen enum en enumNames beperken de waarden van drop-down, controledoos, of radioknoopgebieden tot een vaste reeks. Waarden die in enumNames worden vermeld, worden weergegeven in de gebruikersinterface. De waarden die worden vermeld gebruikend het enum bezit worden gebruikt voor berekening.<br> voor meer informatie, zie <strong> een vormgebied in veelvoudige-keus controledozen in de adaptieve vorm </strong> omzetten, <strong> zet een tekstgebied in drop-down lijst in de adaptieve vorm </strong>, en <strong> voegt extra opties aan de drop-down lijst </strong> in <a href="#custommetamodelexamples"> meta-model voorbeelden van de Douane toe.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Op trefwoorden gebaseerde zoekopdracht om eigenschappen toe te passen op gegenereerde adaptieve formuliervelden {#keywordsearch}

De dienst van de automatede form conversion (AFCS) voert een sleutelwoordonderzoek op het bronvorm tijdens omzetting uit. Nadat de velden die aan de zoekcriteria voldoen, zijn gefilterd, past de conversieservice de eigenschappen die voor die velden in het metamodel zijn gedefinieerd toe op de gegenereerde adaptieve formuliervelden.

De sleutelwoorden worden van verwijzingen voorzien gebruikend het **naam:affKeyword** bezit.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

In dit voorbeeld, gebruikt de omzettingsdienst de tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het de rekeningsaantal van de Bank** in de vorm, zet de omzettingsdienst het gebied in a **aantal** type gebruikend het **type** bezit om.

### Aanvullende eigenschappen voor gegenereerde adaptieve formuliervelden {#additionalproperties}

U kunt het **gebruiken aem:afProperties** bezit in meta-model om volgende extra eigenschappen voor adaptieve vormgebieden te bepalen die gebruikend de dienst van de Automatede form conversion (AFCS) worden geproduceerd:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Eigenschapnaam</strong></th> 
   <th><strong>Beschrijving</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>Met de eigenschap multiLine wordt een bronformulierveld na conversie omgezet in een veld met meerdere regels in het adaptieve formulier. Voor meer informatie, zie <strong> een koordgebied in een multi-line gebied </strong> in <a href="#custommetamodelexamples"> de meta-model voorbeelden van de Douane omzetten.</a></p> </td> 
  </tr>
  <td><p>verplicht</p></td> 
   <td> 
    <p>Met de eigenschap mandatory wordt de invoer voor een adaptief formulierveld na conversie als verplicht ingesteld.<br> voor meer informatie, zie <strong> bevestigingen aan adaptieve vormgebieden </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden toevoegen.</a></p>
    </td> 
  </tr>
  <td><p>jcr:titel</p></td> 
   <td> 
    <p>Met de eigenschap jcr:title, met de eigenschap JSON-schema voor de titel, kunt u het label van een adaptief formulierveld wijzigen na conversie.<br> voor meer informatie, zie <strong> het etiket van een vormgebied </strong> in <a href="#custommetamodelexamples"> meta-model voorbeelden van de Douane wijzigen.</a><br> zie <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank"> Creërend adaptieve vormen gebruikend schema JSON </a> voor informatie over meer eigenschappen die u op adaptieve vormgebieden kunt toepassen gebruikend schema JSON.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType en guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType en guideNodeClass eigenschappen laten u toe om een vormgebied aan een overeenkomstige adaptieve vormcomponent in kaart te brengen.<br> voor meer informatie, zie <strong> een vormgebied in veelvoudige-keus controledozen in de adaptieve vorm </strong> omzetten en <strong> zet een tekstgebied in drop-down lijst in de adaptieve vorm </strong> in <a href="#custommetamodelexamples"> meta-model voorbeelden van de Douane om.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>Met de eigenschap validatePictureClause wordt een validatie ingesteld voor de indeling die is toegestaan in het adaptieve formulierveld na conversie.<br> voor meer informatie, zie <strong> bevestigingen aan adaptieve vormgebieden </strong> in <a href="#custommetamodelexamples"> Douane meta-model voorbeelden toevoegen.</p> </td> 
  </tr>
 </tbody> 
</table>

## Een aangepast model in uw eigen taal maken{#language-specific-meta-model}

U kunt een taalspecifiek metamodel maken. Een dergelijk metamodel helpt u toewijzingsregels te maken in de taal van uw keuze. Met AFCS (automatede form conversion Service) kunt u metamodellen maken in de volgende talen:

* Engels(en)
* Frans(fr)
* Duits(de)
* Spaans(en)
* Italiaans(it)
* Portugees (pt-br)

Voeg *naam toe:Taal* metatag markering aan bovenkant een meta-model om zijn taal te specificeren. Bijvoorbeeld:

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

  Wanneer de taal van het metamodel bijvoorbeeld Frans is (&quot;aem:Language&quot;: &quot;fr&quot;), moet u ervoor zorgen dat alle beschrijvingen en berichten in de Franse taal zijn geschreven.

* Verzeker alle [ het schemaeigenschappen van JSON ](#jsonschemaproperties) gebruik slechts gesteunde waarden. De eigenschap type kan bijvoorbeeld alleen geselecteerde waarden van String, Number, Integer en Boolean omvatten.

In de volgende afbeelding ziet u voorbeelden van het metamodel voor de Engelse taal en het overeenkomstige metamodel voor de Franse taal:

![](assets/language-specific-meta-model-comparison.png)

## Aangepaste formuliervelden wijzigen met behulp van een aangepast metamodel {#modify-adaptive-form-fields-using-custom-meta-model}

Uw organisatie kan patronen en bevestigingen naast die hebben die in het standaard meta-model worden vermeld. U kunt het standaardmetamodel uitbreiden om een patroon, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie. AFCS (automatede form conversion Service) past tijdens de conversie het aangepaste metamodel toe op de formuliervelden. U kunt het metamodel blijven bijwerken aangezien de nieuwe patronen, de bevestigingen, en de entiteiten specifiek voor uw organisatie worden ontdekt.

De service automatede form conversion (AFCS) gebruikt een standaardmetamodel dat op de volgende locatie is opgeslagen om bronformuliervelden tijdens de conversie toe te wijzen aan de adaptieve formuliervelden:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

U kunt echter een aangepast metamodel opslaan in een map en de eigenschappen van de conversieservice wijzigen om tijdens de conversie het aangepaste metamodel te gebruiken.

### Aangepast metamodel gebruiken tijdens conversie {#use-custom-meta-model-during-conversion}

Voer de volgende stappen uit om een aangepast meta-model tijdens omzetting te gebruiken:

1. Maak een map in **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** en upload het JSON-schemabestand met het aangepaste metamodel naar de map.
1. Open de eigenschappen van de conversieservice met:

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **&lt;Eigenschappen van geselecteerde configuratie>**

1. Geef op het tabblad **[!UICONTROL Basic]** de locatie van het aangepaste metamodel op in het veld **[!UICONTROL Custom Meta-model]** en tik op **[!UICONTROL Save & Close]** .
1. [ stel de omzetting ](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) in werking om het douane meta-model op het omzettingsproces toe te passen.

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

**Voorbeeld:** wijzig het etiket van het de rekeningsaantal van de Bank in de vorm aan het Aantal van de Rekening van de Douane in de adaptieve vorm na omzetting.

In dit douane meta-model, gebruikt de omzettingsdienst het **titel** bezit als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het de rekeningsaantal van de Bank** in de vorm, vervangt de omzettingsdienst de tekst met het **3} koord van het de rekeningsaantal van de Klant dat met** jcr wordt vermeld:titel **bezit in** aem:afProperties **sectie.**

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

**Voorbeeld**: Wijzig het **3} gebied van het de rekeningsaantal van de Bank {van teksttype in de vorm vóór omzetting in een aantaltypegebied in de adaptieve vorm na omzetting.**

In dit douane meta-model, gebruikt de omzettingsdienst de tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het de rekeningsaantal van de Bank** in de vorm, zet de omzettingsdienst het gebied in een aantaltype gebruikend het **type** bezit om.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Help-tekst toevoegen aan een formulierveld {#add-help-text-to-a-form-field}

**Voorbeeld**: Voeg de tekst van de Hulp aan het **3} gebied van het de rekeningsaantal van de Bank {van adaptieve vorm toe.**

In dit douane meta-model, gebruikt de omzettingsdienst de tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het de rekeningsaantal van de Bank** in de vorm, voegt de omzettingsdienst de tekst van de Hulp aan het adaptieve vormgebied toe gebruikend het **beschrijvings** bezit.

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

**Voorbeeld**: Zet het **3} gebied van het Land {van koordtype in de vorm vóór omzetting in controledozen in de adaptieve vorm na omzetting om.**

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het Land** in de vorm, zet de omzettingsdienst het gebied in volgende controledozen gebruikend het **enum** bezit om:

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:resourceType** en **guideNodeClass** eigenschappen kaart een vormgebied aan de component van de controledoos adaptieve vorm.

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

**Voorbeeld**: Wijzig het formaat van het **E-mailadres** gebied aan een e-mailformaat.

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **Tekst van het E-mailAdres** in de vorm, zet de omzettingsdienst het gebied in een e-mailformaat gebruikend het **formaat** bezit om.

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

**Voorbeeld 1:** voeg een bevestiging aan het **3} gebied van de Code van de Postal van de adaptieve vorm toe.**

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van de Postcode** in de vorm, voegt de omzettingsdienst een bevestiging aan het gebied toe gebruikend het **validatePictureClause** bezit dat in **wordt bepaald:afProperties** sectie. Gebaseerd op de bevestiging, moet de input die u voor het **gebied van de Code van de Postal** in de adaptieve vorm na omzetting specificeert zes karakters omvatten.

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

**Voorbeeld 2:** voeg een bevestiging aan het **3} gebied van het de rekeningsaantal van de Bank {van de adaptieve vorm toe.**

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het de rekeningsaantal van de Bank** in de vorm, voegt de omzettingsdienst een bevestiging aan het gebied toe gebruikend het **verplichte** bezit dat in **wordt bepaald:afProperties** sectie. Gebaseerd op de bevestiging, moet u een waarde voor het **gebied van het de rekeningsaantal van de 1} Bank specificeren alvorens de vorm na omzetting voor te leggen.**

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

**Voorbeeld**: Zet het **3} gebied van het Land {van koordtype in de vorm vóór omzetting in drop-down opties in de adaptieve vorm na omzetting om.**

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het Land** in de vorm, zet de omzettingsdienst het gebied in volgende drop-down lijstopties gebruikend het **enum** bezit om:

* India
* Engeland
* Australië
* Nieuw-Zeeland

**sling:resourceType** en **guideNodeClass** eigenschappen kaart een vormgebied aan de drop-down adaptieve vormcomponent.

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

**Voorbeeld:** voeg **Sri Lanka** als extra optie aan een bestaande drop-down lijst toe gebruikend een douane meta-model.

Om een extra optie toe te voegen, werk het **enum** bezit met de nieuwe optie bij. In dit voorbeeld, werk het **enum** bezit met **Sri Lanka** als extra optie bij. Waarden die in **worden vermeld enum** bezitsvertoning in de drop-down lijst.

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

**Voorbeeld:** zet het **3} gebied van het Adres {van koordtype in een multi-line gebied in de vorm na omzetting om.**

In dit douane meta-model, gebruikt de omzettingsdienst tekst binnen **naam:affKeyword** als onderzoekssleutelwoord. Na het terugwinnen van de **tekst van het Adres** in de vorm, zet de dienst het tekstgebied in een multi-line gebied gebruikend het **multiLine** bezit dat in **wordt bepaald:afProperties** sectie.

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

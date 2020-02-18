---
title: De geconverteerde adaptieve formulieren met een JSON-schema naar database verzenden
description: Verzend de geconverteerde adaptieve formulieren met een JSON-schema naar de database door een formuliergegevensmodel te maken en er in een AEM-workflow naar te verwijzen.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: b879a0ddecd5370c754dfe9e1bf33121dd5ecc97

---


# Aangepast formulier integreren met database met AEM-workflow {#submit-forms-to-database-using-forms-portal}

Met de service voor automatische formulierconversie kunt u een niet-interactief PDF-formulier, een Acro-formulier of een op XFA gebaseerd PDF-formulier converteren naar een adaptief formulier. Tijdens het starten van het conversieproces kunt u een adaptief formulier genereren, met of zonder gegevensbindingen.

Als u een adaptief formulier wilt genereren zonder gegevensbindingen, kunt u het geconverteerde adaptieve formulier na conversie integreren met een formuliergegevensmodel, XML-schema of JSON-schema. Voor het formuliergegevensmodel moet u adaptieve formuliervelden handmatig binden met het formuliergegevensmodel. Als u echter een adaptief formulier genereert met gegevensbindingen, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden die beschikbaar zijn in het adaptieve formulier en het JSON-schema. Vervolgens kunt u het aangepaste formulier integreren met een door u gewenste database, gegevens in het formulier invullen en naar de database verzenden. Op dezelfde manier kunt u, nadat u de integratie met de database hebt voltooid, velden in het geconverteerde adaptieve formulier configureren om waarden op te halen uit de database en aangepaste formuliervelden vooraf invullen.

In de volgende afbeelding ziet u de verschillende fasen van het integreren van een geconverteerd adaptief formulier in een database:

![database-integratie](assets/integrate-adaptive-form-with-database.png)

In dit artikel worden de stapsgewijze instructies beschreven waarmee u al deze integratiefasen kunt uitvoeren.

## Voorwaarden {#pre-requisites}

* AEM 6.5-auteurinstantie met de nieuwste AEM 6.5 Service Pack
* Laatste versie van het invoegpakket voor AEM Forms
* [Automated Forms Conversion-service](configure-service.md)
* Een database die moet worden geïntegreerd. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt het geconverteerde adaptieve formulier echter integreren met elke gewenste database.

## Monster van adaptief formulier {#sample-adaptive-form}

Als u geconverteerde adaptieve formulieren met een AEM-workflow wilt integreren in de database, downloadt u het volgende voorbeeld-PDF-bestand.

U kunt het voorbeeld van het contactformulier downloaden met:

[Bestand ophalen](assets/sample_contact_us_form.pdf)

Het PDF-bestand fungeert als invoer voor de service Formulierconversie automatiseren. De service converteert dit bestand naar een adaptief formulier. In de volgende afbeelding ziet u het voorbeeld waarmee u contact met ons opneemt in een PDF-indeling.

![aanvraagformulier voor een voorbeeldlening](assets/sample_contact_us_form.png)

## Het bestand mysql-connector-java-5.1.39-bin.jar installeren {#install-mysql-connector-java-file}

Voer de volgende stappen uit, op alle auteur- en publicatieinstanties, om het bestand mysql-connector-java-5.1.39-bin.jar te installeren:

1. Navigeer naar `http://server:port/system/console/depfinder` en zoek naar het pakket com.mysql.jdbc.
1. Controleer in de kolom Geëxporteerd door of het pakket wordt geëxporteerd door een willekeurige bundel. Ga door als het pakket niet door enige bundel wordt uitgevoerd.
1. Navigeer naar `http://server:port/system/console/bundles` en klik **[!UICONTROL Install/Update]**.
1. Klik **[!UICONTROL Choose File]** en blader om het bestand mysql-connector-java-5.1.39-bin.jar te selecteren. Selecteer ook **[!UICONTROL Start Bundle]** en **[!UICONTROL Refresh Packages]** selectievakjes.
1. Klik **[!UICONTROL Install]** of **[!UICONTROL Update]**. Start de server opnieuw als de bewerking is voltooid.
1. (Alleen Windows) Schakel de systeemfirewall van uw besturingssysteem uit.

## Gegevens voorbereiden voor formuliermodel {#prepare-data-for-form-model}

Met de integratie van gegevens in AEM-formulieren kunt u verschillende gegevensbronnen configureren en verbinden. Nadat u een adaptief formulier hebt gegenereerd met behulp van het conversieproces, kunt u het formuliermodel definiëren op basis van een formuliergegevensmodel, XSD of een JSON-schema. U kunt een gegevensbestand, de Dynamica van Microsoft, of een andere derdedienst gebruiken om een model van vormgegevens tot stand te brengen.

Deze zelfstudie gebruikt de MySQL-database als bron voor het maken van een formuliergegevensmodel. Maak een schema in de database en voeg een **inhoudsopgave** toe aan het schema op basis van de velden die beschikbaar zijn in het adaptieve formulier.

![Voorbeeldgegevens mysql](assets/db_entries_sample_form.png)

U kunt de volgende verklaring gebruiken DDL om de **contactus** lijst in gegevensbestand tot stand te brengen.

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## Verbinding tussen AEM-instantie en database configureren {#configure-connection-between-aem-instance-and-database}

Voer de volgende configuratiestappen uit om een verbinding tussen instantie AEM en het gegevensbestand tot stand te brengen MYSQL:

1. Ga naar de configuratiepagina van AEM-webconsole op `http://server:port/system/console/configMgr`.
1. Zoek en klik om te openen **[!UICONTROL Apache Sling Connection Pooled DataSource]** in de bewerkingsmodus in de configuratie van de webconsole. Geef de waarden voor de eigenschappen op zoals in de volgende tabel wordt beschreven:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Eigenschap</strong></th> 
    <th><strong>Waarde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Naam gegevensbron</p></td> 
    <td><p>Een gegevensbronnaam voor het filtreren bestuurders van de gegevensbronpool.</p></td>
    </tr>
    <tr> 
    <td><p>JDBC-stuurprogrammaklasse</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>URI voor JDBC-verbinding</p></td> 
    <td><p>jdbc:mysql://[host]:[poort]/[schema_naam]</p></td>
    </tr>
    <tr> 
    <td><p>Gebruikersnaam</p></td> 
    <td><p>Een gebruikersnaam om handelingen voor databasetabellen te verifiëren en uit te voeren</p></td>
    </tr>
    <tr> 
    <td><p>Wachtwoord</p></td> 
    <td><p>Aan de gebruikersnaam gekoppeld wachtwoord</p></td>
    </tr>
    <tr> 
    <td><p>Transactieisolatie</p></td> 
    <td><p>READ_COMTED</p></td>
    </tr>
    <tr> 
    <td><p>Max. actieve verbindingen</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>Max. aantal inactieve verbindingen</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>Min. onbelaste verbindingen</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Oorspronkelijke grootte</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Max. wachttijd</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Testen op lenen</p></td> 
    <td><p>Ingeschakeld</p></td>
    </tr>
     <tr> 
    <td><p>Testen tijdens inactiviteit</p></td> 
    <td><p>Ingeschakeld</p></td>
    </tr>
     <tr> 
    <td><p>Validatiezoekopdracht</p></td> 
    <td><p>Voorbeelden zijn SELECT 1 (mysql), select 1 (dual), SELECT 1 (MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Time-out voor validatiezoekopdracht</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## Formuliergegevensmodel maken {#create-form-data-model}

Nadat u MYSQL als gegevensbron hebt geconfigureerd, voert u de volgende stappen uit om een formuliergegevensmodel te maken:

1. Navigeer in de auteur van AEM naar **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.

1. Tik **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. Geef in de **[!UICONTROL Create Form Data Model]** wizard **workflow_submit** op als naam voor het gegevensmodel van het formulier. Tik **[!UICONTROL Next]**.

1. Selecteer de MYSQL-gegevensbron die u in de vorige sectie hebt geconfigureerd en tik op **[!UICONTROL Create]**.

1. Tik **[!UICONTROL Edit]** en vouw de gegevensbron uit die in de linkerruit wordt vermeld om **contactus** lijst, **[!UICONTROL get]**, en de **[!UICONTROL insert]** diensten te selecteren, en **[!UICONTROL Add Selected]**.

   ![Voorbeeldgegevens mysql](assets/fdm_details_workfdlow_submit.png)

1. Selecteer het gegevensmodelobject in het rechterdeelvenster en tik op **[!UICONTROL Edit Properties]**. Selecteer **[!UICONTROL get]** en **[!UICONTROL insert]** van **[!UICONTROL Read Service]** **[!UICONTROL Write Service]** en drop-down lijsten. Geef de argumenten voor de leesservice op en tik op **[!UICONTROL Done]**.

1. Selecteer op het **[!UICONTROL Services]** tabblad de **[!UICONTROL get]** service en tik op **[!UICONTROL Edit Properties]**. Selecteer de **[!UICONTROL Output Model Object]**, schakel de **[!UICONTROL Return array]** schakeloptie uit en tik op de knop **[!UICONTROL Done]**.

1. Selecteer de **[!UICONTROL Insert]** service en tik op **[!UICONTROL Edit Properties]**. Selecteer het gereedschap **[!UICONTROL Input Model Object]** en tik op **[!UICONTROL Done]**.

1. Tik **[!UICONTROL Save]** om het formuliergegevensmodel op te slaan.

U kunt het model met voorbeeldformuliergegevens downloaden:

[Bestand ophalen](assets/DownloadedFormsPackage_1497728018502500.zip)

## Aangepaste formulieren genereren met JSON-binding {#generate-adaptive-forms-with-json-binding}

Met de service [Automated Forms Conversion kunt u het formulier](convert-existing-forms-to-adaptive-forms.md) Contact opnemen converteren [](#sample-adaptive-form) naar een adaptief formulier met gegevensbinding. Zorg ervoor dat u het **[!UICONTROL Generate adaptive form(s) without data bindings]** selectievakje niet inschakelt terwijl u het adaptieve formulier genereert.

![Aangepaste vorm met JSON-binding](assets/generate_af_with_data_bindings.png)

Selecteer het geconverteerde formulier **** Contact opnemen in de **[!UICONTROL output]** map in **[!UICONTROL Forms & Documents]** en tik op **[!UICONTROL Edit]**. Tik **[!UICONTROL Preview]** op waarden in de aangepaste formuliervelden en tik op **[!UICONTROL Submit]**.

Meld u aan bij de **crx-repository** en navigeer naar */content/forms/fp/admin/submit/data* om de verzonden waarden in JSON-indeling te bekijken. Hier volgen de voorbeeldgegevens in JSON-indeling wanneer u het omgezette adaptieve formulier **Contact opnemen** verzendt:

```json
{
  "afData": {
    "afUnboundData": {
      "data": {}
    },
    "afBoundData": {
      "data": {
        "name1": "Gloria",
        "email": "abc@xyz.com",
        "phone_number": "2346578965",
        "issue_description": "Test message"
      }
    },
    "afSubmissionInfo": {
      "computedMetaInfo": {},
      "stateOverrides": {},
      "signers": {},
      "afPath": "/content/dam/formsanddocuments/docs_conversion/output/sample_form_json",
      "afSubmissionTime": "20191204014007"
    }
  }
}
```

U moet nu een workflowmodel maken dat deze gegevens kan verwerken en verzenden naar de MYSQL-database met behulp van het formuliergegevensmodel dat u in de vorige secties hebt gemaakt.

## Een workflowmodel maken voor het verwerken van JSON-gegevens {#create-workflow-model}

Voer de volgende stappen uit om een workflowmodel te maken voor het verzenden van de adaptieve formuliergegevens naar de database:

1. Open de console Workflowmodellen. De standaard-URL is `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`.

1. Selecteer **[!UICONTROL Create]**, dan **[!UICONTROL Create Model]**. Het **[!UICONTROL Add Workflow Model]** dialoogvenster verschijnt.

1. Voer de **[!UICONTROL Title]** en **[!UICONTROL Name]** (optioneel) in. Bijvoorbeeld, **workflow_json_submit**. Tik **[!UICONTROL Done]** om het model te maken.

1. Selecteer het workflowmodel en tik **[!UICONTROL Edit]** op om het model in de bewerkingsmodus te openen. Tik op + en voeg **[!UICONTROL Invoke Form Data Model Service]** stap toe aan het workflowmodel.

1. Tik op de **[!UICONTROL Invoke Form Data Model Service]** stap en tik op ![Configureren](assets/configure_icon.png).

1. Selecteer op het **[!UICONTROL Form Data Model]** tabblad het formuliergegevensmodel dat u in het **[!UICONTROL Form Data Model path]** veld hebt gemaakt en selecteer een model in de **[!UICONTROL insert]** **[!UICONTROL Service]** vervolgkeuzelijst.

1. Selecteer op het **[!UICONTROL Input for Service]** tabblad **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** in de vervolgkeuzelijst de optie **[!UICONTROL Map input fields from input JSON]** Selectievakje, selecteer **[!UICONTROL Relative to payload]** en geef **data.xml** op als waarde voor het **[!UICONTROL Select input JSON document using]** veld.

1. Geef in de **[!UICONTROL Service Arguments]** sectie de volgende waarden op voor de argumenten van het formuliergegevensmodel:

   ![Formuliergegevensmodelservice aanroepen](assets/invoke_form_data_model_service.png)

   De velden van het formuliergegevensmodel, bijvoorbeeld contactus dot name, worden toegewezen aan **afData.afBoundData.data.name1**, die verwijst naar de JSON-schemabindingen voor het verzonden adaptieve formulier.

## Aangepaste formulierverzending configureren {#configure-adaptive-form-submission}

Voer de volgende stappen uit om het aangepaste formulier te verzenden naar het workflowmodel dat u in de vorige sectie hebt gemaakt:

1. Selecteer het geconverteerde formulier Contact opnemen in de **[!UICONTROL output]** map in **[!UICONTROL Forms & Documents]** en tik op **[!UICONTROL Edit]**.

1. Open adaptieve formuliereigenschappen door te tikken **[!UICONTROL Form Container]** en vervolgens te tikken op ![Configureren](assets/configure_icon.png).

1. Selecteer in de **[!UICONTROL Submission]** sectie **[!UICONTROL Invoke an AEM workflow]** in de **[!UICONTROL Submit Action]** vervolgkeuzelijst het workflowmodel dat u in de vorige sectie hebt gemaakt en geef in het **veld** data.xml **[!UICONTROL Data File Path]** op.

1. Tik op ![Opslaan](assets/save_icon.png) om de eigenschappen op te slaan.

1. Tik **[!UICONTROL Preview]** op waarden in de aangepaste formuliervelden en tik op **[!UICONTROL Submit]**. De ingediende waarden worden nu weergegeven in de MYSQL-databasetabel in plaats van in de **crx-opslagplaats**.

## Aangepast formulier configureren om waarden vooraf in te vullen vanuit de database

Voer de volgende stappen uit om adaptief formulier te configureren voor het vooraf invullen van waarden uit de MYSQL-database op basis van de primaire sleutel die in de tabel is gedefinieerd (in dit geval per e-mail):

1. Tik op het veld **E-mail** in het adaptieve formulier en tik op ![Bewerken-regel](assets/edit-rules.png).

1. Tik **[!UICONTROL Create]** en selecteer **[!UICONTROL is changed]** in de **[!UICONTROL Select State]** vervolgkeuzelijst in de **[!UICONTROL When]** sectie.

1. Selecteer in de **[!UICONTROL Then]** sectie **[!UICONTROL Invoke Service]** en **krijg** de service voor het formuliergegevensmodel dat u in een vorige sectie van dit artikel hebt gemaakt.

1. Selecteer **E-mail** in de **[!UICONTROL Input]** sectie en de overige drie gebieden van het model van vormgegevens, **Naam**, **Telefoonaantal**, en Beschrijving **van de** Uitgave in de **[!UICONTROL Output]** sectie. Tik **[!UICONTROL Done]** om de instellingen op te slaan.

   ![Voorinstellingen voor e-mail configureren](assets/email_prefill_settings.png)

   Hierdoor kunt u op basis van bestaande e-mailgegevens in de MYSQL-database de waarden voor de overige drie velden vooraf invullen in de **[!UICONTROL Preview]** modus van het adaptieve formulier. Als u bijvoorbeeld aya.tan@xyz.com opgeeft in het veld **E-mail** (op basis van bestaande gegevens in de sectie Formuliergegevensmodel [voorbereiden van dit artikel) en tab uit het veld, worden de overige drie velden,](#prepare-data-for-form-model) Naam **,** Telefoonnummer **en Beschrijving** van **** uitgave automatisch weergegeven in het aangepaste formulier.

U kunt het geconverteerde adaptieve voorbeeldformulier downloaden met:

[Bestand ophalen](assets/DownloadedFormsPackage_1498226829041200.zip)

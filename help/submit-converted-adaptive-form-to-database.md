---
title: De geconverteerde adaptieve formulieren met een JSON-schema naar database verzenden
description: Verzend de geconverteerde adaptieve formulieren met een JSON-schema naar de database door een formuliergegevensmodel te maken en ernaar te verwijzen in een AEM workflow.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: 5447b66f-9fac-476f-ab8a-9290bb1f9c0d
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---

# Adaptief formulier integreren met database door middel van AEM-workflow {#submit-forms-to-database-using-forms-portal}

Met de service automatede form conversion kunt u een niet-interactief PDF-formulier, een Acro-formulier of een XFA-formulier converteren naar een adaptief formulier. Tijdens het starten van het conversieproces kunt u een adaptief formulier genereren, met of zonder gegevensbindingen.

Als u een adaptief formulier wilt genereren zonder gegevensbindingen, kunt u het geconverteerde adaptieve formulier na conversie integreren met een formuliergegevensmodel, XML-schema of JSON-schema. Voor het formuliergegevensmodel moet u adaptieve formuliervelden handmatig binden met het formuliergegevensmodel. Als u echter een adaptief formulier genereert met gegevensbindingen, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden die beschikbaar zijn in het adaptieve formulier en het JSON-schema. Vervolgens kunt u het aangepaste formulier integreren met een door u gewenste database, gegevens in het formulier invullen en naar de database verzenden. Op dezelfde manier kunt u, nadat u de integratie met de database hebt voltooid, velden in het geconverteerde adaptieve formulier configureren om waarden op te halen uit de database en aangepaste formuliervelden vooraf invullen.

In de volgende afbeelding ziet u de verschillende fasen van het integreren van een geconverteerd adaptief formulier in een database:

![database-integratie](assets/integrate-adaptive-form-with-database.png)

In dit artikel worden de stapsgewijze instructies beschreven waarmee u al deze integratiefasen kunt uitvoeren.

## Voorwaarden {#pre-requisites}

* Een AEM 6.4- of 6.5-auteurinstantie instellen
* Installeren [nieuwste servicepack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) voor uw AEM
* Laatste versie van het AEM Forms-invoegpakket
* Configureren [automatede form conversion](configure-service.md)
* Stel een database in. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt het geconverteerde adaptieve formulier echter integreren met elke gewenste database.

## Monster van adaptief formulier {#sample-adaptive-form}

Als u geconverteerde adaptieve formulieren met een AEM workflow wilt integreren in de database, downloadt u het volgende voorbeeldbestand voor de PDF.

U kunt het voorbeeld van het contactformulier downloaden met:

[Bestand ophalen](assets/sample_contact_us_form.pdf)

Het PDF-bestand fungeert als invoer voor de service Automatede form conversion. De service converteert dit bestand naar een adaptief formulier. De volgende afbeelding toont de voorbeeldcontactgegevens van een formulier in PDF-indeling.

![aanvraagformulier voor een voorbeeldlening](assets/sample_contact_us_form.png)

## Het bestand mysql-connector-java-5.1.39-bin.jar installeren {#install-mysql-connector-java-file}

Voer de volgende stappen uit, op alle auteur- en publicatieinstanties, om het bestand mysql-connector-java-5.1.39-bin.jar te installeren:

1. Navigeren naar `http://server:port/system/console/depfinder` en zoek naar het pakket com.mysql.jdbc.
1. Controleer in de kolom Geëxporteerd door of het pakket wordt geëxporteerd door een willekeurige bundel. Ga door als het pakket niet door enige bundel wordt uitgevoerd.
1. Navigeren naar `http://server:port/system/console/bundles` en klik op **[!UICONTROL Install/Update]**.
1. Klikken **[!UICONTROL Choose File]** en bladert u om het bestand mysql-connector-java-5.1.39-bin.jar te selecteren. Selecteer ook **[!UICONTROL Start Bundle]** en **[!UICONTROL Refresh Packages]** selectievakjes.
1. Klikken **[!UICONTROL Install]** of **[!UICONTROL Update]**. Start de server opnieuw als de bewerking is voltooid.
1. (Alleen Windows) Schakel de systeemfirewall van uw besturingssysteem uit.

## Gegevens voorbereiden voor formuliermodel {#prepare-data-for-form-model}

Met AEM Forms Data Integration kunt u verschillende gegevensbronnen configureren en verbinden. Nadat u een adaptief formulier hebt gegenereerd met behulp van het conversieproces, kunt u het formuliermodel definiëren op basis van een formuliergegevensmodel, XSD of een JSON-schema. U kunt een database, Microsoft Dynamics of een andere service van derden gebruiken om een formuliergegevensmodel te maken.

Deze zelfstudie gebruikt de MySQL-database als bron voor het maken van een formuliergegevensmodel. Een schema maken in de database en toevoegen **contactus** tabel naar het schema op basis van de velden die beschikbaar zijn in het adaptieve formulier.

![Voorbeeldgegevens mysql](assets/db_entries_sample_form.png)

U kunt de volgende verklaring gebruiken DDL om tot de **contactus** tabel in de database.

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## Verbinding tussen AEM instantie en database configureren {#configure-connection-between-aem-instance-and-database}

Voer de volgende configuratiestappen uit om een verbinding tussen AEM instantie en het gegevensbestand tot stand te brengen MYSQL:

1. Ga naar AEM webconsoleconfiguratiepagina op `http://server:port/system/console/configMgr`.
1. Zoeken en klikken om te openen **[!UICONTROL Apache Sling Connection Pooled DataSource]** in geef wijze in de Configuratie van de Console van het Web uit. Geef de waarden voor de eigenschappen op zoals in de volgende tabel wordt beschreven:

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
    <td><p>Voorbeelden zijn SELECT 1(mysql), select 1 vanuit dual (oracle), SELECT 1 (MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Time-out voor validatiezoekopdracht</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## Formuliergegevensmodel maken {#create-form-data-model}

Nadat u MYSQL als gegevensbron hebt geconfigureerd, voert u de volgende stappen uit om een formuliergegevensmodel te maken:

1. Navigeer in AEM auteurinstantie naar **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.

1. Tik op **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. In de **[!UICONTROL Create Form Data Model]** wizard, specificeer **workflow_submit** als de naam voor het formuliergegevensmodel. Tik op **[!UICONTROL Next]**.

1. Selecteer de MYSQL-gegevensbron die u in de vorige sectie hebt geconfigureerd en tik **[!UICONTROL Create]**.

1. Tikken **[!UICONTROL Edit]** en breid de gegevensbron uit die in de linkerruit wordt vermeld om te selecteren **contactus** tabel, **[!UICONTROL get]**, en **[!UICONTROL insert]** services en tikken **[!UICONTROL Add Selected]**.

   ![Voorbeeldgegevens mysql](assets/fdm_details_workfdlow_submit.png)

1. Selecteer het gegevensmodelobject in het rechtervenster en tik op **[!UICONTROL Edit Properties]**. Selecteren **[!UICONTROL get]** en **[!UICONTROL insert]** van **[!UICONTROL Read Service]** en **[!UICONTROL Write Service]** vervolgkeuzelijsten. Geef de argumenten voor de leesservice op en tik op **[!UICONTROL Done]**.

1. In de **[!UICONTROL Services]** selecteert u de **[!UICONTROL get]** service en tikken **[!UICONTROL Edit Properties]**. Selecteer **[!UICONTROL Output Model Object]**, schakelt u de **[!UICONTROL Return array]** schakelen en tikken **[!UICONTROL Done]**.

1. Selecteer **[!UICONTROL Insert]** service en tikken **[!UICONTROL Edit Properties]**. Selecteer **[!UICONTROL Input Model Object]** en tikken **[!UICONTROL Done]**.

1. Tikken **[!UICONTROL Save]** om het formuliergegevensmodel op te slaan.

U kunt het model met voorbeeldformuliergegevens downloaden:

[Bestand ophalen](assets/DownloadedFormsPackage_1497728018502500.zip)

## Aangepaste formulieren genereren met JSON-binding {#generate-adaptive-forms-with-json-binding}

Gebruik de [Omzetten van automatede form conversion](convert-existing-forms-to-adaptive-forms.md) de [Formulier Contact met ons opnemen](#sample-adaptive-form) in een adaptief formulier met gegevensbinding. Zorg ervoor dat u de optie **[!UICONTROL Generate adaptive form(s) without data bindings]** selectievakje tijdens het genereren van het adaptieve formulier.

![Aangepaste vorm met JSON-binding](assets/generate_af_with_data_bindings.png)

Omgezette selecteren **Formulier Contact met ons opnemen** beschikbaar in **[!UICONTROL output]** map in **[!UICONTROL Forms & Documents]** en tikken **[!UICONTROL Edit]**. Tikken **[!UICONTROL Preview]**, voert u waarden in de aangepaste formuliervelden in en tikt u op **[!UICONTROL Submit]**.

Aanmelden bij **crx-repository** en navigeer naar */content/forms/fp/admin/submit/data* om de verzonden waarden weer te geven in JSON-indeling. Hieronder volgen de voorbeeldgegevens in de JSON-indeling wanneer u de omgezette gegevens verzendt **Contact opnemen** adaptief formulier:

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

1. Selecteren **[!UICONTROL Create]** vervolgens **[!UICONTROL Create Model]**. De **[!UICONTROL Add Workflow Model]** wordt weergegeven.

1. Voer de **[!UICONTROL Title]** en **[!UICONTROL Name]** (optioneel). Bijvoorbeeld: **workflow_json_submit**. Tikken **[!UICONTROL Done]** om het model te maken.

1. Selecteer het workflowmodel en tik op **[!UICONTROL Edit]** om het model te openen in de bewerkingsmodus. Tik + en voeg toe **[!UICONTROL Invoke Form Data Model Service]** stap naar het workflowmodel.

1. Tik op de knop **[!UICONTROL Invoke Form Data Model Service]** stap en tik ![Configureren](assets/configure_icon.png).

1. In de **[!UICONTROL Form Data Model]** selecteert u het formuliergegevensmodel dat u in het dialoogvenster **[!UICONTROL Form Data Model path]** veld en selecteer **[!UICONTROL insert]** van de **[!UICONTROL Service]** vervolgkeuzelijst.

1. In de **[!UICONTROL Input for Service]** tab, selecteert u **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** in de vervolgkeuzelijst selecteert u **[!UICONTROL Map input fields from input JSON]** selectievakje, selecteren **[!UICONTROL Relative to payload]** en **data.xml** als de waarde voor de **[!UICONTROL Select input JSON document using]** veld.

1. In de **[!UICONTROL Service Arguments]** de volgende waarden op voor de argumenten van het formuliergegevensmodel:

   ![Formuliergegevensmodelservice aanroepen](assets/invoke_form_data_model_service.png)

   De modelvelden van het formuliergegevensmodel, bijvoorbeeld de puntnaam van contactus, zijn toegewezen aan **afData.afBoundData.data.name1**, die verwijst naar de bindingen van het JSON-schema voor het ingediende adaptieve formulier.

## Aangepaste formulierverzending configureren {#configure-adaptive-form-submission}

Voer de volgende stappen uit om het aangepaste formulier te verzenden naar het workflowmodel dat u in de vorige sectie hebt gemaakt:

1. Selecteer het geconverteerde contactformulier dat beschikbaar is in het dialoogvenster **[!UICONTROL output]** map in **[!UICONTROL Forms & Documents]** en tikken **[!UICONTROL Edit]**.

1. Eigenschappen van adaptieve formulieren openen door te tikken **[!UICONTROL Form Container]** en tikt u vervolgens op ![Configureren](assets/configure_icon.png).

1. In de **[!UICONTROL Submission]** sectie, selecteert u **[!UICONTROL Invoke an AEM workflow]** van de **[!UICONTROL Submit Action]** vervolgkeuzelijst, selecteert u het workflowmodel dat u in de vorige sectie hebt gemaakt en geeft u **data.xml** in de **[!UICONTROL Data File Path]** veld.

1. Tikken ![Opslaan](assets/save_icon.png) om de eigenschappen op te slaan.

1. Tikken **[!UICONTROL Preview]**, voert u waarden in de aangepaste formuliervelden in en tikt u op **[!UICONTROL Submit]**. De verzonden waarden worden nu weergegeven in de MYSQL-databasetabel in plaats van **crx-repository**.

## Aangepast formulier configureren om waarden vooraf in te vullen vanuit de database

Voer de volgende stappen uit om adaptief formulier te configureren voor het vooraf invullen van waarden uit de MYSQL-database op basis van de primaire sleutel die in de tabel is gedefinieerd (in dit geval per e-mail):

1. Tik op de knop **E-mail** veld in het adaptieve formulier en tik ![Regel bewerken](assets/edit-rules.png).

1. Tikken **[!UICONTROL Create]** en selecteert u **[!UICONTROL is changed]** van de **[!UICONTROL Select State]** vervolgkeuzelijst in het dialoogvenster **[!UICONTROL When]** sectie.

1. In de **[!UICONTROL Then]** sectie, selecteert u **[!UICONTROL Invoke Service]** en **get** als de service voor het formuliergegevensmodel dat u in een vorige sectie van dit artikel hebt gemaakt.

1. Selecteren **E-mail** in de **[!UICONTROL Input]** en de overige drie velden van het formuliergegevensmodel, **Naam**, **Telefoonnummer**, en **Probleembeschrijving** in de **[!UICONTROL Output]** sectie. Tikken **[!UICONTROL Done]** om de instellingen op te slaan.

   ![Voorinstellingen voor e-mail configureren](assets/email_prefill_settings.png)

   Als gevolg hiervan kunt u op basis van bestaande e-mailadressen in de MYSQL-database de waarden voor de overige drie velden vooraf invullen in de **[!UICONTROL Preview]** modus van het adaptieve formulier. Als u bijvoorbeeld aya.tan@xyz.com opgeeft in het dialoogvenster **E-mail** veld (gebaseerd op bestaande gegevens in [Formuliergegevensmodel voorbereiden](#prepare-data-for-form-model) (deel van dit artikel) en de overige drie velden met een tab uit het veld; **Naam**, **Telefoonnummer**, en **Probleembeschrijving** automatisch in het adaptieve formulier worden weergegeven.

U kunt het geconverteerde adaptieve voorbeeldformulier downloaden met:

[Bestand ophalen](assets/DownloadedFormsPackage_1498226829041200.zip)

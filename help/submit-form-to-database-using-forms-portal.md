---
title: Aangepaste formulieren naar de database verzenden met Forms Portal
description: Het standaardmetamodel uitbreiden om patronen, validaties en entiteiten toe te voegen die specifiek zijn voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service voor automatische formulierconversie wordt uitgevoerd.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: c552f4073ac88ca9016a746116a27a5898df7f7d

---


# Aangepaste formulieren integreren met database via Forms Portal {#submit-forms-to-database-using-forms-portal}

Met de service voor automatische formulierconversie kunt u een niet-interactief PDF-formulier, een Acro-formulier of een op XFA gebaseerd PDF-formulier converteren naar een adaptief formulier. Tijdens het starten van het conversieproces kunt u een adaptief formulier genereren, met of zonder gegevensbindingen.

Als u een adaptief formulier wilt genereren zonder gegevensbindingen, kunt u het geconverteerde adaptieve formulier na conversie integreren met een formuliergegevensmodel, XML-schema of JSON-schema. Als u echter een adaptief formulier genereert met gegevensbindingen, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden die beschikbaar zijn in het adaptieve formulier en het JSON-schema. Vervolgens kunt u het adaptieve formulier integreren met een door u gewenste database, gegevens in het formulier invullen en naar de database verzenden met behulp van het Forms Portal.

In de volgende afbeelding ziet u de verschillende fasen van de integratie van een geconverteerd adaptief formulier in een database met Forms Portal:

![database-integratie](assets/database_integration.gif)

In dit artikel worden de stapsgewijze instructies beschreven waarmee u al deze integratiefasen kunt uitvoeren.

Het voorbeeld, dat in dit artikel wordt besproken, is een referentie-implementatie van aangepaste gegevens en metagegevensservices om een pagina Forms Portal met een database te integreren. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt de pagina Forms Portal echter integreren met elke gewenste database.

## Voorwaarden {#pre-requisites}

* Een instantie van AEM 6.4 of 6.5-auteurs instellen
* Installeer het [recentste de dienstpak](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) voor uw instantie AEM
* Laatste versie van het invoegpakket voor AEM Forms
* Service voor [automatische conversie van formulieren configureren](configure-service.md)
* Stel een database in. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt het geconverteerde adaptieve formulier echter integreren met elke gewenste database.

## Verbinding tussen AEM-instantie en database instellen {#set-up-connection-aem-instance-database}

Het instellen van een verbinding tussen een AEM-instantie en een MYSQL-database bestaat uit:

* [Een MYSQL-aansluitingspakket installeren](#install-mysql-connector-java-file)

* [Schema en tabellen maken in de database](#create-schema-and-tables-in-database)

* [Verbindingsinstellingen configureren](#configure-connection-between-aem-instance-and-database)

* [Het voorbeeldpakket instellen en configureren voor de integratie van Forms Portal](#set-up-and-configure-sample)

### Het bestand mysql-connector-java-5.1.39-bin.jar installeren {#install-mysql-connector-java-file}

Voer de volgende stappen uit, op alle auteur- en publicatieinstanties, om het bestand mysql-connector-java-5.1.39-bin.jar te installeren:

1. Ga naar http://[server]:[poort]/systeem/console/depfinder en zoek naar het pakket com.mysql.jdbc.
1. Controleer in de kolom Geëxporteerd door of het pakket wordt geëxporteerd door een willekeurige bundel. Ga door als het pakket niet door enige bundel wordt uitgevoerd.
1. Ga naar http://[server]:[poort]/systeem/console/bundles en klik op **[!UICONTROL Install/Update]**.
1. Klik **[!UICONTROL Choose File]** en blader om het bestand mysql-connector-java-5.1.39-bin.jar te selecteren. Selecteer ook **[!UICONTROL Start Bundle]** en **[!UICONTROL Refresh Packages]** selectievakjes.
1. Klik **[!UICONTROL Install]** of **[!UICONTROL Update]**. Start de server opnieuw als de bewerking is voltooid.
1. (Alleen Windows) Schakel de systeemfirewall van uw besturingssysteem uit.

### Schema en tabellen maken in de database {#create-schema-and-tables-in-database}

Voer de volgende stappen uit om schema en lijsten in het gegevensbestand tot stand te brengen:

1. Maak een schema in de database met de volgende SQL-instructie:

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   waarbij **formsportal** verwijst naar de naam van het schema.

1. Maak een **gegevenstabel** in het databaseschema met de volgende SQL-instructie:

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Maak een tabel met **metagegevens** in het databaseschema met de volgende SQL-instructie:

   ```sql
   CREATE TABLE `metadata` (
       `formPath` varchar(1000) DEFAULT NULL,
       `formType` varchar(100) DEFAULT NULL,
       `description` text,
       `formName` varchar(255) DEFAULT NULL,
       `owner` varchar(255) DEFAULT NULL,
       `enableAnonymousSave` varchar(45) DEFAULT NULL,
       `renderPath` varchar(1000) DEFAULT NULL,
       `nodeType` varchar(45) DEFAULT NULL,
       `charset` varchar(45) DEFAULT NULL,
       `userdataID` varchar(45) DEFAULT NULL,
       `status` varchar(45) DEFAULT NULL,
       `formmodel` varchar(45) DEFAULT NULL,
       `markedForDeletion` varchar(45) DEFAULT NULL,
       `showDorClass` varchar(255) DEFAULT NULL,
       `sling:resourceType` varchar(1000) DEFAULT NULL,
       `attachmentList` longtext,
       `draftID` varchar(45) DEFAULT NULL,
       `submitID` varchar(45) DEFAULT NULL,
       `id` varchar(60) NOT NULL,
       `profile` varchar(255) DEFAULT NULL,
       `submitUrl` varchar(1000) DEFAULT NULL,
       `xdpRef` varchar(1000) DEFAULT NULL,
       `agreementId` varchar(255) DEFAULT NULL,
       `nextSigners` varchar(255) DEFAULT NULL,
       `eSignStatus` varchar(45) DEFAULT NULL,
       `pendingSignID` varchar(45) DEFAULT NULL,
       `agreementDataId` varchar(255) DEFAULT NULL,
       `enablePortalSubmit` varchar(45) DEFAULT NULL,
       `submitType` varchar(45) DEFAULT NULL,
       `dataType` varchar(45) DEFAULT NULL,
       `jcr:lastModified` varchar(45) DEFAULT NULL,
       PRIMARY KEY (`id`),
       UNIQUE KEY `ID_UNIQUE` (`id`)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Maak een **aanvullende tabel met metagegevens** in het databaseschema met de volgende SQL-instructie:

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Maak een **tabel met opmerkingen** in het databaseschema met de volgende SQL-instructie:

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### Verbinding tussen AEM-instantie en database configureren {#configure-connection-between-aem-instance-and-database}

Voer de volgende configuratiestappen uit om een verbinding tussen instantie AEM en het gegevensbestand tot stand te brengen MYSQL:

1. Ga naar de pagina Configuratie AEM-webconsole op *http://[host]:[poort]/systeem/console/configMgr*.
1. Klik om te openen **[!UICONTROL Forms Portal Draft and Submission Configuration]** in bewerkingsmodus.
1. Geef de waarden voor de eigenschappen op zoals in de volgende tabel wordt beschreven:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Eigenschap</strong></th> 
    <th><strong>Beschrijving</strong></th>
    <th><strong>Waarde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Forms Portal Conceptgegevensservice</p></td> 
    <td><p>Id voor conceptgegevensservice</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal-service met metagegevens</p></td> 
    <td><p>Identificatiecode voor service met metagegevens van concept</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal verzendt Data Service</p></td> 
    <td><p>Id voor verzendgegevensservice</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal verzendt metagegevensservice</p></td> 
    <td><p>Id voor verzendmetagegevensservice</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Formulierportaal in afwachting van de service Gegevens ondertekenen</p></td> 
    <td><p>Identifier voor de dataservice in afwachting van ondertekening</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal Pending Sign Metadata Service</p></td> 
    <td><p>Identificatiecode voor de metagegevensservice in afwachting van ondertekening</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. Andere configuraties ongewijzigd laten en klikken **[!UICONTROL Save]**.
1. Zoek en klik om te openen **[!UICONTROL Apache Sling Connection Pooled DataSource]** in de bewerkingsmodus in de configuratie van de webconsole. Geef de waarden voor de eigenschappen op zoals in de volgende tabel wordt beschreven:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Eigenschap</strong></th> 
    <th><strong>Waarde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Naam gegevensbron</p></td> 
    <td><p>Een gegevensbronnaam voor het filtreren bestuurders van de gegevensbronpool. De steekproefimplementatie gebruikt FormsPortal als naam van de gegevensbron.</p></td>
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

### Het voorbeeld instellen en configureren {#set-up-and-configure-sample}

Voer de volgende stappen uit, op alle auteur en publiceer instanties, om de steekproef te installeren en te vormen:

1. Download het volgende **zip-pakket aem-fp-db-integration-sample-pkg-6.1.2.zip** naar uw bestandssysteem.

   [Bestand ophalen](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Ga naar AEM package manager op *http://[host]:[port]/crx/packmgr/*.
1. Klik op **[!UICONTROL Upload Package]**.
1. Blader naar het **zip-pakket aem-fp-db-integration-sample-pkg-6.1.2.zip** en klik op **[!UICONTROL OK]**.
1. Klik op **[!UICONTROL Install]** naast het pakket om het pakket te installeren.

## Het geconverteerde adaptieve formulier configureren voor Forms Portal-integratie {#configure-converted-adaptive-form-for-forms-portal-integration}

Voer de volgende stappen uit om het verzenden van aangepaste formulieren via de pagina Forms Portal mogelijk te maken:
1. [Voer de conversie](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) uit om een bronformulier om te zetten in een adaptief formulier.
1. Open het adaptieve formulier in de bewerkingsmodus.
1. Tik op Form Container en selecteer Configure ![Configure adptive form](assets/configure-adaptive-form.png).
1. Selecteer in de **[!UICONTROL Submission]** sectie een optie in de **[!UICONTROL Forms Portal Submit Action]** **[!UICONTROL Submit Action]** vervolgkeuzelijst.
1. Tik op Sjabloonbeleid ![](assets/edit_template_done.png) opslaan om de instellingen op te slaan.

## De pagina Forms Portal maken en configureren {#create-configure-forms-portal-page}

Voer de volgende stappen uit om een pagina van het Portaal van Forms tot stand te brengen en het te vormen zodat u adaptieve formulieren kunt voorleggen gebruikend deze pagina:

1. Meld u aan bij de AEM-auteur en tik op **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**.
1. Selecteer de locatie waar u de nieuwe pagina Forms Portal wilt opslaan en tik op **[!UICONTROL Create]** > **[!UICONTROL Page]**.
1. Selecteer de sjabloon voor de pagina, tik **[!UICONTROL Next]**, geef een titel op voor de pagina en tik op **[!UICONTROL Create]**.
1. Tik **[!UICONTROL Edit]** om de pagina te configureren.
1. Tik in de koptekst van de pagina op Sjabloon ![](assets/edit_template_sites.png) bewerken > **[!UICONTROL Edit Template]** om de sjabloon van de pagina te openen.
1. Tik op Container voor lay-out en tik op ![Sjabloonbeleid](assets/edit_template_policy.png)bewerken. Schakel op het **[!UICONTROL Allowed Components]** tabblad de opties **[!UICONTROL Document Services]** en **[!UICONTROL Document Services Predicates]** opties in en tik op Sjabloonbeleid ![](assets/edit_template_done.png)opslaan.
1. Voeg **[!UICONTROL Search & Lister]** een component op de pagina in. Hierdoor worden alle bestaande adaptieve formulieren die beschikbaar zijn op uw AEM-exemplaar weergegeven op de pagina.
1. Voeg **[!UICONTROL Drafts & Submissions]** een component op de pagina in. Er zijn twee tabbladen **[!UICONTROL Draft Forms]** en **[!UICONTROL Submitted Forms]** deze worden weergegeven op de pagina Forms Portal. Op het **[!UICONTROL Draft Forms]** tabblad wordt ook het geconverteerde adaptieve formulier weergegeven dat is gegenereerd met de stappen die worden vermeld in het [geconverteerde adaptieve formulier configureren voor Forms Portal-integratie](#configure-converted-adaptive-form-for-forms-portal-integration)

1. Tik **[!UICONTROL Preview]** op het geconverteerde adaptieve formulier, geef waarden op voor adaptieve formuliervelden en verzend het. De waarden die u opgeeft voor adaptieve formuliervelden worden verzonden naar de geïntegreerde database.

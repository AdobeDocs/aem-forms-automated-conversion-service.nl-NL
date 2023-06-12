---
title: Aangepaste formulieren naar database verzenden met Forms Portal
description: Breid het standaardmetamodel uit om patroon, validaties en entiteiten toe te voegen specifiek voor uw organisatie en configuraties toe te passen op adaptieve formuliervelden terwijl de service Automatede form conversion wordt uitgevoerd.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: 298d6c0641d7b416edb5b2bcd5fec0232f01f4c7
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Aangepaste formulieren integreren met database via Forms Portal {#submit-forms-to-database-using-forms-portal}

Met de service automatede form conversion kunt u een niet-interactief PDF-formulier, een Acro-formulier of een XFA-formulier converteren naar een adaptief formulier. Tijdens het starten van het conversieproces kunt u een adaptief formulier genereren, met of zonder gegevensbindingen.

Als u een adaptief formulier wilt genereren zonder gegevensbindingen, kunt u het geconverteerde adaptieve formulier na conversie integreren met een formuliergegevensmodel, XML-schema of JSON-schema. Als u echter een adaptief formulier genereert met gegevensbindingen, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden die beschikbaar zijn in het adaptieve formulier en het JSON-schema. Vervolgens kunt u het adaptieve formulier integreren met een door u gewenste database, gegevens in het formulier invullen en het naar de database verzenden via de Forms Portal.

In de volgende afbeelding ziet u de verschillende fasen van de integratie van een geconverteerd adaptief formulier in een database met Forms Portal:

![database-integratie](assets/database_integration.gif)

In dit artikel worden de stapsgewijze instructies beschreven waarmee u al deze integratiefasen kunt uitvoeren.

Het voorbeeld, dat in dit artikel wordt besproken, is een referentie-implementatie van aangepaste gegevens en metagegevensservices om een Forms Portal-pagina met een database te integreren. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt de pagina Forms Portal echter integreren met elke gewenste database.

## Voorwaarden {#pre-requisites}

* Een AEM 6.4- of 6.5-auteurinstantie instellen
* Installeren [nieuwste servicepack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) voor uw AEM
* Laatste versie van het AEM Forms-invoegpakket
* Configureren [automatede form conversion](configure-service.md)
* Stel een database in. De database die wordt gebruikt in de voorbeeldimplementatie is MySQL 5.6.24. U kunt het geconverteerde adaptieve formulier echter integreren met elke gewenste database.

## Verbinding tussen AEM instantie en database instellen {#set-up-connection-aem-instance-database}

Het instellen van een verbinding tussen een AEM instantie en een MYSQL-database bestaat uit:

* [Een MYSQL-aansluitingspakket installeren](#install-mysql-connector-java-file)

* [Schema en tabellen maken in de database](#create-schema-and-tables-in-database)

* [Verbindingsinstellingen configureren](#configure-connection-between-aem-instance-and-database)

* [Voorbeeldpakket instellen en configureren voor integratie met Forms Portal](#set-up-and-configure-sample)

### Het bestand mysql-connector-java-5.1.39-bin.jar installeren {#install-mysql-connector-java-file}

Voer de volgende stappen uit, op alle auteur- en publicatieinstanties, om het bestand mysql-connector-java-5.1.39-bin.jar te installeren:

1. Ga naar http://[server]:[poort]/system/console/depfinder en zoek naar het pakket com.mysql.jdbc.
1. Controleer in de kolom Geëxporteerd door of het pakket wordt geëxporteerd door een willekeurige bundel. Ga door als het pakket niet door enige bundel wordt uitgevoerd.
1. Ga naar http://[server]:[poort]/systeem/console/bundels en klik op **[!UICONTROL Install/Update]**.
1. Klikken **[!UICONTROL Choose File]** en bladert u om het bestand mysql-connector-java-5.1.39-bin.jar te selecteren. Selecteer ook **[!UICONTROL Start Bundle]** en **[!UICONTROL Refresh Packages]** selectievakjes.
1. Klikken **[!UICONTROL Install]** of **[!UICONTROL Update]**. Start de server opnieuw als de bewerking is voltooid.
1. (Alleen Windows) Schakel de systeemfirewall van uw besturingssysteem uit.

### Schema en tabellen maken in de database {#create-schema-and-tables-in-database}

Voer de volgende stappen uit om schema en lijsten in het gegevensbestand tot stand te brengen:

1. Maak een schema in de database met de volgende SQL-instructie:

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   waar **formsportief** verwijst naar de naam van het schema.

1. Een **data** tabel in het databaseschema met behulp van de volgende SQL-instructie:

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Een **metagegevens** tabel in het databaseschema met behulp van de volgende SQL-instructie:

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

1. Een **additionalmetadatable** tabel in het databaseschema met behulp van de volgende SQL-instructie:

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Een **opmerkelijk** tabel in het databaseschema met behulp van de volgende SQL-instructie:

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### Verbinding tussen AEM instantie en database configureren {#configure-connection-between-aem-instance-and-database}

Voer de volgende configuratiestappen uit om een verbinding tussen AEM instantie en het gegevensbestand tot stand te brengen MYSQL:

1. Ga naar AEM webconsoleconfiguratiepagina op *http://[host]:[poort]/system/console/configMgr*.
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
    <td><p>Forms Portal Draft Metadata Service</p></td> 
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
    <td><p>Forms Portal in afwachting van Sign Data Service</p></td> 
    <td><p>Identifier voor de dataservice in afwachting van ondertekening</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal in afwachting van Sign Metadata Service</p></td> 
    <td><p>Identificatiecode voor de metagegevensservice in afwachting van ondertekening</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. Andere configuraties ongewijzigd laten en klikken **[!UICONTROL Save]**.
1. Zoeken en klikken om te openen **[!UICONTROL Apache Sling Connection Pooled DataSource]** in geef wijze in de Configuratie van de Console van het Web uit. Geef de waarden voor de eigenschappen op zoals in de volgende tabel wordt beschreven:

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
    <td><p>Voorbeelden zijn SELECT 1(mysql), select 1 vanuit dual (oracle), SELECT 1 (MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Time-out voor validatiezoekopdracht</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

### Het voorbeeld instellen en configureren {#set-up-and-configure-sample}

Voer de volgende stappen uit, op alle auteur en publiceer instanties, om de steekproef te installeren en te vormen:

1. Download het volgende **aem-fp-db-integration-sample-pkg-6.1.2.zip** aan uw bestandssysteem te verpakken.

[Bestand ophalen](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Ga naar AEM pakketbeheer op *http://[host]:[poort]/crx/packmgr/*.
1. Klik op **[!UICONTROL Upload Package]**.
1. Bladeren om de **aem-fp-db-integration-sample-pkg-6.1.2.zip** verpakken en klikken **[!UICONTROL OK]**.
1. Klikken **[!UICONTROL Install]** naast het pakket om het pakket te installeren.

## Het geconverteerde adaptieve formulier configureren voor Forms Portal-integratie {#configure-converted-adaptive-form-for-forms-portal-integration}

Voer de volgende stappen uit om het verzenden van aangepaste formulieren via de Forms Portal-pagina mogelijk te maken:
1. [De conversie uitvoeren](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) om een bronformulier om te zetten in een adaptief formulier.
1. Open het adaptieve formulier in de bewerkingsmodus.
1. Tik op Form Container en selecteer Configure ![Bijbehorende vorm configureren](assets/configure-adaptive-form.png).
1. In de **[!UICONTROL Submission]** sectie, selecteert u **[!UICONTROL Forms Portal Submit Action]** van de **[!UICONTROL Submit Action]** vervolgkeuzelijst.
1. Tikken ![Sjabloonbeleid opslaan](assets/edit_template_done.png) om de instellingen op te slaan.

## De pagina Forms Portal maken en configureren {#create-configure-forms-portal-page}

Voer de volgende stappen uit om een Forms Portal-pagina te maken en deze zo te configureren dat u adaptieve formulieren kunt verzenden met deze pagina:

1. Meld u aan bij de AEM auteur en tik op **[!UICONTROL Adobe Experience Manager]** >  **[!UICONTROL Sites]**.
1. Selecteer de locatie waar u de nieuwe Forms Portal-pagina wilt opslaan en tik op **[!UICONTROL Create]** > **[!UICONTROL Page]**.
1. Selecteer de sjabloon voor de pagina en tik op **[!UICONTROL Next]** geeft u een titel voor de pagina op en tikt u op **[!UICONTROL Create]**.
1. Tikken **[!UICONTROL Edit]** om de pagina te configureren.
1. Tik in de paginakoptekst op ![Sjabloon bewerken](assets/edit_template_sites.png)  > **[!UICONTROL Edit Template]** om de sjabloon van de pagina te openen.
1. Tik op de container voor lay-out en tik op ![Sjabloonbeleid bewerken](assets/edit_template_policy.png). In de **[!UICONTROL Allowed Components]** tab, inschakelen **[!UICONTROL Document Services]** en **[!UICONTROL Document Services Predicates]** en tikken ![Sjabloonbeleid opslaan](assets/edit_template_done.png).
1. Invoegen **[!UICONTROL Search & Lister]** op de pagina. Hierdoor worden alle bestaande adaptieve formulieren die beschikbaar zijn op het AEM weergegeven op de pagina.
1. Invoegen **[!UICONTROL Drafts & Submissions]** op de pagina. Twee tabbladen, **[!UICONTROL Draft Forms]** en **[!UICONTROL Submitted Forms]**, weergegeven op de pagina Forms Portal. De **[!UICONTROL Draft Forms]** wordt ook het geconverteerde adaptieve formulier weergegeven dat is gegenereerd met de stappen vermeld in [Het geconverteerde adaptieve formulier configureren voor Forms Portal-integratie](#configure-converted-adaptive-form-for-forms-portal-integration)

1. Tikken **[!UICONTROL Preview]** tikken op het geconverteerde adaptieve formulier, waarden opgeven voor adaptieve formuliervelden en verzenden. De waarden die u opgeeft voor adaptieve formuliervelden worden verzonden naar de geïntegreerde database.

---
title: De service voor automatische conversie van formulieren configureren
description: Klaar uw AEM instantie om de dienst van de Automatede form conversion te gebruiken
translation-type: tm+mt
source-git-commit: 741ff89370a5215b70d90c49eea220171efe9339
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 7%

---


# De service voor automatische conversie van formulieren configureren {#about-this-help}

In deze Help wordt beschreven hoe een AEM beheerder de service Automatede form conversion kan configureren om de conversie van zijn PDF forms naar adaptieve formulieren te automatiseren. Deze hulp is voor IT en AEM beheerders bij uw organisatie. De verstrekte informatie is gebaseerd op de veronderstelling dat iedereen die deze Hulp leest met de volgende technologieën vertrouwd is:

* Adobe Experience Manager- en AEM-pakketten installeren, configureren en beheren,

* Linux- en Microsoft Windows-besturingssystemen gebruiken

* SMTP-mailservers configureren

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service** -->

## Onboarding{#onboarding}

De service is gratis beschikbaar voor AEM 6.4 Forms en AEM 6.5 Forms On-Premise-termijnklanten en Adobe Managed Service Enterprise-klanten. U kunt contact opnemen met het Adobe-verkoopteam of uw Adobe-vertegenwoordiger om toegang tot de service aan te vragen.

Adobe maakt toegang voor uw organisatie mogelijk en biedt de vereiste rechten aan de persoon die is aangewezen als beheerder in uw organisatie. De beheerder kan toegang verlenen aan de AEM Forms-ontwikkelaars (gebruikers) van uw organisatie om verbinding te maken met de service.

## Vereisten {#prerequisites}

U vereist het volgende om de Dienst van de Automatede form conversion te gebruiken:

* De dienst van de automatede form conversion wordt toegelaten voor uw organisatie
* Een Adobe ID-account met beheerdersrechten voor de conversieservice
* Een up-to-date AEM 6.4 of AEM 6.5-auteurinstantie met de nieuwste AEM Service Pack
* Een AEM gebruiker (op uw AEM) die lid is van een formulier-gebruikersgroep

## De omgeving {#setuptheservice} instellen

Voordat u de service gebruikt, moet u de AEM auteur voorbereiden om verbinding te maken met de service die wordt uitgevoerd op Adobe Cloud. Voer de volgende stappen in de vermelde reeks uit om uw exemplaar voor de service voor te bereiden:

1. [Download en installeer AEM 6.4 of AEM 6.5](#aemquickstart)
1. [Download en installeer de nieuwste AEM Service Pack](#servicepack)
1. [Download en installeer het nieuwste AEM Forms Add-on-pakket](#downloadaemformsaddon)
1. (optioneel) [Download en installeer het nieuwste connectorpakket](#installConnectorPackage)
1. [Aangepaste thema&#39;s en sjablonen maken](#referencepackage)

### Download en installeer AEM 6.4 of AEM 6.5 {#aemquickstart}


De de dienstlooppas van de automatede form conversion op AEM auteursinstantie. U hebt AEM 6.4 of AEM 6.5 nodig om een AEM auteur-instantie in te stellen. Als u niet AEM, download het van de volgende plaatsen:

* Als u een bestaande AEM klant bent, downloadt u AEM 6.4 of AEM 6.5 van [Adobe-licentiewebsite](http://licensing.adobe.com).

* Als u een partner van de Adobe bent, gebruik [Adobe Partner Training Programma](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) om AEM 6.4 of AEM 6.5 te verzoeken.

Nadat u AEM downloadt, voor instructies aan opstelling een AEM auteursinstantie, zie [opstellen en handhaven](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).

### Download en installeer AEM nieuwste Service Pack {#servicepack}

Download en installeer de nieuwste AEM Service Pack. Voor gedetailleerde instructies, zie, of [AEM 6.4 de Nota&#39;s van de Versie van het Pak ](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) of [AEM 6.5 de Nota&#39;s van de Versie van het Pak van de Dienst ](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html).

### AEM Forms-invoegtoepassing downloaden en installeren {#downloadaemformsaddon}

Een AEM-exemplaar bevat basisfuncties voor formulieren. Voor de conversieservice zijn alle mogelijkheden van AEM Forms vereist. Download en installeer het invoegpakket voor AEM Forms om alle mogelijkheden van AEM Forms te benutten. Het pakket is vereist om de conversieservice in te stellen en uit te voeren. Zie [Mogelijkheden voor het vastleggen van gegevens installeren en configureren.](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> Zorg ervoor dat u de verplichte configuraties na de installatie uitvoert nadat u het invoegpakket hebt geïnstalleerd.


### (Optioneel) Download en installeer het aansluitingspakket {#installConnectorPackage}

Het aansluitpakket biedt vroege toegang tot de [Auto-Detection logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) functies en verbeteringen die zijn geleverd in release AFC-2020.03.1. Installeer het pakket niet als u geen functie en verbeteringen in AFC-2020.03.1 nodig hebt.  U kunt [het schakelaarpakket van AEM Pakket Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1) downloaden.


### Aangepaste thema&#39;s en sjablonen maken {#referencepackage}

Als u AEM start in [productiemodus](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) (geen samplcontent runmode), worden de referentiepakketten niet geïnstalleerd. De referentiepakketten bevatten voorbeeldthema&#39;s en sjablonen. Voor de service automatede form conversion zijn ten minste één thema en één sjabloon nodig om een PDF forms om te zetten in een adaptief formulier. Creeer een douanethema en een malplaatje van uw en punt [de dienstconfiguratie](#configure-the-cloud-service) om douanesjablonen en thema&#39;s te gebruiken alvorens de dienst te gebruiken.

## Service configureren {#configure-the-service}

Voordat u verdergaat om de service te configureren en uw lokale instantie te verbinden met de service die wordt uitgevoerd op Adobe Cloud, dient u meer te weten te komen over de personen en rechten die nodig zijn om verbinding te maken met de service. De dienst gebruikt twee verschillende types van persona&#39;s, beheerders en ontwikkelaars:

* **Beheerders**: Beheerders zijn verantwoordelijk voor het beheer van Adobe-software en -services voor hun organisatie. Beheerders verlenen toegang aan ontwikkelaars in hun organisatie om verbinding te maken met de service Automatede form conversion die wordt uitgevoerd op Adobe Cloud. Wanneer een beheerder is ingericht voor een organisatie, ontvangt de beheerder een e-mail met titel **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**. Als u een beheerder bent, controleer uw brievenbus voor e-mail met bovengenoemde titel en ga aan [verlenen toegang tot ontwikkelaars van uw organisatie](#adduseranddevs) te werk.

![e-mail voor toegangsbeheer](assets/admin-console-adobe-io-access-grantedx75.png)

* **Ontwikkelaars**: Een ontwikkelaar maakt verbinding met een lokale AEM Forms-auteurinstantie met een Automatede form conversion-service die wordt uitgevoerd op Adobe Cloud. Wanneer een beheerder rechten toekent aan een ontwikkelaar om verbinding te maken met de service Automatede form conversion, wordt een e-mail met de titel U hebt nu toegang tot ontwikkelaars om de integratie van de Adobe API voor uw organisatie te beheren, verzonden naar de ontwikkelaar. Als u een ontwikkelaar bent, controleert u uw postvak op e-mail met bovengenoemde titel en gaat u verder naar [Sluit uw lokale AEM aan op de service Automatede form conversion op Adobe Cloud.](#connectafcadobeio)

![ontwikkel toegang verlenen e-mail](assets/email-developer-accessx94.png)

### (Alleen voor beheerders) Toegang verlenen aan ontwikkelaars van uw organisatie {#adduseranddevs}

Nadat Adobe toegang voor uw organisatie toelaat en vereiste voorrechten aan de beheerder verstrekt, kan de beheerder zich aanmelden in Admin Console (gedetailleerde instructies hieronder), een profiel creëren, en ontwikkelaars toevoegen aan het profiel. Ontwikkelaars kunnen een lokale versie van AEM Forms verbinden met de service Automatede forms conversion op Adobe Cloud.

De ontwikkelaars zijn leden van uw organisatie die wordt aangewezen om de omzettingsdienst in werking te stellen. Alleen ontwikkelaars die zijn toegevoegd aan het serviceprofiel Adobe Automatede form conversion hebben het recht om de service Automatede form conversion te gebruiken. Voer de onderstaande stappen uit om een profiel te maken en er ontwikkelaars aan toe te voegen. Er is minimaal één profiel vereist om vereiste toegang te verlenen aan ontwikkelaars van uw organisatie:

1. Meld u aan bij [Admin Console](https://adminconsole.adobe.com/). Gebruik **Adobe ID** van beheerder provisioned om de dienst van de Automatede form conversion aan login te gebruiken. Geen andere id of Federated ID om u aan te melden.
1. Klik op de optie **[!UICONTROL Automated Forms Conversion]**.
1. Klik op **[!UICONTROL New Profile]** op het tabblad **[!UICONTROL Products]**.
1. Geef **[!UICONTROL Name]**, **[!UICONTROL Display Name]** en **[!UICONTROL Description]** op voor het profiel. Klik op **[!UICONTROL Done]**. Er wordt een profiel gemaakt.

   ![Geef details op voor het nieuwe profiel.](assets/create-new-profile-details.png)

1. Voeg ontwikkelaar toe aan het profiel. U voegt als volgt de ontwikkelaars toe:
   1. Navigeer in [Admin Console](https://adminconsole.adobe.com/enterprise) naar het tabblad Overzicht.
   1. Klik op **[!UICONTROL Assign Developers]** op de vereiste productkaart.
   1. Voer het e-mailadres en (optioneel) de naam en achternaam van de ontwikkelaar in.
   1. Selecteer productprofielen. Tik op **[!UICONTROL Save]**.

Herhaal bovenstaande stappen voor alle gebruikers.  Zie [Ontwikkelaars beheren](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor meer informatie over het toevoegen van ontwikkelaars.

Nadat een beheerder ontwikkelaars heeft toegevoegd aan het Adobe I/O-profiel, worden de ontwikkelaars via e-mail op de hoogte gesteld. Nadat ontwikkelaars de e-mail hebben ontvangen, kunnen ze een lokale AEM Forms-instantie verbinden met de service Automatede form conversion op Adobe Cloud[.](#connectafcadobeio)

### (Alleen voor ontwikkelaars) Sluit uw lokale AEM Forms-instantie aan op de service Automatede forms conversion op Adobe Cloud {#connectafcadobeio}

Nadat een beheerder u ontwikkelaarstoegang verleent, kunt u uw lokale instantie van AEM Forms met de dienst verbinden van de Automatede form conversion die op Adobe Cloud loopt. Voer de volgende stappen in de vermelde reeks uit om uw AEM Forms-instantie te verbinden met de service:

* [E-mailmeldingen configureren](configure-service.md#configureemailnotification)
* [Gebruiker toevoegen aan de groep met gebruikers van het formulier](#adduserstousergroup)
* [Openbare certificaten verkrijgen](#obtainpubliccertificates)
* [De service-API&#39;s configureren in de Adobe Developer Console](#createintegration)
* [De cloudservice configureren](configure-service.md#configure-the-cloud-service)

#### E-mailmelding {#configureemailnotification} configureren

De service automatede form conversion gebruikt de Dagelijkse CQ-mailservice om e-mailberichten te verzenden. Deze e-mailmeldingen bevatten informatie over geslaagde of mislukte conversies. Sla deze stappen over als u geen melding wilt ontvangen. Voer de volgende stappen uit om de Day CQ Mail Service te configureren:

1. Ga naar AEM configuratiemanager op `http://localhost:4502/system/console/configMgr`
1. Open de configuratie van de Day CQ Mail Service. Geef een waarde op voor de velden **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]** en **[!UICONTROL From address]**. Klik op **[!UICONTROL Save]**.

   U kunt contact opnemen met uw e-mailserviceprovider of IT-beheerder voor informatie over de hostnaam en poort van SMTP-server. U kunt elk geldig e-mailadres gebruiken in het veld Van. Bijvoorbeeld notification@example.com of donotreply@example.com.

1. Open de **[!UICONTROL Day CQ Link Externalizer]** configuratie. Geef in het veld **[!UICONTROL Domains]** de werkelijke hostnaam of het werkelijke IP-adres en het poortnummer op voor lokale instanties, auteurs en publicatieinstanties. Klik op **[!UICONTROL Save]**.

#### Gebruiker toevoegen aan de groep gebruikers van het formulier {#adduserstousergroup}

Geef een e-mailadres op in het profiel van de AEM gebruiker die is aangewezen om de service uit te voeren. Zorg ervoor dat de gebruiker lid is van de [notatie gebruiker](https://helpx.adobe.com/experience-manager/6-4/forms/using/forms-groups-privileges-tasks.html) groep. E-mails worden verzonden naar het e-mailadres van de gebruiker die de conversie uitvoert. U kunt als volgt een e-mailadres voor de gebruiker opgeven en gebruiker toevoegen aan de gebruikersgroep Formulieren:

1. Meld u als AEM beheerder aan bij de auteur-instantie van AEM Forms. Gebruik uw lokale AEM om u aan te melden. Gebruik Adobe ID niet om u aan te melden. Tik **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Selecteer een gebruiker die is aangewezen om de conversieservice uit te voeren en op **[!UICONTROL Properties]** te tikken. De pagina Gebruikersinstellingen bewerken wordt geopend.
1. Geef een e-mailadres op in het veld **[!UICONTROL Email]** en tik **[!UICONTROL Save]**. De e-mails worden naar het opgegeven e-mailadres verzonden wanneer de conversie is voltooid of mislukt.
1. Tik op het tabblad **Groepen**. Typ en selecteer op het tabblad Groep selecteren de groep **forms-users**. Tik **Opslaan en sluiten**. De gebruiker is nu lid van de groep met gebruikers van het formulier.

#### Openbare certificaten verkrijgen {#obtainpubliccertificates}

Met een openbaar certificaat kunt u uw profiel verifiëren op Adobe I/O.

1. Meld u aan bij de AEM Forms-auteur. Ga naar **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Tik op **[!UICONTROL Create]**. De pagina **[!UICONTROL Adobe IMS Technical Account Configuration]** wordt weergegeven.

   ![De pagina Configuratie van de technische account van Adobe IMS](assets/adobe-ims-technical-account-configuration.png)

1. Selecteer **[!UICONTROL Automated Forms Conversion Service]** in Cloudoplossing.

1. Selecteer het selectievakje **[!UICONTROL Create new certificate]** en geef een alias op. De alias fungeert als naam voor het dialoogvenster. Tik op **[!UICONTROL Create certificate]**. Er wordt een dialoogvenster weergegeven. Klik op **[!UICONTROL OK]**. Het certificaat wordt gemaakt.

1. Tik **[!UICONTROL Download Public Key]** en sla het certificaatbestand *AEM-Adobe-IMS.crt* op uw computer op. Het certificaatbestand wordt gebruikt om de service-API&#39;s op de Adobe Developer Console[ te configureren. ](#createintegration) Tik op **[!UICONTROL Next]**.

1. Geef het volgende op:

   * Titel: Geef een titel op.
   * Autorisatieserver: [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)\

   Laat de overige velden voorlopig leeg (later te verstrekken). Laat de pagina open.

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### De service-API&#39;s configureren in de Adobe Developer Console {#createintegration}

Om de dienst van de Automatede form conversion te gebruiken, creeer een project en voeg Geautomatiseerde de Dienst API van de Configuratie van Forms aan het project op de Console van de Ontwikkelaar van Adobe toe. De integratie genereert API Key, Client Secret, Payload (JWT).

1. Meld u aan bij [https://console.adobe.io/](https://console.adobe.io/). Gebruik uw Adobe ID, ontwikkelaarsaccount die uw beheerder heeft ingericht om u aan te melden bij de Adobe I/O-console.
1. Selecteer uw organisatie in de rechterbovenhoek. Neem contact op met de beheerder als u uw organisatie niet kent.
1. Tik op **[!UICONTROL Create new project]**. Er verschijnt een scherm om aan de slag te gaan met uw nieuwe project. Tik op **[!UICONTROL Add API]**. Er verschijnt een scherm met een lijst van alle API&#39;s die voor uw account zijn ingeschakeld.
1. Selecteer **[!UICONTROL Automated Forms Conversion service]** en tik **[!UICONTROL Next]**. Er verschijnt een scherm om de API te configureren.
1. Selecteer de optie [!UICONTROL Upload your public key], upload het bestand AEM-Adobe-IMS.crt dat u hebt gedownload in de sectie [Openbare certificaten verkrijgen](#obtainpubliccertificates) en tik op **[!UICONTROL Next]**. De optie Create a new Service Account (JWT) credential wordt weergegeven. Tik op **[!UICONTROL Next]**.
1. Selecteer een productprofiel en tik **[!UICONTROL Save configured API]**. Selecteer het profiel dat is gemaakt terwijl [toegang wordt verleend aan ontwikkelaars van uw organisatie](#adduseranddevs). Neem contact op met de beheerder als u niet weet welk profiel u moet selecteren.
1. Tik op **[!UICONTROL Service Account (JWT)]** om de API-sleutel, het clientgeheim en andere informatie weer te geven die nodig is om uw lokale AEM-instantie aan te sluiten op de service Automatede form conversion. De informatie op de pagina wordt gebruikt om configuratie IMS op uw lokale machine tot stand te brengen.

1. Open de pagina van de Configuratie IMS op uw lokale instantie. U hebt de pagina open gelaten aan het einde van de sectie voor [Openbaar certificaat verkrijgen](#obtainpubliccertificates).

   ![Titel, API-sleutel, clientgeheim en payload opgeven  ](assets/ims-configuration-details.png)

1. Geef API-sleutel en clientgeheim op de technische pagina Adobe IMS op. Gebruik de waarden die op de de consolepagina van de Ontwikkelaar van de Adobe op de Rekening van de Dienst (JWT) worden gespecificeerd.

   >[!NOTE]
   >
   >
   >Voor nuttige lading, gebruik de code die op het Generate JWT lusje van de pagina van de Rekening van de Dienst (JWT) van de Console van de Ontwikkelaar van Adobe wordt verstrekt.

1. Tik op **[!UICONTROL Save]**. De IMS-configuratie wordt gemaakt.

   >[!CAUTION]
   >
   >Maak slechts één IMS-configuratie. Maak niet meer dan één IMS-configuratie.

1. Selecteer de IMS-configuratie en tik **[!UICONTROL Check Health]**. Er wordt een dialoogvenster weergegeven. Tik op **[!UICONTROL Check]**. Bij een geslaagde verbinding wordt het bericht *Token retrieved successfully* weergegeven.

   ![Bij een geslaagde verbinding wordt het bericht met succes opgehaalde token weergegeven.  ](assets/health-check.png)

   <br/> <br/>

#### De cloudservice {#configure-the-cloud-service} configureren

Maak een cloudserviceconfiguratie om uw AEM aan te sluiten op de conversieservice. U kunt hiermee ook een sjabloon, thema en formulierfragmenten opgeven voor conversie. U kunt meerdere configuraties voor cloudservices maken, afzonderlijk voor elke set formulieren. U kunt bijvoorbeeld een aparte configuratie voor de formulieren van de verkoopafdeling en een aparte configuratie voor de formulieren voor klantenondersteuning hebben. Voer de volgende stappen uit om een configuratie van de wolkendienst tot stand te brengen:

1. Tik in uw AEM Forms-instantie op **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**.
1. Tik op de map **[!UICONTROL Global]** en tik **[!UICONTROL Create]**. De pagina om de configuratie van de Automatede form conversion tot stand te brengen verschijnt. De configuratie wordt gemaakt in de map Global. U kunt de configuratie ook maken in een andere map die al bestaat of een nieuwe map voor uw configuraties maken.

1. Geef op de pagina **[!UICONTROL Create Automated Forms Conversion Configuration]** een waarde op voor de volgende velden en tik **[!UICONTROL Next]**.

   | Veld | Beschrijving |
   |--- |--- |
   | Titel | Unieke titel voor de configuratie. De titel wordt weergegeven in de gebruikersinterface waarmee de conversie wordt gestart. |
   | Naam | Unieke naam voor de configuratie. De configuratie wordt met de opgegeven naam opgeslagen in de CRX-gegevensopslagruimte. De naam kan identiek zijn aan de titel. |
   | Locatie miniatuur | Locatie van de miniatuur voor de configuratie. |
   | Service-URL | URL van de service Automatede form conversion op Adobe Cloud. Gebruik de URL `https://aemformsconversion.adobe.io/`. |
   | Sjabloonmodel | Standaardsjabloon die op geconverteerde formulieren moet worden toegepast. U kunt altijd een andere sjabloon opgeven voordat u de conversie start. Een sjabloon bevat basisstructuur en initiële inhoud voor een adaptief formulier. U kunt een sjabloon kiezen uit de sjablonen die u buiten het vak plaatst. U kunt ook een aangepaste sjabloon maken. |
   | Thema | Standaardthema dat op geconverteerde formulieren moet worden toegepast. U kunt altijd een ander thema opgeven voordat u de conversie start.  U kunt op het pictogram klikken om een thema te kiezen dat buiten het vak wordt weergegeven. U kunt ook een aangepast thema maken. |
   | Bestaande fragmenten | Plaats van bestaande fragmenten, indien aanwezig. |
   | Aangepast metamodel | Pad van het bestand .schema.json van het aangepaste metamodel. |



1. Geef op het tabblad **[!UICONTROL Advanced]** van de pagina **[!UICONTROL Create Automated Forms Conversion Configuration]** een waarde op voor het volgende veld:

   <table>
   <thead>
   <tr>
   <th>Veld</th>
   <th>Beschrijving</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td >Document van record genereren</td>
   <td>Selecteer de optie om automatisch het Document van Verslag voor omgezette vormen te produceren. De optie is alleen beschikbaar voor XFA-formulieren (XDP en PDF forms). Wanneer u de optie inschakelt nadat u een formulier hebt verzonden, kunt u uw klanten toestaan om de informatie die zij in het formulier hebben ingevuld, in gedrukte vorm of in documentindeling bij te houden voor toekomstig gebruik. Dit wordt bedoeld als document van verslag.</td>
   </tr>
   <tr>
   <td>Analyse inschakelen</td>
   <td>Selecteer de optie om Adobe Analytics in te schakelen op alle geconverteerde formulieren. Controleer voordat u deze optie gebruikt of Adobe Analytics is ingeschakeld voor uw AEM Forms-exemplaar.</td>
   </tr>
   </tbody>
   </table>

   * Als de bron een op XFA-Gebaseerde vorm met uitbreiding .XDP is, dan behoudt de output DOR de XFA lay-out, anders gebruikt de omzettingsdienst een uit-van-de-doos malplaatje om DOR voor andere op XFA-Gebaseerde vormen te produceren.
   * Wanneer een XFA-formulier wordt verzonden, worden de gegevens van het formulier opgeslagen als een XML-element of een kenmerk. Bijvoorbeeld, `<Amount currency="USD"> 10.00 </Amount>`. De valuta wordt opgeslagen als een kenmerk en valutabedrag, 10,00 als een element. Gegevens van een adaptief formulier verzenden heeft geen kenmerken, het heeft alleen elementen. Dus wanneer een XFA-formulier wordt geconverteerd naar een adaptief formulier, bevatten de adaptieve formulierverzendgegevens een element voor elk van deze kenmerken. Bijvoorbeeld,

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. Tik op **[!UICONTROL Create]**. De cloudconfiguratie wordt gemaakt. Uw AEM Forms-exemplaar is gereed om oudere formulieren te converteren naar adaptieve formulieren.

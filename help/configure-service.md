---
title: De service voor automatische conversie van formulieren configureren
description: Gereed uw AEM-exemplaar voor gebruik van de Automated Forms Conversion-service
translation-type: tm+mt
source-git-commit: 741ff89370a5215b70d90c49eea220171efe9339
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 7%

---


# De service voor automatische conversie van formulieren configureren {#about-this-help}

In deze Help wordt beschreven hoe een AEM beheerder de Automated Forms Conversion-service kan configureren om de conversie van de PDF forms naar adaptieve formulieren te automatiseren. Deze hulp is voor IT en AEM beheerders bij uw organisatie. De verstrekte informatie is gebaseerd op de veronderstelling dat iedereen die deze Hulp leest met de volgende technologieën vertrouwd is:

* Adobe Experience Manager- en AEM-pakketten installeren, configureren en beheren,

* Linux- en Microsoft Windows-besturingssystemen gebruiken

* SMTP-mailservers configureren

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service** -->

## Onboarding{#onboarding}

De service is gratis beschikbaar voor AEM 6.4 Forms en AEM 6.5 Forms On-Premise-termijnklanten en Adobe Managed Service Enterprise-klanten. U kunt contact opnemen met het Adobe-verkoopteam of uw Adobe-vertegenwoordiger om toegang tot de service aan te vragen.

Adobe maakt toegang voor uw organisatie mogelijk en biedt de vereiste rechten aan de persoon die is aangewezen als beheerder in uw organisatie. De beheerder kan toegang verlenen aan de AEM Forms-ontwikkelaars (gebruikers) van uw organisatie om verbinding te maken met de service.

## Vereisten {#prerequisites}

U hebt het volgende nodig om de Automated Forms Conversion Service te gebruiken:

* De geautomatiseerde service Forms Conversion is ingeschakeld voor uw organisatie
* Een Adobe ID-account met beheerdersrechten voor de conversieservice
* Een up-to-date AEM 6.4 of AEM 6.5-auteurinstantie met de nieuwste AEM Service Pack
* Een AEM gebruiker (op uw AEM) die lid is van een formulier-gebruikersgroep

## Set up the environment {#setuptheservice}

Voordat u de service gebruikt, moet u de AEM auteur voorbereiden om verbinding te maken met de service die wordt uitgevoerd op Adobe Cloud. Voer de volgende stappen in de vermelde reeks uit om uw exemplaar voor de service voor te bereiden:

1. [Download en installeer AEM 6.4 of AEM 6.5](#aemquickstart)
1. [Download en installeer de nieuwste AEM Service Pack](#servicepack)
1. [Download en installeer het nieuwste AEM Forms Add-on-pakket](#downloadaemformsaddon)
1. (optioneel) [Download en installeer het nieuwste aansluitingspakket](#installConnectorPackage)
1. [Aangepaste thema&#39;s en sjablonen maken](#referencepackage)

### Download en installeer AEM 6.4 of AEM 6.5 {#aemquickstart}


De geautomatiseerde dienst van de Omzetting van Forms loopt op AEM auteursinstantie. U hebt AEM 6.4 of AEM 6.5 nodig om een AEM auteur-instantie in te stellen. Als u niet AEM, download het van de volgende plaatsen:

* Als u een bestaande AEM klant bent, downloadt u AEM 6.4 of AEM 6.5 van de [Adobe-licentiewebsite](http://licensing.adobe.com).

* Als u een partner van de Adobe bent, gebruik het Programma [van de Opleiding van de Partner van](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) Adobe om AEM 6.4 of AEM 6.5 te verzoeken.

Nadat u AEM downloadt, voor instructies aan opstelling een AEM auteurinstantie, zie het [opstellen en het handhaven](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).

### Download en installeer AEM nieuwste Service Pack {#servicepack}

Download en installeer de nieuwste AEM Service Pack. Voor gedetailleerde instructies zie, of [AEM 6.4 de Nota&#39;s](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) van de Versie van het Pak van de Dienst of [AEM 6.5 de Nota&#39;s](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html)van de Versie van het Pak van de Dienst.

### AEM Forms-invoegtoepassing downloaden en installeren  {#downloadaemformsaddon}

Een AEM-exemplaar bevat basisfuncties voor formulieren. Voor de conversieservice zijn alle mogelijkheden van AEM Forms vereist. Download en installeer het invoegpakket voor AEM Forms om alle mogelijkheden van AEM Forms te benutten. Het pakket is vereist om de conversieservice in te stellen en uit te voeren. Zie Mogelijkheden voor gegevensvastlegging [installeren en configureren voor gedetailleerde instructies.](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> Zorg ervoor dat u de verplichte configuraties na de installatie uitvoert nadat u het invoegpakket hebt geïnstalleerd.


### (Optioneel) Installeer het aansluitingspakket  {#installConnectorPackage}

Het aansluitpakket biedt vroege toegang tot de functies voor [automatisch detecteren van logische secties](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) en verbeteringen die zijn geleverd in release AFC-2020.03.1. Installeer het pakket niet als u geen functie en verbeteringen in AFC-2020.03.1 nodig hebt.  U kunt het schakelaarpakket van AEM Pakketaandeel [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1)downloaden.


### Aangepaste thema&#39;s en sjablonen maken {#referencepackage}

Als u AEM start in de [productiemodus](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) (geen samplcontent-runmode), worden de referentiepakketten niet geïnstalleerd. De referentiepakketten bevatten voorbeeldthema&#39;s en sjablonen. Voor de geautomatiseerde Forms Conversion-service is minstens één thema en één sjabloon vereist om een PDF forms om te zetten in een adaptief formulier. Creeer een douanethema en een malplaatje van uw eigen en de [puntdienstconfiguratie](#configure-the-cloud-service) om douanesjablonen en thema&#39;s te gebruiken alvorens de dienst te gebruiken.

## Service configureren {#configure-the-service}

Voordat u verdergaat om de service te configureren en uw lokale instantie te verbinden met de service die wordt uitgevoerd op Adobe Cloud, dient u meer te weten te komen over de personen en rechten die nodig zijn om verbinding te maken met de service. De dienst gebruikt twee verschillende types van persona&#39;s, beheerders en ontwikkelaars:

* **Beheerders**: Beheerders zijn verantwoordelijk voor het beheer van Adobe-software en -services voor hun organisatie. Beheerders verlenen ontwikkelaars in hun organisatie toegang tot de service Automated Forms Conversion die op Adobe Cloud wordt uitgevoerd. Wanneer een beheerder voor een organisatie wordt voorzien, ontvangt de beheerder een e-mail met titel **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**. Als u een beheerder bent, controleer uw brievenbus e-mail met bovengenoemde titel en ga te werk om toegang tot ontwikkelaars van uw organisatie [te](#adduseranddevs)verlenen.

![e-mail voor toegangsbeheer](assets/admin-console-adobe-io-access-grantedx75.png)

* **Ontwikkelaars**: Een ontwikkelaar maakt verbinding met een lokale AEM Forms-auteurinstantie met de Automated Forms Conversion-service die wordt uitgevoerd op Adobe Cloud. Wanneer een beheerder rechten toekent aan een ontwikkelaar om verbinding te maken met de Automated Forms Conversion-service, wordt een e-mail met de titel U hebt nu toegang tot ontwikkelaars om de Adobe API-integratie voor uw organisatie te beheren, verzonden naar de ontwikkelaar. Als u een ontwikkelaar bent, controleert u uw postvak op e-mail met de bovenstaande titel en gaat u verder om uw lokale AEM te [verbinden met de Automated Forms Conversion-service op Adobe Cloud.](#connectafcadobeio)

![ontwikkel toegang verlenen e-mail](assets/email-developer-accessx94.png)

### (Alleen voor beheerders) Toegang verlenen aan ontwikkelaars van uw organisatie {#adduseranddevs}

Nadat Adobe toegang voor uw organisatie toelaat en vereiste voorrechten aan de beheerder verstrekt, kan de beheerder zich aanmelden in Admin Console (gedetailleerde instructies hieronder), een profiel creëren, en ontwikkelaars toevoegen aan het profiel. Ontwikkelaars kunnen een lokale versie van AEM Forms verbinden met de Automated Forms Conversion-service op Adobe Cloud.

De ontwikkelaars zijn leden van uw organisatie die wordt aangewezen om de omzettingsdienst in werking te stellen. Alleen ontwikkelaars die zijn toegevoegd aan het Adobe Automated Forms Conversion-serviceprofiel hebben het recht om de Automated Forms Conversion-service te gebruiken. Voer de onderstaande stappen uit om een profiel te maken en er ontwikkelaars aan toe te voegen. Er is minimaal één profiel vereist om vereiste toegang te verlenen aan ontwikkelaars van uw organisatie:

1. Meld u aan bij de [Admin Console](https://adminconsole.adobe.com/). Gebruik **Adobe ID** van beheerder provisioned om de Automated Forms Conversion-service te gebruiken voor aanmelding. Geen andere id of Federated ID om u aan te melden.
1. Klik op de **[!UICONTROL Automated Forms Conversion]** optie.
1. Klik **[!UICONTROL New Profile]** op het **[!UICONTROL Products]** tabblad.
1. Geef **[!UICONTROL Name]**, **[!UICONTROL Display Name]** en **[!UICONTROL Description]** voor het profiel op. Klik op **[!UICONTROL Done]**. Er wordt een profiel gemaakt.

   ![Geef details op voor het nieuwe profiel.](assets/create-new-profile-details.png)

1. Voeg ontwikkelaar toe aan het profiel. U voegt als volgt de ontwikkelaars toe:
   1. Navigeer in de [Admin Console](https://adminconsole.adobe.com/enterprise)naar het tabblad Overzicht.
   1. Klik op **[!UICONTROL Assign Developers]** de vereiste productkaart.
   1. Voer het e-mailadres en (optioneel) de naam en achternaam van de ontwikkelaar in.
   1. Selecteer productprofielen. Tik op **[!UICONTROL Save]**.

Herhaal bovenstaande stappen voor alle gebruikers.  Zie [Ontwikkelaars](https://helpx.adobe.com/enterprise/using/manage-developers.html)beheren voor meer informatie over het toevoegen van ontwikkelaars.

Nadat een beheerder ontwikkelaars heeft toegevoegd aan het Adobe I/O-profiel, worden de ontwikkelaars via e-mail op de hoogte gesteld. Nadat ontwikkelaars de e-mail hebben ontvangen, kunnen ze op Adobe Cloud [een lokale AEM Forms-instantie](#connectafcadobeio)verbinden met de Automated Forms Conversion-service.

### (Alleen voor ontwikkelaars) Verbind uw lokale AEM Forms-instantie met de Automated Forms Conversion-service op Adobe Cloud {#connectafcadobeio}

Nadat een beheerder u ontwikkelaarstoegang verleent, kunt u uw lokale AEM Forms-instantie verbinden met de Automated Forms-conversieservice die wordt uitgevoerd op Adobe Cloud. Voer de volgende stappen in de vermelde reeks uit om uw AEM Forms-instantie te verbinden met de service:

* [E-mailmeldingen configureren](configure-service.md#configureemailnotification)
* [Gebruiker toevoegen aan de groep met gebruikers van het formulier](#adduserstousergroup)
* [Openbare certificaten verkrijgen](#obtainpubliccertificates)
* [De service-API&#39;s configureren in de Adobe Developer Console](#createintegration)
* [De cloudservice configureren](configure-service.md#configure-the-cloud-service)

#### E-mailmelding configureren {#configureemailnotification}

De geautomatiseerde dienst van de Omzetting van Forms gebruikt de Dag CQ- postdienst om e-mailberichten te verzenden. Deze e-mailmeldingen bevatten informatie over geslaagde of mislukte conversies. Sla deze stappen over als u geen melding wilt ontvangen. Voer de volgende stappen uit om de Day CQ Mail Service te configureren:

1. Ga naar AEM configuratiebeheer op `http://localhost:4502/system/console/configMgr`
1. Open de configuratie van de Day CQ Mail Service. Geef een waarde op voor de velden **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]** en **[!UICONTROL From address]** velden. Klik op **[!UICONTROL Save]**.

   U kunt contact opnemen met uw e-mailserviceprovider of IT-beheerder voor informatie over de hostnaam en poort van SMTP-server. U kunt elk geldig e-mailadres gebruiken in het veld Van. Bijvoorbeeld notification@example.com of donotreply@example.com.

1. Open de **[!UICONTROL Day CQ Link Externalizer]** configuratie. Geef in het **[!UICONTROL Domains]** veld de werkelijke hostnaam of het werkelijke IP-adres en het poortnummer op voor lokale, auteur- en publicatieinstanties. Klik op **[!UICONTROL Save]**.

#### Gebruiker toevoegen aan de groep met gebruikers van het formulier {#adduserstousergroup}

Geef een e-mailadres op in het profiel van de AEM gebruiker die is aangewezen om de service uit te voeren. Zorg ervoor dat de gebruiker lid is van de gebruikersgroep [Formulieren](https://helpx.adobe.com/experience-manager/6-4/forms/using/forms-groups-privileges-tasks.html) . E-mails worden verzonden naar het e-mailadres van de gebruiker die de conversie uitvoert. U kunt als volgt een e-mailadres voor de gebruiker opgeven en gebruiker toevoegen aan de gebruikersgroep Formulieren:

1. Meld u als AEM beheerder aan bij de auteur-instantie van AEM Forms. Gebruik uw lokale AEM om u aan te melden. Gebruik Adobe ID niet om u aan te melden. Tap **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Selecteer een gebruiker die is toegewezen om de conversieservice uit te voeren en tik op **[!UICONTROL Properties]**. De pagina Gebruikersinstellingen bewerken wordt geopend.
1. Geef een e-mailadres op in het **[!UICONTROL Email]** veld en tik op **[!UICONTROL Save]**. De e-mails worden naar het opgegeven e-mailadres verzonden wanneer de conversie is voltooid of mislukt.
1. Tap the **Groups** tab. Typ en selecteer op het tabblad Groep de groep **gebruikers** van formulieren. Tik op **Opslaan en sluiten**. De gebruiker is nu lid van de groep met gebruikers van het formulier.

#### Openbare certificaten verkrijgen {#obtainpubliccertificates}

Met een openbaar certificaat kunt u uw profiel verifiëren op Adobe I/O.

1. Meld u aan bij de AEM Forms-auteur. Ga naar **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Tik op **[!UICONTROL Create]**. De **[!UICONTROL Adobe IMS Technical Account Configuration]** pagina wordt weergegeven.

   ![De pagina Configuratie van de technische account van Adobe IMS](assets/adobe-ims-technical-account-configuration.png)

1. Selecteer **[!UICONTROL Automated Forms Conversion Service]** in Cloudoplossing.

1. Selecteer het **[!UICONTROL Create new certificate]** selectievakje en geef een alias op. De alias fungeert als naam voor het dialoogvenster. Tik op **[!UICONTROL Create certificate]**. Er wordt een dialoogvenster weergegeven. Klik op **[!UICONTROL OK]**. Het certificaat wordt gemaakt.

1. Tap **[!UICONTROL Download Public Key]** and save the *AEM-Adobe-IMS.crt* certificate file on your machine. Het certificaatbestand wordt gebruikt om de service-API&#39;s in de Adobe Developer Console [te](#createintegration)configureren. Tik op **[!UICONTROL Next]**.

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

Als u de Automated Forms Conversion-service wilt gebruiken, maakt u een project en voegt u de Automated Forms Configuration Service API toe aan het project in de Adobe Developer Console. De integratie genereert API Key, Client Secret, Payload (JWT).

1. Meld u aan bij [https://console.adobe.io/](https://console.adobe.io/). Gebruik uw Adobe ID, ontwikkelaarsaccount die uw beheerder heeft ingericht om u aan te melden bij de Adobe I/O-console om u aan te melden.
1. Selecteer uw organisatie in de rechterbovenhoek. Neem contact op met de beheerder als u uw organisatie niet kent.
1. Tik op **[!UICONTROL Create new project]**. Er verschijnt een scherm om aan de slag te gaan met uw nieuwe project. Tik op **[!UICONTROL Add API]**. Er verschijnt een scherm met een lijst van alle API&#39;s die voor uw account zijn ingeschakeld.
1. Selecteer **[!UICONTROL Automated Forms Conversion service]** en tik op **[!UICONTROL Next]**. Er verschijnt een scherm om de API te configureren.
1. Selecteer de [!UICONTROL Upload your public key] optie, upload het AEM-Adobe-IMS.crt-bestand dat u in de sectie [Openbare certificaten](#obtainpubliccertificates) verkrijgen hebt gedownload en tik op **[!UICONTROL Next]**. De optie Create a new Service Account (JWT) credential wordt weergegeven. Tik op **[!UICONTROL Next]**.
1. Selecteer een productprofiel en tik op **[!UICONTROL Save configured API]**. Selecteer het profiel dat u hebt gemaakt terwijl u toegang [verleent aan ontwikkelaars van uw organisatie](#adduseranddevs). Neem contact op met de beheerder als u niet weet welk profiel u moet selecteren.
1. Tik **[!UICONTROL Service Account (JWT)]** om de API-sleutel, het clientgeheim en andere informatie weer te geven die nodig is om uw lokale AEM aan te sluiten op de Automated Forms Conversion-service. De informatie op de pagina wordt gebruikt om configuratie IMS op uw lokale machine tot stand te brengen.

1. Open de pagina van de Configuratie IMS op uw lokale instantie. U hebt de pagina open gelaten aan het einde van de sectie voor [Openbaar certificaat verkrijgen](#obtainpubliccertificates).

   ![Titel, API-sleutel, clientgeheim en payload opgeven ](assets/ims-configuration-details.png)

1. Geef API-sleutel en clientgeheim op de technische pagina Adobe IMS op. Gebruik de waarden die op de de consolepagina van de Ontwikkelaar van de Adobe op de Rekening van de Dienst (JWT) worden gespecificeerd.

   >[!NOTE]
   >
   >
   >Voor nuttige lading, gebruik de code die op het Generate JWT lusje van de pagina van de Rekening van de Dienst (JWT) van de Console van de Ontwikkelaar van Adobe wordt verstrekt.

1. Tik op **[!UICONTROL Save]**. De IMS-configuratie wordt gemaakt.

   >[!CAUTION]
   >
   >Maak slechts één IMS-configuratie. Maak niet meer dan één IMS-configuratie.

1. Select the IMS configuration and tap **[!UICONTROL Check Health]**. Er wordt een dialoogvenster weergegeven. Tik op **[!UICONTROL Check]**. Bij een geslaagde verbinding wordt het bericht *Token retrieved successfully* weergegeven.

   ![Bij een geslaagde verbinding wordt het bericht met succes opgehaalde token weergegeven. ](assets/health-check.png)

   <br/> <br/>

#### Configure the cloud service {#configure-the-cloud-service}

Maak een cloudserviceconfiguratie om uw AEM aan te sluiten op de conversieservice. U kunt hiermee ook een sjabloon, thema en formulierfragmenten opgeven voor conversie. U kunt meerdere configuraties voor cloudservices maken, afzonderlijk voor elke set formulieren. U kunt bijvoorbeeld een aparte configuratie voor de formulieren van de verkoopafdeling en een aparte configuratie voor de formulieren voor klantenondersteuning hebben. Voer de volgende stappen uit om een configuratie van de wolkendienst tot stand te brengen:

1. Tik op uw AEM Forms-exemplaar op **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**.
1. Tik op de **[!UICONTROL Global]** map en tik op **[!UICONTROL Create]**. De pagina voor het maken van de configuratie voor automatische Forms-omzetting wordt weergegeven. De configuratie wordt gemaakt in de map Global. U kunt de configuratie ook maken in een andere map die al bestaat of een nieuwe map voor uw configuraties maken.

1. Geef op de **[!UICONTROL Create Automated Forms Conversion Configuration]** pagina een waarde op voor de volgende velden en tik op **[!UICONTROL Next]**.

   | Veld | Beschrijving |
   |--- |--- |
   | Titel | Unieke titel voor de configuratie. De titel wordt weergegeven in de gebruikersinterface waarmee de conversie wordt gestart. |
   | Naam | Unieke naam voor de configuratie. De configuratie wordt met de opgegeven naam opgeslagen in de CRX-gegevensopslagruimte. De naam kan identiek zijn aan de titel. |
   | Locatie miniatuur | Locatie van de miniatuur voor de configuratie. |
   | Service-URL | URL van de Automated Forms Conversion-service op Adobe Cloud. Gebruik de `https://aemformsconversion.adobe.io/` URL. |
   | Sjabloonmodel | Standaardsjabloon die op geconverteerde formulieren moet worden toegepast. U kunt altijd een andere sjabloon opgeven voordat u de conversie start. Een sjabloon bevat basisstructuur en initiële inhoud voor een adaptief formulier. U kunt een sjabloon kiezen uit de sjablonen die u buiten het vak plaatst. U kunt ook een aangepaste sjabloon maken. |
   | Thema | Standaardthema dat op geconverteerde formulieren moet worden toegepast. U kunt altijd een ander thema opgeven voordat u de conversie start.  U kunt op het pictogram klikken om een thema te kiezen dat buiten het vak wordt weergegeven. U kunt ook een aangepast thema maken. |
   | Bestaande fragmenten | Plaats van bestaande fragmenten, indien aanwezig. |
   | Aangepast metamodel | Pad van het bestand .schema.json van het aangepaste metamodel. |



1. Geef op het **[!UICONTROL Advanced]** tabblad van de **[!UICONTROL Create Automated Forms Conversion Configuration]** pagina een waarde op voor het volgende veld:

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

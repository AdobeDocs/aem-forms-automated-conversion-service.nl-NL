---
title: 'PDF-formulieren converteren naar adaptieve formulieren '
seo-title: Convert PDF forms to adaptive forms
description: Voer de service Automatede form conversion uit om PDF forms om te zetten in adaptieve formulieren
seo-description: Run the Automated Forms Conversion service to convert PDF forms to adaptive forms
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
exl-id: 415e05b5-5a90-490c-bf7c-d3365ce95e24
source-git-commit: 5f07f5df6369007a491cf0873839f84a61827cb5
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 7%

---

# PDF-formulieren converteren naar adaptieve formulieren {#convert-print-forms-to-adaptive-forms}

AEM Forms Automatede form conversion Service, aangedreven door Adobe Sensei, zet uw PDF forms automatisch om in apparaatvriendelijke en responsieve adaptieve formulieren. Of u nu niet-interactieve PDF forms, Acro Forms of op XFA gebaseerde PDF forms gebruikt, de service Automatede form conversion kan deze formulieren eenvoudig converteren naar adaptieve formulieren. Voor informatie over de mogelijkheden, de omzettingswerkstroom en het aan boord gaan van informatie zie [automatede form conversion](introduction.md) service.

## Voorwaarden {#pre-requisites}

* [**De conversieservice configureren**](configure-service.md)

* **De [sjablonen](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) toe te passen op geconverteerde formulieren:** Met behulp van een sjabloon kunt u consistente branding toepassen op alle adaptieve formulieren. Bovendien haalt en gebruikt de dienst van de Automatede form conversion geen kopbal en footer van bronPDF documenten. U kunt adaptieve formuliersjablonen gebruiken om kop- en voettekst op te geven. De kop- en voettekst die in de sjabloon is opgegeven, worden tijdens de conversie op het adaptieve formulier toegepast. Wanneer u een map voor de sjablonen maakt, selecteert u de **[!UICONTROL Browse configurations]** voor iedereen.

* **De [thema&#39;s](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) toe te passen op geconverteerde formulieren:** Met een thema kunt u een consistente stijl toepassen op alle adaptieve vormen van uw organisatie.

* **(optioneel)** [**Uw bron-PDF forms converteren naar Adobe Sign-formulier**](frequently-asked-questions.md)

## Het conversieproces starten {#start-the-conversion-process}

Nadat u uw AEM hebt aangesloten met AEM Forms Conversion Service, kunt u uw PDF forms converteren naar adaptieve formulieren. Voer de volgende stappen in de vermelde volgorde uit om de formulieren om te zetten:

* [PDF forms uploaden naar uw AEM Forms-server](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [De conversie uitvoeren](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Omgezette formulieren controleren en corrigeren](review-correct-ui-edited.md)

### PDF forms uploaden naar uw AEM Forms-server {#upload-pdf-forms-to-your-aem-forms-server}

De conversieservice converteert PDF forms die beschikbaar zijn op uw AEM Forms-exemplaar naar adaptieve formulieren. U kunt alle PDF forms tegelijk uploaden of, indien nodig, gefaseerd. Houd rekening met het volgende voordat u de formulieren uploadt:

* Houd het aantal formulieren in een map kleiner dan 15 en houd het totale aantal pagina&#39;s in een map kleiner dan 50.
* Houd de map kleiner dan 10 MB. Formulieren niet in een submap bewaren.
* Houd het aantal pagina&#39;s in een formulier kleiner dan 15.
* Upload de beveiligde formulieren niet. De service converteert formulieren die met een wachtwoord zijn beveiligd niet.
* Upload geen bronformulieren met spaties in de bestandsnaam. Verwijder de ruimte uit de naam van het bestand voordat u de formulieren uploadt.
* Upload geen [PDF-portfolio&#39;s](https://helpx.adobe.com/nl/acrobat/using/overview-pdf-portfolios.html). De service zet een PDF-Portfolio niet om in een adaptieve vorm.
* Lees de [Bekende problemen](known-issues.md) en de [Beste praktijken en overwegingen](styles-and-pattern-considerations-and-best-practices.md) secties te openen en wijzigingen in formulieren aan te brengen.

Voer de volgende stappen uit om de formulieren te uploaden die moeten worden geconverteerd naar een map op uw AEM Forms-exemplaar:

1. Meld u aan bij de AEM Forms-instantie.

1. Tikken **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Tik op **[!UICONTROL Create]**> **[!UICONTROL Folder]**. Opgeven **Titel** en **Naam** van de map. Tik op **[!UICONTROL Create]**. Er wordt een map gemaakt.
1. Tik om de nieuwe map te openen.
1. Tik op **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. Selecteer de formulieren die u wilt uploaden, klikt u op **[!UICONTROL Open]** en klik op **[!UICONTROL Upload]**. De formulieren worden geüpload.

### De conversie uitvoeren {#run-the-conversion}

Nadat u de formulieren hebt geüpload en de service hebt geconfigureerd, voert u de volgende stappen uit om de conversie te starten:

1. Tik op uw AEM Forms-exemplaar **[!UICONTROL Adobe Experience Manager]** ![Dialoogvenster Conversie-instellingen](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Selecteer een formulier of de map met PDF forms (te converteren formulieren) en tik **[!UICONTROL Start Automated Conversion]**. De **[!UICONTROL Conversion Settings]** wordt weergegeven.

   ![De configuraties opgeven](assets/conversion-settings-dialog.png)

1. In de **[!UICONTROL Basic]** tabblad van het dialoogvenster Conversie-instellingen:

   * **[!UICONTROL Select a cloud configuration]**. Als u een configuratie selecteert, worden de standaardsjabloon en het standaardthema al opgegeven. U kunt desgewenst een andere sjabloon of een thema opgeven.
   * Geef een locatie op waar u gegenereerde adaptieve formulieren en het bijbehorende schema wilt opslaan. U kunt standaardpaden gebruiken of aangepaste paden opgeven.
   * Gebruik de **Aangepaste formulieren genereren zonder gegevensmodelbindingen** Selecteer deze optie als u een adaptief formulier wilt genereren met of zonder gegevensmodelbindingen.
Als u deze optie niet selecteert, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden in het adaptieve formulier en het JSON-schema. De **[!UICONTROL Save generated data model schema at]** wordt de standaardlocatie weergegeven waar het gegenereerde JSON-schema wordt opgeslagen. U kunt de locatie ook aanpassen om het gegenereerde schema op te slaan.
Als u deze optie selecteert, genereert de conversieservice een adaptief formulier zonder bindingen van gegevensmodellen. Na een geslaagde conversie kunt u een adaptief formulier koppelen aan een formuliergegevensmodel, een XML-schema of een JSON-schema. Zie voor meer informatie [Een adaptief formulier maken](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).

   <!--

   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. In de **[!UICONTROL Additional]** tabblad Conversie-instellingen,
   * Selecteer **[!UICONTROL Extract fragment from adaptive forms]** zodat de conversieservice formulierfragmenten voor geconverteerde formulieren kan identificeren, uitnemen en downloaden. Wanneer u **[!UICONTROL Extract fragment from adaptive forms]** , zijn de opties voor het opgeven van paden voor het opslaan van geëxtraheerde formulierfragmenten en de bijbehorende schema&#39;s voor formulierfragmenten ingeschakeld.
   * Geef de locatie op van **[!UICONTROL existing adaptive form fragments]**, als u een aantal bestaande JSON-schema&#39;s hebt en geen adaptieve formulierfragmenten met schema&#39;s hebt en u van plan bent deze fragmenten te gebruiken in automatisch gegenereerde adaptieve formulieren. Conversieservice komt overeen met beschikbare JSON-formulierfragmenten op basis van schema&#39;s en zonder adaptieve formulierfragmenten met invoerfragmenten (alleen niet-interactieve PDF forms), als er een overeenkomst is, wordt het overeenkomende adaptieve formulierfragment gebruikt in de overeenkomende adaptieve formulieren.

   >[!NOTE]
   >
   >
   > * U kunt alleen **[!UICONTROL  Extract Fragment]** of **[!UICONTROL Use existing adaptive form fragments]** op een bepaald moment. U kunt niet beide opties tegelijk gebruiken.
   > * U kunt de **[!UICONTROL Use existing adaptive form fragments]** alleen met niet-interactieve PDF forms. Andere formuliertypen worden nog niet ondersteund.
   > * U kunt alleen ongebonden fragmenten of fragmenten gebruiken die zijn gebonden aan een JSON-schema met de Automated Conversion Service. Gebruik geen XFA-fragmenten. XFA-fragmenten worden niet ondersteund.


   * Selecteer **[!UICONTROL Auto-detect multi-column layout of input forms]** voor het behouden van de indeling van het bronformulier voor grote schermen zoals desktops en laptops. De optie is handig als u de indeling van bronformulieren met meerdere kolommen wilt behouden. Wanneer een PDF een bronapparaat heeft met twee kolommen, genereert de service bijvoorbeeld een adaptief uitvoerformulier met een indeling met twee kolommen voor schermschermen met groot scherm en een lay-out met één kolom voor apparaten met klein scherm, zoals mobiele telefoons. De eigenschap heeft sommige bekende kwesties met de structuur van het gegevensbronschema. Zie voor meer informatie de [bekende problemen](known-issues.md) artikel.
   * De service creëert standaard een aparte, bovenliggende laag voor elke pagina van een PDF-formulier. U kunt nu de opdracht **[!UICONTROL Auto-detect logical sections]** geen deelvensters op paginaniveau (op paginanummers gebaseerde deelvensters) maken en alleen logische deelvensters maken. Hierbij worden ook de velden die niet bij een sectie met een voorafgaande logische sectie horen en de velden van een logische sectie die verspreid zijn over twee aangrenzende pagina&#39;s samengevoegd tot één enkele logische sectie. Als sommige velden van een logische sectie bijvoorbeeld aan het einde van pagina 1 staan en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden samengevoegd tot één enkele logische sectie.

      >[!NOTE]
      > U hebt het aansluitpakket 1.1.38 of hoger nodig om de  **[!UICONTROL Auto-detect logical sections]** gebruiken.


* (Alleen AEM Forms as a Cloud Service) De [Secties automatisch omzetten in fragmenten] Deze optie is van toepassing op PDF forms met meer dan 15 pagina&#39;s. De gedetecteerde bovenste secties worden omgezet in fragmenten. Ook wordt het uitladen van alle gemaakte fragmenten ingeschakeld. Het verbetert de rendersnelheid van geconverteerde formulieren en maakt het gemakkelijker om grote formulieren in een adaptieve formuliereditor te laden.

   >[!NOTE]
   > Gebruik geen responsieve lay-outsjabloon wanneer u de optie Secties automatisch omzetten in fragmenten gebruikt.
   > Gebruik de revisie en de juiste editor om kleine deelvensters samen te voegen tot een groot venster. Hierdoor wordt het aantal fragmenten in de omgezette adaptieve vorm verminderd.
   > Als u de &quot;teveel vraag&quot;uitzondering ervaart,
   >
   > * het formulier herstructureren om een vereenvoudigde hiërarchie te maken
   > * [verhoog de waarde van de parameter sling.max.call]tot een voldoende hoog aantal tot de uitzondering verdwijnt.
   > * [vergroten, grootte van cache](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/configure-aem-forms/configure-adaptive-forms-cache.html). De fout treedt op als het formulier te complex is, een groot aantal tabellen heeft en een hiërarchische structuur op meerdere niveaus.


1. Tik op **[!UICONTROL Start Conversion]**. De conversie wordt gestart. De voortgang van de conversie wordt weergegeven op de map of het formulier totdat de conversie wordt uitgevoerd. Het bericht wordt vervangen door een ander statusbericht (geconverteerd, gedeeltelijk geconverteerd of Conversie mislukt) nadat de conversie is voltooid. Na voltooiing van de conversie wordt ook een statuse-mail verzonden naar het geconfigureerde e-mailadres:

   * Bij een geslaagde conversie worden het geconverteerde adaptieve formulier en het bijbehorende schema gedownload naar het pad dat is opgegeven in het dialoogvenster **[!UICONTROL Basic]** van het dialoogvenster voor conversie. Formulierfragmenten en het bijbehorende schema worden alleen gedownload als de optie Fragment extraheren is geselecteerd voordat de conversie wordt gestart.
   * Bij een mislukte conversie **[!UICONTROL Conversion Failed]** wordt een bericht weergegeven als alle invoerformulieren niet zijn geconverteerd of als de **[!UICONTROL Partially Failed]** wordt een bericht weergegeven wanneer slechts enkele invoerformulieren niet zijn geconverteerd. Er wordt een statuse-mail verzonden op de [geconfigureerd e-mailadres](configure-service.md#configureemailnotification) en er wordt een fout bij het bestand error.log geregistreerd.

   Als u een XFA-gebaseerd PDF formulier converteert naar een adaptief formulier, koppelt de conversieservice het PDF-formulier automatisch aan het geconverteerde adaptieve formulier als de Document of Record-sjabloon. Na de conversie kunt u de adaptieve formuliereigenschappen openen om de sjabloon Document of Record te bekijken in het dialoogvenster **[!UICONTROL Document of Record Template Configuration]** deel van **[!UICONTROL Form Model]** tab. </br>

   De conversieservice uploadt het PDF-formulier alleen automatisch naar het geconverteerde adaptieve formulier als Document of Record-sjabloon als u de optie **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** optie.

   <!--

   Comment Type: draft

   <note type="note">
   <p>By default, the adaptive form produces a JSON schema instead of XML schema on submission. JSON schema of a converted adaptive form is complaint with XML schema of an XFA-based form. You can use the <a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString">org.apache.sling.commons.json.xml API</a> to convert a JSON schema to XML schema. You can also use the following sample code for conversion:</p>
   <p><code class="code">import org.apache.sling.commons.json.JSONException;
   <discoiqbr /> import org.apache.sling.commons.json.JSONObject;
   <discoiqbr /> import org.apache.sling.commons.json.xml.XML;
   <discoiqbr />
   <discoiqbr /> public class ConversionUtils {
   <discoiqbr />
   <discoiqbr /> public static String jsonToXML(String jsonString) throws JSONException {
   <discoiqbr /> //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
   <discoiqbr /> //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
   <discoiqbr /> //Note: Need to extract boundData part before converting to XML
   <discoiqbr /> return XML.toString(new JSONObject(jsonString));
   <discoiqbr /> }
   <discoiqbr /> }</code><br /> </p>
   </note>
   -->

   >[!NOTE]
   >
   >Als het conversieproces meer dan 60 minuten in beslag neemt en het PDF-formulier nog steeds niet wordt geconverteerd naar een adaptief formulier, maakt u een map op AEM Forms-exemplaar, uploadt u het PDF-formulier naar de nieuwe map en start u de conversie opnieuw.

## Omgezette formulieren controleren en corrigeren {#review-and-correct-the-converted-forms}

Real world-forms hebben complexe vereisten voor het vastleggen van gegevens. Zodra de automatische conversie is voltooid, kunnen klanten de conversiekwaliteit van het formulier controleren en de benodigde updates uitvoeren voor het formulier. AEM Forms biedt een [beoordelen en corrigeren](review-correct-ui-edited.md) editor om de vereiste wijzigingen aan te brengen. Zo kunt u de automatische identificatie van formuliervelden verbeteren en geïdentificeerde velden van het ene type naar het andere converteren. U kunt bijvoorbeeld de indeling van twee kolommen in een formulier bepalen en een veld dat automatisch als keuzerondje wordt aangeduid, wijzigen in een veld met meerdere keuzen.

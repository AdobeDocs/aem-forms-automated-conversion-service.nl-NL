---
title: PDF forms converteren naar adaptieve formulieren
seo-title: Convert PDF forms to adaptive forms
description: Voer AFCS (Automatede form conversion Service) uit om PDF forms om te zetten in adaptieve formulieren
seo-description: Run the Automated Forms Conversion service (AFCS) to convert PDF forms to adaptive forms
contentOwner: khsingh
topic-tags: forms
feature: Adaptive Forms, Foundation Components
exl-id: 415e05b5-5a90-490c-bf7c-d3365ce95e24
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 6%

---

# PDF forms converteren naar adaptieve formulieren {#convert-print-forms-to-adaptive-forms}

AEM Forms Automatede form conversion Service (AFCS), aangedreven door Adobe Sensei, zet uw PDF forms automatisch om in apparaatvriendelijke en responsieve adaptieve formulieren. Of u nu niet-interactieve PDF forms, Acro Forms of op XFA gebaseerde PDF forms gebruikt, de Automatede form conversion-service (AFCS) kan deze formulieren eenvoudig converteren naar adaptieve formulieren. Voor informatie over de mogelijkheden, omzettingswerkschema, en op het instappen informatie zie ](introduction.md) dienst van de Automatede form conversion [.

## Voorwaarden {#pre-requisites}

* [**vorm de omzettingsdienst**](configure-service.md)

* **bereidt de [ malplaatjes ](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) voor om op omgezette vormen worden toegepast:** Gebruikend een malplaatje staat u toe om verenigbare branding over alle adaptieve vormen toe te passen. Bovendien haalt en gebruikt de dienst van de Automatede form conversion (AFCS) geen kopbal en footer van bronPDF documenten. U kunt adaptieve formuliersjablonen gebruiken om kop- en voettekst op te geven. De kop- en voettekst die in de sjabloon is opgegeven, worden tijdens de conversie op het adaptieve formulier toegepast. Wanneer u een map voor de sjablonen maakt, selecteert u de optie **[!UICONTROL Browse configurations]** voor iedereen.

* **bereidt de [ thema&#39;s ](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) voor om op omgezette vormen worden toegepast:** Gebruikend een thema staat u toe om een verenigbare stijl op alle adaptieve vormen van uw organisatie toe te passen.

* **(facultatief)** [**zet uw bronPDF forms in de vorm van Adobe Sign**](frequently-asked-questions.md) om

## Het conversieproces starten {#start-the-conversion-process}

Nadat u uw AEM hebt aangesloten met AEM Forms Conversion Service, kunt u uw PDF forms converteren naar adaptieve formulieren. Voer de volgende stappen in de vermelde volgorde uit om de formulieren om te zetten:

* [PDF forms uploaden naar uw AEM Forms-server](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [De conversie uitvoeren](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Omgezette formulieren controleren en corrigeren](review-correct-ui-edited.md)

### PDF forms uploaden naar uw AEM Forms-server {#upload-pdf-forms-to-your-aem-forms-server}

De conversieservice converteert PDF forms die beschikbaar zijn op uw AEM Forms-exemplaar naar adaptieve formulieren. U kunt alle PDF forms in één keer of op een gefaseerde manier uploaden, zoals vereist. Houd rekening met het volgende voordat u de formulieren uploadt:

* Houd het aantal formulieren in een map kleiner dan 15 en houd het totale aantal pagina&#39;s in een map kleiner dan 50.
* Houd de map kleiner dan 10 MB. Formulieren niet in een submap bewaren.
* Houd het aantal pagina&#39;s in een formulier kleiner dan 15.
* Upload de beveiligde formulieren niet. De service converteert formulieren die met een wachtwoord zijn beveiligd niet.
* Upload geen bronformulieren met spaties in de bestandsnaam. Verwijder de ruimte uit de naam van het bestand voordat u de formulieren uploadt.
* Upload geen [PDF-portfolio&#39;s](https://helpx.adobe.com/nl/acrobat/using/overview-pdf-portfolios.html). De service zet een PDF-Portfolio niet om in een adaptieve vorm.
* Lees de [ Bekende kwesties ](known-issues.md) en de [ Beste praktijken en overwegingen ](styles-and-pattern-considerations-and-best-practices.md) secties en breng voorgestelde veranderingen in vormen aan.

Voer de volgende stappen uit om de formulieren te uploaden die moeten worden geconverteerd naar een map op uw AEM Forms-exemplaar:

1. Meld u aan bij de AEM Forms-instantie.

1. Tik op **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** .
1. Tik op **[!UICONTROL Create]** > **[!UICONTROL Folder]** . Specificeer **Titel** en **Naam** van de omslag. Tik op **[!UICONTROL Create]**. Er wordt een map gemaakt.
1. Tik om de nieuwe map te openen.
1. Tik op **[!UICONTROL Create]** > **[!UICONTROL File Upload]** . Selecteer de te uploaden formulieren, klik op **[!UICONTROL Open]** en klik op **[!UICONTROL Upload]** . De formulieren worden geüpload.

### De conversie uitvoeren {#run-the-conversion}

Nadat u de formulieren hebt geüpload en de service hebt geconfigureerd, voert u de volgende stappen uit om de conversie te starten:

1. Tik op uw AEM Forms-instantie op **[!UICONTROL Adobe Experience Manager]** ![ Dialoogvenster Conversie-instellingen ](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** .
1. Selecteer een formulier of de map met PDF forms (te converteren formulieren) en tik op **[!UICONTROL Start Automated Conversion]** . Het dialoogvenster **[!UICONTROL Conversion Settings]** wordt weergegeven.

   ![ specificeer de configuraties ](assets/conversion-settings-dialog.png)

1. Op het tabblad **[!UICONTROL Basic]** van het dialoogvenster Conversie-instellingen:

   * **[!UICONTROL Select a cloud configuration]**. Als u een configuratie selecteert, worden de standaardsjabloon en het standaardthema al opgegeven. U kunt desgewenst een andere sjabloon of een thema opgeven.
   * Geef een locatie op waar u gegenereerde adaptieve formulieren en het bijbehorende schema wilt opslaan. U kunt standaardpaden gebruiken of aangepaste paden opgeven.
   * Gebruik **produceer adaptieve vormen zonder de bindingen van het gegevensmodel** optie om te selecteren als u een adaptieve vorm met of zonder de banden van het gegevensmodel wilt produceren.
Als u deze optie niet selecteert, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden in het adaptieve formulier en het JSON-schema. In het veld **[!UICONTROL Save generated data model schema at]** wordt de standaardlocatie weergegeven waar het gegenereerde JSON-schema wordt opgeslagen. U kunt de locatie ook aanpassen om het gegenereerde schema op te slaan.
Als u deze optie selecteert, genereert de conversieservice een adaptief formulier zonder bindingen van gegevensmodellen. Na een geslaagde conversie kunt u een adaptief formulier koppelen aan een formuliergegevensmodel, een XML-schema of een JSON-schema. Voor meer informatie, zie [ Creërend een adaptieve vorm ](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).

   <!--

   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. In het tabblad **[!UICONTROL Additional]** van het dialoogvenster Conversie-instellingen,
   * Selecteer de optie **[!UICONTROL Extract fragment from adaptive forms]** als u wilt dat de conversieservice formulierfragmenten voor geconverteerde formulieren kan identificeren, uitnemen en downloaden. Wanneer u de optie **[!UICONTROL Extract fragment from adaptive forms]** selecteert, zijn de opties voor het opslaan van geëxtraheerde formulierfragmenten en de bijbehorende schema&#39;s voor formulierfragmenten ingeschakeld.
   * Geef de locatie van **[!UICONTROL existing adaptive form fragments]** op als u bestaande, op JSON-schema&#39;s gebaseerde en niet-adaptieve formulierfragmenten met schema&#39;s hebt en u deze fragmenten wilt gebruiken in automatisch gegenereerde adaptieve formulieren. Conversieservice komt overeen met beschikbare JSON-formulierfragmenten op basis van schema&#39;s en zonder adaptieve formulierfragmenten met invoerfragmenten (alleen niet-interactieve PDF forms), als er een overeenkomst is, wordt het overeenkomende adaptieve formulierfragment gebruikt in de overeenkomende adaptieve formulieren.

   >[!NOTE]
   >
   >
   > * U kunt alleen de optie **[!UICONTROL  Extract Fragment]** of **[!UICONTROL Use existing adaptive form fragments]** tegelijk gebruiken. U kunt niet beide opties tegelijk gebruiken.
   > * U kunt de optie **[!UICONTROL Use existing adaptive form fragments]** alleen gebruiken met niet-interactieve PDF forms. Andere formuliertypen worden nog niet ondersteund.
   > * U kunt alleen ongebonden fragmenten of fragmenten gebruiken die zijn gebonden aan een JSON-schema met de Automated Conversion Service. Gebruik geen XFA-fragmenten. XFA-fragmenten worden niet ondersteund.
   >

   * Selecteer de optie **[!UICONTROL Auto-detect multi-column layout of input forms]** om de indeling van het bronformulier te behouden voor grote schermen zoals desktops en laptops. De optie is handig als u de indeling van bronformulieren met meerdere kolommen wilt behouden. Wanneer een PDF een bronapparaat heeft met twee kolommen, genereert de service bijvoorbeeld een adaptief uitvoerformulier met een indeling met twee kolommen voor schermschermen met groot scherm en een lay-out met één kolom voor apparaten met klein scherm, zoals mobiele telefoons. De eigenschap heeft sommige bekende kwesties met de structuur van het gegevensbronschema. Voor details, zie het [ gekende-kwesties ](known-issues.md) artikel.
   * De service creëert standaard een aparte, bovenliggende laag voor elke pagina van een PDF-formulier. Met de optie **[!UICONTROL Auto-detect logical sections]** kunt u nu geen deelvensters op paginaniveau (op paginanummers gebaseerde deelvensters) maken en alleen logische deelvensters maken. Hierbij worden ook de velden die niet bij een sectie met een voorafgaande logische sectie horen en de velden van een logische sectie die verspreid zijn over twee aangrenzende pagina&#39;s samengevoegd tot één enkele logische sectie. Als sommige velden van een logische sectie bijvoorbeeld aan het einde van pagina 1 staan en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden samengevoegd tot één enkele logische sectie.

     >[!NOTE]
     > U hebt het connectorpakket 1.1.38 of hoger nodig om de functie **[!UICONTROL Auto-detect logical sections]** te kunnen gebruiken.

* (Alleen AEM Forms as a Cloud Service) De [ Auto-convert secties in fragmenten ] optie is op PDF forms met meer dan 15 pagina&#39;s van toepassing. De gedetecteerde bovenste secties worden omgezet in fragmenten. Ook wordt het uitladen van alle gemaakte fragmenten ingeschakeld. Het verbetert de rendersnelheid van geconverteerde formulieren en maakt het gemakkelijker om grote formulieren in een adaptieve formuliereditor te laden.

  >[!NOTE]
  > Gebruik geen responsieve lay-outsjabloon wanneer u de optie Secties automatisch omzetten in fragmenten gebruikt.
  > Gebruik de revisie en de juiste editor om kleine deelvensters samen te voegen tot een groot venster. Hierdoor wordt het aantal fragmenten in de omgezette adaptieve vorm verminderd.
  > Als u de &quot;teveel vraag&quot;uitzondering ervaart,
  >
  > * het formulier herstructureren om een vereenvoudigde hiërarchie te maken
  > * [ verhoging de waarde van de parameter sling.max.call ] aan een hoog genoeg aantal tot de uitzondering verdwijnt.
  > * [ toename grootte van het geheime voorgeheugen ](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/configure-aem-forms/configure-adaptive-forms-cache.html). De fout treedt op als het formulier te complex is, een groot aantal tabellen heeft en een hiërarchische structuur op meerdere niveaus.

1. Tik op **[!UICONTROL Start Conversion]**. De conversie wordt gestart. De voortgang van de conversie wordt weergegeven op de map of het formulier totdat de conversie wordt uitgevoerd. Het bericht wordt vervangen door een ander statusbericht (geconverteerd, gedeeltelijk geconverteerd of Conversie mislukt) nadat de conversie is voltooid. Na voltooiing van de conversie wordt ook een statuse-mail verzonden naar het geconfigureerde e-mailadres:

   * Wanneer de conversie is gelukt, worden het geconverteerde adaptieve formulier en het bijbehorende schema gedownload naar het pad dat is opgegeven op het tabblad **[!UICONTROL Basic]** van het dialoogvenster voor conversie. Formulierfragmenten en het bijbehorende schema worden alleen gedownload als de optie Fragment extraheren is geselecteerd voordat de conversie wordt gestart.
   * Bij een mislukte conversie wordt het **[!UICONTROL Conversion Failed]** -bericht weergegeven als alle invoerformulieren niet zijn geconverteerd of als het **[!UICONTROL Partially Failed]** -bericht wordt weergegeven wanneer slechts een paar invoerformulieren niet zijn geconverteerd. Een statuse-mail wordt verzonden op het [ gevormde e-mailadres ](configure-service.md#configureemailnotification) en een fout wordt geregistreerd aan het error.log dossier.

   Als u een XFA-gebaseerd PDF formulier converteert naar een adaptief formulier, koppelt de conversieservice het PDF-formulier automatisch aan het geconverteerde adaptieve formulier als de Document of Record-sjabloon. Na de conversie kunt u de adaptieve formuliereigenschappen openen om de sjabloon Document of Record weer te geven in de sectie **[!UICONTROL Document of Record Template Configuration]** van het tabblad **[!UICONTROL Form Model]** . </br>

   De conversieservice uploadt het PDF-formulier alleen automatisch naar het geconverteerde adaptieve formulier als Document of Record-sjabloon als u de optie **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** inschakelt.

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

Real world-forms hebben complexe vereisten voor het vastleggen van gegevens. Zodra de automatische conversie is voltooid, kunnen klanten de conversiekwaliteit van het formulier controleren en de benodigde updates uitvoeren voor het formulier. AEM Forms verstrekt a [ overzicht en correcte ](review-correct-ui-edited.md) redacteur om vereiste veranderingen aan te brengen. Zo kunt u de automatische identificatie van formuliervelden verbeteren en geïdentificeerde velden van het ene type naar het andere converteren. U kunt bijvoorbeeld de indeling van twee kolommen in een formulier bepalen en een veld dat automatisch als keuzerondje wordt aangeduid, wijzigen in een veld met meerdere keuzen.

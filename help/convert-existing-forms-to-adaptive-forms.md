---
title: 'PDF-formulieren converteren naar adaptieve formulieren '
seo-title: 'PDF-formulieren converteren naar adaptieve formulieren '
description: Voer de service Automated Forms Conversion uit om PDF-formulieren te converteren naar adaptieve formulieren
seo-description: Voer de service Automated Forms Conversion uit om PDF-formulieren te converteren naar adaptieve formulieren
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: c0ca850a0a1e82e34364766601011d6367b218ac

---


# PDF-formulieren converteren naar adaptieve formulieren {#convert-print-forms-to-adaptive-forms}

Met de AEM Forms Automated Forms Conversion-service van Adobe Sensei worden uw PDF-formulieren automatisch geconverteerd naar apparaatvriendelijke en responsieve adaptieve formulieren. Of u nu niet-interactieve PDF-formulieren, Acro Forms of op XFA gebaseerde PDF-formulieren gebruikt, de service Automated Forms Conversion kan deze formulieren eenvoudig converteren naar adaptieve formulieren. Zie de service [Automated Forms Conversion](introduction.md) voor informatie over de mogelijkheden, de omzettingsworkflow en de instapkaartgegevens.

## Voorwaarden {#pre-requisites}

* [**De conversieservice configureren **](configure-service.md)

* **De[sjablonen](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html)voorbereiden die op geconverteerde formulieren moeten worden toegepast:** Met behulp van een sjabloon kunt u consistente branding toepassen op alle adaptieve formulieren. Bovendien worden met de service Automated Forms Conversion geen kop- en voettekst van PDF-brondocumenten geëxtraheerd en gebruikt. U kunt adaptieve formuliersjablonen gebruiken om kop- en voettekst op te geven. De kop- en voettekst die in de sjabloon is opgegeven, worden tijdens de conversie op het adaptieve formulier toegepast.

* **Bereid de[thema](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html)&#39;s voor die op geconverteerde formulieren moeten worden toegepast:** Met een thema kunt u een consistente stijl toepassen op alle adaptieve vormen van uw organisatie.

## Het conversieproces starten {#start-the-conversion-process}

Nadat u een AEM-exemplaar hebt aangesloten met AEM Forms Conversion Service, kunt u uw PDF-formulieren converteren naar adaptieve formulieren. Voer de volgende stappen in de vermelde volgorde uit om de formulieren om te zetten:

* [PDF-formulieren uploaden naar uw AEM Forms-server](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [De conversie uitvoeren](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Omgezette formulieren controleren en corrigeren](review-correct-ui-edited.md)

### PDF-formulieren uploaden naar uw AEM Forms-server {#upload-pdf-forms-to-your-aem-forms-server}

De conversieservice converteert PDF-formulieren die beschikbaar zijn in uw AEM Forms-exemplaar naar adaptieve formulieren. U kunt alle PDF-formulieren naar wens tegelijk of gefaseerd uploaden. Houd rekening met het volgende voordat u de formulieren uploadt:

* Houd het aantal formulieren in een map kleiner dan 15 en houd het totale aantal pagina&#39;s in een map kleiner dan 50.
* Houd de map kleiner dan 10 MB. Formulieren niet in een submap bewaren.
* Houd het aantal pagina&#39;s in een formulier kleiner dan 15.
* Upload de beveiligde formulieren niet. De service converteert formulieren die met een wachtwoord zijn beveiligd niet.
* Upload geen bronformulieren met spaties in de bestandsnaam. Verwijder de ruimte uit de naam van het bestand voordat u de formulieren uploadt.
* Upload geen [PDF-portfolio&#39;s](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). De service converteert een PDF-portfolio niet naar een adaptief formulier.
* Lees de secties [Bekende problemen](known-issues.md) en [Beste praktijken en overwegingen](styles-and-pattern-considerations-and-best-practices.md) en breng voorgestelde veranderingen in vormen aan.

Voer de volgende stappen uit om de formulieren te uploaden die moeten worden geconverteerd naar een map in uw AEM Forms-instantie:

1. Meld u aan bij de instantie AEM Forms.

1. Tap **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Tik op **[!UICONTROL Create]**> **[!UICONTROL Folder]**. Geef de **titel** en de **naam** van de map op. Tik op **[!UICONTROL Create]**. Er wordt een map gemaakt.
1. Tik om de nieuwe map te openen.
1. Tik op **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. Selecteer de formulieren die u wilt uploaden, klik **[!UICONTROL Open]** en klik op **[!UICONTROL Upload]**. De formulieren worden geüpload.

### De conversie uitvoeren {#run-the-conversion}

Nadat u de formulieren hebt geüpload en de service hebt geconfigureerd, voert u de volgende stappen uit om de conversie te starten:

1. Tik in uw AEM Forms-instantie op het dialoogvenster **[!UICONTROL Adobe Experience Manager]** ![Conversie-instellingen >](assets/adobeexperiencemanager.png) **[!UICONTROL Navigation]** > ![](assets/compass.png) > **[!UICONTROL Forms]** **[!UICONTROL Forms & Documents]**.
1. Selecteer een formulier of de map met PDF-formulieren (te converteren formulieren) en tik op **[!UICONTROL Start Automated Conversion]**. Het **[!UICONTROL Conversion Settings]** dialoogvenster verschijnt.

   ![De configuraties opgeven](assets/conversion-settings-dialog.png)

1. Op het **[!UICONTROL Basic]** tabblad van het dialoogvenster Conversie-instellingen:

   * **[!UICONTROL Select a cloud configuration]**. Als u een configuratie selecteert, worden de standaardsjabloon en het standaardthema al opgegeven. U kunt desgewenst een andere sjabloon of een thema opgeven.
   * Geef een locatie op waar u gegenereerde adaptieve formulieren en het bijbehorende schema wilt opslaan. U kunt standaardpaden gebruiken of aangepaste paden opgeven.
   * Selecteer met de optie Aangepaste formulieren **genereren zonder bindingen** van gegevensmodellen of u een adaptief formulier wilt genereren met of zonder bindingen van gegevensmodellen.
Als u deze optie niet selecteert, koppelt de conversieservice de adaptieve formulieren automatisch aan een JSON-schema en wordt een gegevensbinding gemaakt tussen de velden in het adaptieve formulier en het JSON-schema. In het **[!UICONTROL Save generated data model schema at]** veld wordt de standaardlocatie weergegeven waar het gegenereerde JSON-schema wordt opgeslagen. U kunt de locatie ook aanpassen om het gegenereerde schema op te slaan.
Als u deze optie selecteert, genereert de conversieservice een adaptief formulier zonder bindingen van gegevensmodellen. Na een geslaagde conversie kunt u een adaptief formulier koppelen aan een formuliergegevensmodel, een XML-schema of een JSON-schema. Zie [Een adaptief formulier](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html)maken voor meer informatie.
   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. Op het **[!UICONTROL Additional]** tabblad Conversie-instellingen
   * Selecteer de **[!UICONTROL Extract fragment from adaptive forms]** optie waarmee de conversieservice formulierfragmenten voor geconverteerde formulieren kan identificeren, uitnemen en downloaden. Wanneer u de **[!UICONTROL Extract fragment from adaptive forms]** optie selecteert, zijn de opties voor het opslaan van geëxtraheerde formulierfragmenten en de bijbehorende formulierfragmenten ingeschakeld.
   * Geef de locatie van **[!UICONTROL existing adaptive form fragments]** op als u bestaande JSON-schemafragmenten en niet-adaptieve formulierfragmenten met een JSON-schema hebt en u deze fragmenten wilt gebruiken in automatisch gegenereerde adaptieve formulieren. Conversieservice komt overeen met beschikbare JSON-formulierfragmenten met een JSON-schema en zonder adaptieve formulierfragmenten met invoer-PDF-formulieren (alleen niet-interactieve PDF-formulieren), als er een overeenkomst is, wordt het overeenkomende adaptieve formulierfragment gebruikt in de bijbehorende adaptieve formulieren.
   >[!NOTE]
   >
   >
   > * U kunt slechts **[!UICONTROL  Extract Fragment]** **[!UICONTROL Use existing adaptive form fragments]** of optie tegelijkertijd gebruiken. U kunt niet beide opties tegelijk gebruiken.
   > * U kunt de **[!UICONTROL Use existing adaptive form fragments]** optie alleen gebruiken met niet-interactieve PDF-formulieren. Andere formuliertypen worden nog niet ondersteund.
   > * U kunt alleen ongebonden fragmenten of fragmenten gebruiken die zijn gebonden aan een JSON-schema met de Automated Conversion Service. Gebruik geen XFA-fragmenten. XFA-fragmenten worden niet ondersteund.


   * Selecteer de **[!UICONTROL Auto-detect multi-column layout of input forms]** optie om de indeling van het bronformulier te behouden voor grote schermen zoals desktops en laptops. De optie is handig als u de indeling van bronformulieren met meerdere kolommen wilt behouden. Als een bron-PDF bijvoorbeeld een indeling met twee kolommen heeft, genereert de service een adaptief uitvoerformulier met een indeling met twee kolommen voor schermschermen met groot scherm en een lay-out met één kolom voor apparaten met klein scherm, zoals mobiele telefoons. De eigenschap heeft sommige bekende kwesties met de structuur van het gegevensbronschema. Zie het [artikel over bekende problemen](known-issues.md) voor meer informatie.
   * Standaard maakt de service een apart bovenste venster voor elke pagina van een PDF-formulier. U kunt nu de **[!UICONTROL Auto-detect logical sections]** optie gebruiken om geen deelvensters op paginaniveau (op paginanummers gebaseerde deelvensters) te maken en alleen logische deelvensters te maken. De velden die niet tot een sectie met een voorafgaande logische sectie behoren, en velden van een logische sectie die zich over twee aangrenzende pagina&#39;s uitstrekken, worden in één logische sectie samengevoegd. Als sommige velden van een logische sectie zich bijvoorbeeld aan het einde van pagina 1 bevinden en sommige zich aan het begin van pagina 2 bevinden, worden al deze velden opgenomen in één logische sectie.

      >[!NOTE]
      > U hebt het schakelaarpakket 1.1.38 of hierboven nodig om de **[!UICONTROL Auto-detect logical sections]** eigenschap te gebruiken.



1. Tik op **[!UICONTROL Start Conversion]**. De conversie wordt gestart. De voortgang van de conversie wordt weergegeven op de map of het formulier totdat de conversie wordt uitgevoerd. Het bericht wordt vervangen door een ander statusbericht (geconverteerd, gedeeltelijk geconverteerd of Conversie mislukt) nadat de conversie is voltooid. Na voltooiing van de conversie wordt ook een statuse-mail verzonden naar het geconfigureerde e-mailadres:

   * Als de conversie is gelukt, worden het geconverteerde adaptieve formulier en het bijbehorende schema gedownload naar het pad dat is opgegeven op het **[!UICONTROL Basic]** tabblad van het conversiedialoogvenster. Formulierfragmenten en het bijbehorende schema worden alleen gedownload als de optie Fragment extraheren is geselecteerd voordat de conversie wordt gestart.
   * Bij een mislukte conversie wordt het **[!UICONTROL Conversion Failed]** bericht weergegeven als alle invoerformulieren niet zijn geconverteerd of als het **[!UICONTROL Partially Failed]** bericht wordt weergegeven wanneer slechts een paar invoerformulieren niet zijn geconverteerd. Er wordt een status-e-mail verzonden naar het [geconfigureerde e-mailadres](configure-service.md#configureemailnotification) en er wordt een fout geregistreerd naar het bestand error.log.
   Als u een PDF-formulier op basis van XFA converteert naar een adaptief formulier, wordt het PDF-formulier door de conversieservice automatisch gekoppeld aan het geconverteerde adaptieve formulier als Document of Record-sjabloon. Na de conversie kunt u de adaptieve formuliereigenschappen openen om de sjabloon Document of Record weer te geven in de **[!UICONTROL Document of Record Template Configuration]** sectie van het **[!UICONTROL Form Model]** tabblad. </br>

   De conversieservice uploadt het PDF-formulier alleen automatisch naar het geconverteerde adaptieve formulier als de sjabloon Document of Record als u de optie **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** inschakelt.

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
   >Als het conversieproces meer dan 60 minuten in beslag neemt en het PDF-formulier nog steeds niet is geconverteerd naar een adaptief formulier, maakt u een map op de AEM Forms-instantie, uploadt u het PDF-formulier naar de nieuwe map en start u de conversie opnieuw.

## Review and correct the converted forms {#review-and-correct-the-converted-forms}

In werkelijkheid hebben formulieren complexe vereisten voor het vastleggen van gegevens. Zodra de automatische conversie is voltooid, kunnen klanten de conversiekwaliteit van het formulier controleren en de benodigde updates uitvoeren voor het formulier. AEM Forms biedt een [revisie en juiste](review-correct-ui-edited.md) editor om de vereiste wijzigingen aan te brengen. Zo kunt u de automatische identificatie van formuliervelden verbeteren en geïdentificeerde velden van het ene type naar het andere converteren. U kunt bijvoorbeeld de indeling van twee kolommen in een formulier bepalen en een veld dat automatisch als keuzerondje wordt aangeduid, wijzigen in een veld met meerdere keuzen.

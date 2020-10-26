---
title: Veelgestelde vragen
seo-title: Veelgestelde vragen
description: Veelgestelde vragen of veelgestelde vragen
seo-description: veelgestelde vragen over Automated Forms Conversion Service
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
translation-type: tm+mt
source-git-commit: 92cd241915ef5818fb004a8982674b4f6753c171
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 4%

---


# Veelgestelde vragen{#frequently-asked-questions}

1. **Welke versie van AEM Forms wordt door de Automated Forms Conversion-service ondersteund?**

   <p>Automated Forms Conversion service biedt ondersteuning voor AEM 6.4 Forms en AEM 6.5 Forms. Het werkt met zowel AEM Forms op OSGi als AEM vormen op JEE. Als u de service wilt gebruiken, hebt u het nieuwste AEM Forms-add-on-pakket naast AEM auteurinstantie nodig. For detailed instructions, see <a href="configure-service.md">Configure the Automated Forms Conversion</a> service.</p> 
    <br>

1. **Kan de dienst op-gebouw worden geïnstalleerd?**

   <p>Adobe treert regelmatig AI- en ML-algoritmen van de geautomatiseerde Forms-conversiedienst met nieuwe gegevensverzameling om de conversienauwkeurigheid te verbeteren. De bijgewerkte algoritmen worden op gezette tijden geïmplementeerd op de conversieservice die op Adobe Cloud wordt uitgevoerd. Alle klanten van de dienst worden geprofiteerd van de bijgewerkte algoritmen. Dus, de cloud-gehoste centrale implementatie is het meest geschikt voor de Automated Forms Conversion-service om voortdurend te leren en verbeteringen aan alle klanten te leveren.</p> 
    <p>De service converteert lege formulieren naar adaptieve formulieren. De service ondersteunt geen ingevulde formulieren en het ophalen van gegevens uit ingevulde formulieren. Verwijder gegevens uit ingevulde formulieren en verwijder of lijst van gewenste personen bedrijfsspecifieke informatie uit de formulieren voordat u de formulieren ter conversie naar de service stuurt</p> <br>

1. **Steunt de dienst alle formaten van PDF forms? Welke talen worden ondersteund?**

   <p>De service kan niet-interactieve PDF forms, XDP en PDF forms op basis van XFA en AcroForms converteren naar adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Zie het <a href="known-issues.md">artikel over bekende problemen</a> voor andere beperkingen.<br /> </p> 
    <p>Wij voegen regelmatig steun voor andere brontypes toe. Houd de sectie <a href="introduction.md">supportedPDF-formulieren</a> op uw controlelijst voor een regelmatige update van nieuw toegevoegde functies en mogelijkheden.</p>

   De service kan alleen Engelstalige formulieren converteren naar adaptieve formulieren. U kunt de gegenereerde adaptieve formulieren naar een andere taal vertalen met de [AEM-vertaalworkflow.](https://helpx.adobe.com/nl/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Kan de service een XDP produceren in plaats van een adaptief formulier?**

   <p>De service produceert geen XDP-uitvoer. Wij voegen regelmatig eigenschappen en aan de dienst toe. Houd de <a href="introduction.md">ondersteunde talen en PDF forms</a> op uw controlelijst voor een regelmatige update van nieuw toegevoegde functies en mogelijkheden.</p> <br>

1. **Wat is het type gegenereerd schema?**

   <p>U kunt de service gebruiken om het volgende te genereren: </p>

   * een adaptief formulier gebonden aan een JSON-schema en
   * een adaptief formulier dat niet aan een schema is gebonden <br><br>

1. **Kan de service een Microsoft Word-formulier converteren naar adaptieve formulieren?**

   <p>Nee, de service converteert een Microsoft Word-formulier niet naar een adaptief formulier. U kunt een Microsoft Word-formulier opslaan als PDF-formulier en het PDF-formulier converteren naar een adaptief formulier. Het volledige proces is </p> <br>

   1. Met Adobe Acrobat kunt u Word-document [converteren naar een niet-interactieve PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Met Adobe Acrobat kunt u de geproduceerde PDF forms [converteren naar een invulbaar PDF-formulier](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Met Adobe Acrobat kunt u formuliervelden handmatig bijwerken en corrigeren.
   1. Sla het PDF-formulier op. Nu kunt u het formulier met de conversieservice gebruiken om een adaptief formulier te genereren. U kunt het formulier ook gebruiken als Document of Record-sjabloon.


1. **Kan de service gescande papieren formulieren en gekleurde formulieren converteren naar adaptieve formulieren?**

   <p>Met deze service kunt u PDF forms in kleur omzetten in adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Zie het <a href="known-issues.md">artikel over bekende problemen</a> voor andere beperkingen.</p> <br>

1. **Kan de service een gescand formulier of alleen een afbeelding van een formulier converteren naar een adaptief formulier?**

   <p>De service biedt geen ondersteuning voor het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier naar een adaptief formulier te converteren. Zorg dat de afbeelding van het formulier altijd van hoge kwaliteit is als u het wilt converteren in Acrobat. Dit verbetert de kwaliteit van de conversie.</p> <br>

1. **Sommige op XDP gebaseerde formulieren gebruiken formulierfragmenten, waar moeten deze formulierfragmenten worden geüpload?**

   <p class="MsoNormal">Upload formulierfragmenten naar de conversiemap en zorg dat de oorspronkelijke mapstructuur behouden blijft. Relatieve paden die worden gebruikt in op XDP gebaseerde formulieren en formulierfragmenten, blijven behouden.</p> <br>

1. **Steunt de dienst schema gebonden XDP vormen? Als ik een XDP verbindend aan een schema heb, moet ik schema aan XDP inbedden?**

   <p>Ja, de dienst steunt schema-gebonden XDP vormen en vereist dat het schema aan de bronXDP vorm wordt ingebed. Wanneer u een schema-gebonden XDP vorm omzet, produceert de dienst een schema JSON. Het JSON-schema is structureel vergelijkbaar met het XSD-schema van XDP-bronformulieren.</p> <br>

1. **De service heeft formulieren niet geconverteerd. Wat is de reden en hoe moet dit probleem worden opgelost?**
De meest voorkomende redenen voor het mislukken van de conversie zijn:
</p>
   * Voor de conversie worden beveiligde PDF forms verstrekt. Gebruik geen met wachtwoord beveiligde of beveiligde PDF forms voor conversie.
   * De internetverbinding wordt onderbroken. Zorg ervoor dat u tijdens de conversie verbinding hebt met internet.
   * De bron-PDF heeft een afbeelding van het formulier in plaats van het daadwerkelijke formulier.
   * De service is onjuist geconfigureerd, de service-URL is niet opgegeven of de service-URL is onjuist. Controleer de [serviceconfiguratie](configure-service.md#configure-the-cloud-service) op **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-configuratie is niet correct geconfigureerd. Voer een gezondheidscontrole op de configuratie IMS uit om ervoor te zorgen dat het behoorlijk werkt. Controleren of de IMS-configuratie correct is of niet:
      1. Go to `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Selecteer de configuratie. Klik op de **[!UICONTROL Check Health]** knop in de koptekst en klik op **[!UICONTROL Check]**. Als dit gelukt is, krijgt u een **[!UICONTROL Token retrieved successfully!]** bericht. <br> <br>

1. **Heeft het gebruik van aangepaste lettertypen invloed op de conversie?**

   <p>Wanneer een niet-interactief PDF-formulier wordt geconverteerd naar een adaptief formulier, worden de fonts ingesloten in het PDF-formulier om de conversiekwaliteit te verbeteren. De ondersteuning voor het insluiten van lettertypen is beperkt tot niet-interactieve PDF forms. Voor een optimale conversie van op AcroForm en XFA gebaseerde PDF forms worden fallback-lettertypen gebruikt.</p> 
    <p>Alleen formulieren die beschikbaar zijn in de map met aangepaste lettertypen die wordt vermeld in het directoryveld <strong>voor</strong> klantlettertypen van de configuratie <strong> CQ-DAM-Handler-Gibson Font Manager Service</strong> , worden ingesloten in een niet-interactief PDF-formulier.</p> 
    <p> </p> <br>

1. **Identificeert en gebruikt de service fonts van bron-PDF in uitvoeradaptieve formulieren?**

   <p>De stijl en indeling van een responsief HTML-formulier wijkt doorgaans af van een PDF- of op papier gebaseerd formulier. Om consistente opmaak en opmaak in alle organisaties te ondersteunen, gebruiken adaptieve formulieren <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">thema's om een formulier</a>op te maken. De conversieservice gebruikt de lettertypen en lettertypestijlen die zijn opgegeven in het thema dat tijdens de conversie is toegepast. U kunt lettertypen en lettertypestijlen van het thema wijzigen om de componenten van een adaptief formulier een duidelijk uiterlijk te geven.</p> <br>

1. **Extraheert de service JavaScript automatisch uit XDP-formulieren en past deze toe op overeenkomstige adaptieve formulieren?**

   <p>De service converteert scripts van XFA-formulieren of Acro Forms niet automatisch naar overeenkomende aangepaste formulierregels. U (formulierauteurs) kunt de <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">regeleditor</a> gebruiken om interactiviteit toe te voegen aan een adaptief formulier.</p> <br>

1. **Sommige formulierobjecten worden niet correct geconverteerd naar adaptieve formuliercomponenten. Hoe kan dit probleem worden opgelost?**

   <p>De geautomatiseerde Forms Conversion-service is opgeleid voor een groot aantal formulieren. Maar op AI/ML gebaseerde toepassingen worden beperkt door hun trainingsgegevens en patronen. Er kunnen meerdere veldtypen, indelingen, patronen en context zijn die zichtbaar zijn voor menselijke perceptie, maar moeilijk zijn voor automatische herkenning. De dienst kan dergelijke voorwerpen niet identificeren of hen verkeerd erkennen. U kunt de redacteur van de <a href="review-correct-ui-edited.md" target="_blank">Overzicht en van de Correctie</a> gebruiken om noodzakelijke veranderingen in de vertrouwde op vorm gebaseerd indeling van het papieren formulier van de inputvorm aan te brengen.</p> <br/>

1. **Sommige correcties worden in verschillende formulieren herhaald. Kan de dienst alle dergelijke instanties in toekomstige omzettingen identificeren en bevestigen?**

   De service biedt voortdurend training voor uw formulieren en patronen. Het leert nieuwe patronen dagelijks. Het is nog niet mogelijk om automatisch toegepaste correcties toe te passen die in de verschillende formulieren worden herhaald. Voor de beschikbaarheid van een dergelijke functie moet u de pre-releaseformulieren in de gaten houden. <br/><br/>

   U kunt het metamodel gebruiken om de formulierobjecten toe te wijzen aan een aangepaste formuliercomponent van uw keuze en validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen voor de componenten vooraf te configureren. Alle opgegeven eigenschappen worden tijdens de conversie toegepast. U kunt het metamodel gebruiken om gemeenschappelijke eigenschappen op gebieden toe te passen. Hiermee kunt u bepaalde herhaalde problemen in verschillende formulieren verminderen.<br/><br/>

1. **Wat zijn de opties voor formulieren met gevoelige gegevens, zoals PII-gegevens (Personal Identified Information)?**
De service ondersteunt alleen lege of niet-ingevulde formulieren. Upload geen ingevulde formulieren of formulieren met persoonlijk identificeerbare gegevens (PII). Verwijder ook voorgevulde gegevens, persoonlijk identificeerbare informatie (PII), vertrouwelijke informatie en merkgebonden informatie in bronformulieren. 
<br/>

1. **Waar moeten de kop- en voetteksten worden geplaatst?**

   <p>Plaats de kop- en voettekst in een sjabloon voor aangepaste formulieren. Als het bron-PDF-formulier koptekst en voettekst bevat, detecteert en vervangt de service gedetecteerde kop- en voettekst door een kop- en voettekst die beschikbaar is in een adaptief formuliersjabloon tijdens de conversie. Als het aangepaste formulier een extra kop- of voettekst bevat, kunt u de editor <a href="review-correct-ui-edited.md">Reviseren en corrigeren</a> gebruiken om de kop- of voettekst te herstellen of te verwijderen.</p> <br />

1. **Hoeveel tijd bespaart de dienst in vergelijking met het handproces om activa (thema&#39;s, malplaatjes) te plannen, te creëren, en het publiceren van een adaptief vorm?**

   <p>De hoeveelheid tijd is afhankelijk van de grootte en complexiteit van invoerformulieren en het aantal aanvragen. De service is van plan de tijd die nodig is om waarde te bereiken aanzienlijk te beperken door PDF forms in veel sneller tempo om te zetten in adaptieve formulieren dan bij het handmatig converteren van formulieren. </p> <br />

1. **Wat te doen als ik een fout met betrekking tot bibliotheken RSA ontmoet? Het foutbericht is vergelijkbaar met het onderstaande bericht:** <br/>

De bovengenoemde fout komt voor wanneer de laarsdelegatie niet voor bibliotheken RSA/BouncyCastle wordt gevormd. Voer de volgende stappen uit om het probleem op te lossen:   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
De bovengenoemde fout komt voor wanneer de laarsdelegatie niet voor bibliotheken RSA/BouncyCastle wordt gevormd. Voer de volgende stappen uit om het probleem op te lossen:
   <p> </p>

   1. Stop de AEM instantie. Navigate to the `[AEM installation directory]\crx-quickstart\conf\` folder. Open het bestand sling.properties voor bewerking. Als u een AEM-instantie `[AEM installation directory]\crx-quickstart\bin\start.bat` wilt starten, bewerkt u de eigenschappen sling.properties op `[AEM_root]\crx-quickstart\`.
   1. Voeg de volgende eigenschappen toe aan het bestand sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Sla het bestand op en sluit het. <br/>
   1. Start de AEM.<br/>

   <br/>

1. **Hoe wijzigt u automatisch het omhulsel van adaptieve formuliertekst?**

   <p>U kunt adaptief vanuit thema's of stijleditor gebruiken om de behuizing van een veld met een adaptief formulier te wijzigen. U kunt bijvoorbeeld de themaeditor openen en de waarde van de eigenschap Case van alle tekst van het formulier instellen op hoofdletters, kleine letters of hoofdletters. U kunt ook de optie CSS overschrijven in de themaeditor gebruiken om verschillende typen stijlen te maken.</p>

1. **Kan ik Adobe Sign-teksttags gebruiken met de Automated Forms Conversion-service?**

   <p> Wanneer u de Automated Forms Conversion Service gebruikt om een PDF-formulier te converteren naar een adaptief formulier en het PDF-formulier heeft Adobe Sign-tekstcodes, worden deze codes geconverteerd naar de bijbehorende adaptieve formuliervelden en worden de ondertekenaardetails automatisch ingevuld.  Deze functie is alleen beschikbaar voor Acro Forms en adaptieve formulieren ondersteunen een beperkt aantal Adobe Sign-velden.</p>  </br>

1. **Hoe maakt u een PDF-formulier dat geschikt is voor Adobe Sign?**

   </p>Een PDF-formulier maken dat geschikt is voor Adobe Sign:</p>

   Voeg [Adobe Sign-tekstcodes](https://helpx.adobe.com/sign/using/text-tag.html) toe aan veldnamen of gebruik de optie [Converteren naar Adobe Sign-formulier](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) .

---
title: Veelgestelde vragen
seo-title: Frequently asked questions
description: Veelgestelde vragen of veelgestelde vragen
seo-description: frequently asked questions for Automated Forms Conversion Service
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: 298d6c0641d7b416edb5b2bcd5fec0232f01f4c7
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 4%

---

# Veelgestelde vragen{#frequently-asked-questions}

1. **Welke versie van AEM Forms steunt de dienst van de Automatede form conversion?**
   <p>De dienst van de automatede form conversion steunt AEM 6.4 Forms en AEM 6.5 Forms. Het werkt met zowel AEM Forms op OSGi als AEM vormen op JEE. Als u de service wilt gebruiken, hebt u het nieuwste AEM Forms-add-on-pakket naast AEM auteurinstantie nodig. Zie voor gedetailleerde instructies <a href="configure-service.md">De Automatede form conversion configureren</a> service.</p> 
    <br>

1. **Kan de dienst op-gebouw worden geïnstalleerd?**
   <p>Adobe voert regelmatig AI- en ML-algoritmen van Automatede form conversion uit met nieuwe gegevensverzameling om de nauwkeurigheid van de conversie te verbeteren. De bijgewerkte algoritmen worden op gezette tijden geïmplementeerd op de conversieservice die op Adobe Cloud wordt uitgevoerd. Alle klanten van de dienst worden geprofiteerd van de bijgewerkte algoritmen. Dus, de wolk-ontvangen centrale plaatsing is het best geschikt voor de dienst van de Automatede form conversion om onophoudelijk verbeteringen aan alle klanten te leren en te leveren.</p> 
    <p>De service converteert lege formulieren naar adaptieve formulieren. De service ondersteunt geen ingevulde formulieren en het ophalen van gegevens uit ingevulde formulieren. Verwijder gegevens uit ingevulde formulieren en verwijder of lijst van gewenste personen bedrijfsspecifieke informatie uit de formulieren voordat u de formulieren ter conversie naar de service stuurt</p> <br>

1. **Steunt de dienst alle formaten van PDF forms? Welke talen worden ondersteund?**
   <p>De service kan niet-interactieve PDF forms, XDP en PDF forms op basis van XFA en AcroForms converteren naar adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Voor andere beperkingen raadpleegt u de <a href="known-issues.md">bekende problemen</a> artikel.<br /> </p> 
    <p>Wij voegen regelmatig steun voor andere brontypes toe. De <a href="introduction.md">supportedPDF-formulieren</a> voor een regelmatige update van toegevoegde functies en mogelijkheden.</p>

   De service kan alleen de taalformulieren Engels, Frans, Duits, Spaans, Italiaans en Portugees converteren naar adaptieve formulieren. U kunt de gegenereerde adaptieve formulieren naar een andere taal vertalen met de [AEM-vertaalworkflow.](https://helpx.adobe.com/nl/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Kan de service een XDP produceren in plaats van een adaptief formulier?**
   <p>De service produceert geen XDP-uitvoer. Wij voegen regelmatig eigenschappen en aan de dienst toe. De <a href="introduction.md">ondersteunde talen en PDF forms</a> voor een regelmatige update van toegevoegde functies en mogelijkheden.</p> <br>

1. **Wat is het type gegenereerd schema?**
   <p>U kunt de service gebruiken om het volgende te genereren: </p>

   * een adaptief formulier gebonden aan een JSON-schema en
   * een adaptief formulier dat niet aan een schema is gebonden <br><br>

1. **Kan de service een Microsoft Word-formulier converteren naar adaptieve formulieren?**
   <p>Nee, de service converteert een Microsoft Word-formulier niet naar een adaptief formulier. U kunt Microsoft Word-formulieren opslaan in een PDF-formulier en het PDF-formulier converteren naar een adaptief formulier. Het volledige proces is </p> <br>

   1. Adobe Acrobat gebruiken voor [Word-document converteren naar een niet-interactieve PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Adobe Acrobat gebruiken voor [De geproduceerde PDF forms converteren naar een invulbaar PDF-formulier](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Met Adobe Acrobat kunt u formuliervelden handmatig bijwerken en corrigeren.
   1. Sla het PDF-formulier op. Nu kunt u het formulier met de conversieservice gebruiken om een adaptief formulier te genereren. U kunt het formulier ook gebruiken als Document of Record-sjabloon.


1. **Kan de service gescande papieren formulieren en gekleurde formulieren converteren naar adaptieve formulieren?**
   <p>Met deze service kunt u PDF forms in kleur omzetten in adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Voor andere beperkingen raadpleegt u de <a href="known-issues.md">bekende problemen</a> artikel.</p> <br>

1. **Kan de service een gescand formulier of alleen een afbeelding van een formulier converteren naar een adaptief formulier?**
   <p>De service biedt geen ondersteuning voor het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier naar een adaptief formulier te converteren. Zorg dat de afbeelding van het formulier altijd van hoge kwaliteit is als u het wilt converteren in Acrobat. Dit verbetert de kwaliteit van de conversie.</p> <br>

1. **Sommige op XDP gebaseerde formulieren gebruiken formulierfragmenten, waar moeten deze formulierfragmenten worden geüpload?**
   <p class="MsoNormal">Upload formulierfragmenten naar de conversiemap en zorg dat de oorspronkelijke mapstructuur behouden blijft. Relatieve paden die worden gebruikt in op XDP gebaseerde formulieren en formulierfragmenten, blijven behouden.</p> <br>

1. **Steunt de dienst schema gebonden XDP vormen? Als ik een XDP verbindend aan een schema heb, moet ik schema aan XDP inbedden?**
   <p>Ja, de dienst steunt schema-gebonden XDP vormen en vereist dat het schema aan de bronXDP vorm wordt ingebed. Wanneer u een schema-gebonden XDP vorm omzet, produceert de dienst een schema JSON. Het JSON-schema is structureel vergelijkbaar met het XSD-schema van XDP-bronformulieren.</p> <br>

1. **De service heeft formulieren niet geconverteerd. Wat is de reden en hoe moet dit probleem worden opgelost?**
De meest voorkomende redenen voor het mislukken van de conversie zijn:</p>
   * Voor de conversie worden beveiligde PDF forms verstrekt. Gebruik geen met wachtwoord beveiligde of beveiligde PDF forms voor conversie.
   * De internetverbinding wordt onderbroken. Zorg ervoor dat u tijdens de conversie verbinding hebt met internet.
   * Source PDF heeft een afbeelding van het formulier in plaats van het daadwerkelijke formulier.
   * De service is onjuist geconfigureerd, de service-URL is niet opgegeven of de service-URL is onjuist. Controleer de [serviceconfiguratie](configure-service.md#configure-the-cloud-service) om **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-configuratie is niet correct geconfigureerd. Voer een gezondheidscontrole op de configuratie IMS uit om ervoor te zorgen dat het behoorlijk werkt. Controleren of de IMS-configuratie correct is of niet:
      1. Ga naar `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Selecteer de configuratie. Klik op de knop **[!UICONTROL Check Health]** van de koptekst en klik op **[!UICONTROL Check]**. Als dit lukt, krijgt u **[!UICONTROL Token retrieved successfully!]** bericht. <br> <br>

1. **Heeft het gebruik van aangepaste lettertypen invloed op de conversie?**
   <p>Wanneer een niet-interactief PDF formulier wordt geconverteerd naar een adaptief formulier, worden de fonts ingesloten in het PDF-formulier om de conversiekwaliteit te verbeteren. De ondersteuning voor het insluiten van lettertypen is beperkt tot niet-interactieve PDF forms. Voor een optimale conversie van op AcroForm en XFA gebaseerde PDF forms worden fallback-lettertypen gebruikt.</p> 
    <p>Alleen formulieren die beschikbaar zijn in de map met aangepaste lettertypen die in het dialoogvenster <strong>Map met lettertypen van klanten</strong> van het <strong> CQ-DAM-Handler-Gibson Font Manager-service</strong> De configuratie is ingesloten in een niet-interactief PDF-formulier.</p> 
    <p> </p> <br>

1. **Identificeert en gebruikt de dienst doopvonten van bron PDF in output adaptieve vormen?**
   <p>De stijl en indeling van een responsief HTML-formulier wijkt doorgaans af van een PDF- of een op papier gebaseerd formulier. Voor consistente opmaak en opmaak in alle organisaties gebruiken adaptieve formulieren <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">thema's om een formulier op te maken</a>. De conversieservice gebruikt de lettertypen en lettertypestijlen die zijn opgegeven in het thema dat tijdens de conversie is toegepast. U kunt lettertypen en lettertypestijlen van het thema wijzigen om de componenten van een adaptief formulier een duidelijk uiterlijk te geven.</p> <br>

1. **Extraheert de service JavaScript automatisch uit XDP-formulieren en past deze toe op overeenkomstige adaptieve formulieren?**
   <p>De service converteert scripts van XFA-formulieren of Acro Forms niet automatisch naar overeenkomende aangepaste formulierregels. U (formulierauteurs) kunt de opdracht <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">Regeleditor</a> om interactiviteit toe te voegen aan een adaptief formulier.</p> <br>

1. **Sommige formulierobjecten worden niet correct geconverteerd naar adaptieve formuliercomponenten. Hoe kan dit probleem worden opgelost?**
   <p>De service automatede form conversion is opgeleid voor een groot aantal formulieren. Maar op AI/ML gebaseerde toepassingen worden beperkt door hun trainingsgegevens en patronen. Er kunnen meerdere veldtypen, indelingen, patronen en context zijn die zichtbaar zijn voor menselijke perceptie, maar moeilijk zijn voor automatische herkenning. De dienst kan dergelijke voorwerpen niet identificeren of hen verkeerd erkennen. U kunt <a href="review-correct-ui-edited.md" target="_blank">Reviseren en corrigeren</a> editor om de op het gebruikelijke formulier gebaseerde indeling van het invoerformulier aan te passen.</p> <br/>

1. **Sommige correcties worden in verschillende formulieren herhaald. Kan de dienst alle dergelijke instanties in toekomstige omzettingen identificeren en bevestigen?**

   De service biedt voortdurend training voor uw formulieren en patronen. Het leert nieuwe patronen dagelijks. Het is nog niet mogelijk om automatisch toegepaste correcties toe te passen die in de verschillende formulieren worden herhaald. Voor de beschikbaarheid van een dergelijke functie moet u de pre-releaseformulieren in de gaten houden. <br/><br/>

   U kunt het metamodel gebruiken om de formulierobjecten toe te wijzen aan een aangepaste formuliercomponent van uw keuze en validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen voor de componenten vooraf te configureren. Alle opgegeven eigenschappen worden tijdens de conversie toegepast. U kunt het metamodel gebruiken om gemeenschappelijke eigenschappen op gebieden toe te passen. Hiermee kunt u bepaalde herhaalde problemen in verschillende formulieren verminderen.<br/><br/>

1. **Wat zijn de opties voor formulieren met gevoelige gegevens, zoals PII-gegevens (Personal Identified Information)?**
De service ondersteunt alleen lege of niet-ingevulde formulieren. Upload geen ingevulde formulieren of formulieren met persoonlijk identificeerbare gegevens (PII). Verwijder ook voorgevulde gegevens, persoonlijk identificeerbare informatie (PII), vertrouwelijke informatie en merkgebonden informatie in bronformulieren. <br/>

1. **Waar moeten de kop- en voetteksten worden geplaatst?**
   <p>Plaats de kop- en voettekst in een sjabloon voor aangepaste formulieren. Als het bronformulier voor PDF koptekst en voettekst bevat, detecteert en vervangt de service gedetecteerde kop- en voettekst door een kop- en voettekst die beschikbaar is in een adaptieve formuliersjabloon tijdens de conversie. Als er een extra kop- of voettekst in het aangepaste formulier is opgenomen, kunt u de opdracht <a href="review-correct-ui-edited.md">Reviseren en corrigeren</a> editor om een dergelijke kop- of voettekst te herstellen of te verwijderen.</p> <br />

1. **Hoeveel tijd bespaart de dienst in vergelijking met het handproces om activa (thema&#39;s, malplaatjes) te plannen, te creëren, en het publiceren van een adaptief vorm?**
   <p>De hoeveelheid tijd is afhankelijk van de grootte en complexiteit van invoerformulieren en het aantal aanvragen. De service is van plan de tijd die nodig is om waarde te bereiken aanzienlijk te beperken door PDF forms in veel sneller tempo om te zetten in adaptieve formulieren dan bij het handmatig converteren van formulieren. </p> <br />

1. **Wat te doen als ik een fout met betrekking tot bibliotheken RSA ontmoet? Het foutbericht is vergelijkbaar met het onderstaande bericht:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
De bovengenoemde fout komt voor wanneer de laarsdelegatie niet voor bibliotheken RSA/BouncyCastle wordt gevormd. Voer de volgende stappen uit om het probleem op te lossen:
   <p> </p>

   1. Stop de AEM instantie. Ga naar de `[AEM installation directory]\crx-quickstart\conf\` map. Open het bestand sling.properties voor bewerking. Als u `[AEM installation directory]\crx-quickstart\bin\start.bat` om een AEM instantie te starten, bewerkt u de eigenschappen sling.property op `[AEM_root]\crx-quickstart\`.
   1. Voeg de volgende eigenschappen toe aan het bestand sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Sla het bestand op en sluit het. <br/>
   1. Start de AEM.<br/>
   <br/>

1. **Hoe wijzigt u automatisch het omhulsel van adaptieve formuliertekst?**
   <p>U kunt adaptief vanuit thema's of stijleditor gebruiken om de behuizing van een veld met een adaptief formulier te wijzigen. U kunt bijvoorbeeld de themaeditor openen en de waarde van de eigenschap Case van alle tekst van het formulier instellen op hoofdletters, kleine letters of hoofdletters. U kunt ook de optie CSS overschrijven in de themaeditor gebruiken om verschillende typen stijlen te maken.</p>

1. **Kan ik Adobe Sign-tekstcodes gebruiken met de service Automatede form conversion?**
   <p> Wanneer u met de service Automatede form conversion een PDF-formulier omzet in een adaptief formulier en het PDF-formulier Adobe Sign-tekstcodes heeft, worden deze codes geconverteerd naar de bijbehorende adaptieve formuliervelden en worden de ondertekenaardetails automatisch ingevuld.  Deze functie is alleen beschikbaar voor Acro Forms en adaptieve formulieren ondersteunen een beperkt aantal Adobe Sign-velden.</p>  </br>

1. **Hoe kan ik een Adobe Sign-formulier voor PDF maken?**
   </p>Een Adobe Sign-formulier voor PDF maken:</p>

   Toevoegen [Adobe Sign-teksttags](https://helpx.adobe.com/sign/using/text-tag.html) om veldnamen te gebruiken of de [Converteren naar Adobe Sign-formulier](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) optie.

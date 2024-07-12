---
title: Veelgestelde vragen
description: Veelgestelde vragen of veelgestelde vragen
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 2%

---

# Veelgestelde vragen{#frequently-asked-questions}

1. **Welke versie van AEM Forms steunt de dienst van de Automatede form conversion (AFCS)?**
   <p>De dienst van de automatede form conversion (AFCS) steunt AEM 6.4 Forms en AEM 6.5 Forms. Het werkt met zowel AEM Forms op OSGi als AEM vormen op JEE. Als u de service wilt gebruiken, hebt u het nieuwste AEM Forms-add-on-pakket naast AEM auteurinstantie nodig. Voor gedetailleerde instructies, zie <a href="configure-service.md"> de Automatede form conversion </a> dienst vormen.</p> 
    <br>

1. **kan de dienst op-gebouw worden geïnstalleerd?**
   <p>Adobe treinen AI- en ML-algoritmen van de dienst Automatede form conversion (AFCS) op regelmatige basis met nieuwe gegevensverzameling om de nauwkeurigheid van de conversie te verbeteren. De bijgewerkte algoritmen worden op periodieke intervallen geïmplementeerd op de conversieservice die op de Adobe Cloud wordt uitgevoerd. Alle klanten van de dienst worden geprofiteerd van de bijgewerkte algoritmen. Dus, de wolk-ontvangen centrale plaatsing is het best geschikt voor de dienst van de Automatede form conversion (AFCS) om onophoudelijk verbeteringen aan alle klanten te leren en te leveren.</p> 
    <p>De service converteert lege formulieren naar adaptieve formulieren. De service ondersteunt geen ingevulde formulieren en het ophalen van gegevens uit ingevulde formulieren. Verwijder gegevens uit ingevulde formulieren en verwijder of lijst van gewenste personen bedrijfsspecifieke informatie uit de formulieren voordat u de formulieren ter conversie naar de service stuurt</p> <br>

1. **steunt de dienst alle formaten van PDF forms? Welke talen worden gesteund?**
   <p>De service kan niet-interactieve PDF forms, XDP- en PDF forms op basis van XFA en AcroForms converteren naar adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Voor andere beperkingen, zie het <a href="known-issues.md"> bekende kwesties </a> artikel.<br /> </p> 
    <p>Wij voegen regelmatig steun voor andere brontypes toe. Houd de <a href="introduction.md"> supportedPDF vormen </a> sectie op uw controlelijst voor een regelmatige update op onlangs toegevoegde eigenschappen en mogelijkheden.</p>

   De service kan alleen de taalformulieren Engels, Frans, Duits, Spaans, Italiaans en Portugees converteren naar adaptieve formulieren. U kunt de geproduceerde adaptieve vormen in een andere taal vertalen gebruikend [ AEM vertaalwerkschema.](https://helpx.adobe.com/nl/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html) </br> </br>

1. **kan de dienst XDP in plaats van een adaptieve vorm veroorzaken?**
   <p>De service produceert geen XDP-uitvoer. Wij voegen regelmatig eigenschappen en aan de dienst toe. Houd de <a href="introduction.md"> gesteunde talen en PDF forms </a> sectie op uw controlelijst voor een regelmatige update op onlangs toegevoegde eigenschappen en mogelijkheden.</p> <br>

1. **wat is het type van geproduceerd schema?**
   <p>U kunt de service gebruiken om het volgende te genereren: </p>

   * een adaptief formulier gebonden aan een JSON-schema en
   * een adaptief formulier dat niet aan een schema is gebonden <br><br>

1. **kan de dienst een vorm van Microsoft Word in adaptieve vormen omzetten?**
   <p>Nee, de service converteert een Microsoft Word-formulier niet naar een adaptief formulier. U kunt Microsoft Word-formulieren opslaan in een PDF-formulier en het PDF-formulier converteren naar een adaptief formulier. Het volledige proces is </p> <br>

   1. Het gebruik Adobe Acrobat om [ het Document van Word in een niet-interactieve PDF ](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html) om te zetten.
   1. Gebruik Adobe Acrobat om [ geproduceerde PDF forms in invulbare vorm van PDF om te zetten ](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Met Adobe Acrobat kunt u formuliervelden handmatig bijwerken en corrigeren.
   1. Sla het PDF-formulier op. Nu kunt u het formulier met de conversieservice gebruiken om een adaptief formulier te genereren. U kunt het formulier ook gebruiken als Document of Record-sjabloon.


1. **Kan de dienst gescande papieren vormen en gekleurde vormen in aanpassingsvormen omzetten?**
   <p>Met deze service kunt u PDF forms in kleur omzetten in adaptieve formulieren. De service ondersteunt geen gescande of ingevulde formulieren. Voor andere beperkingen, zie het <a href="known-issues.md"> bekende kwesties </a> artikel.</p> <br>

1. **kan de dienst een gescande vorm of slechts beeld van een vorm in een adaptieve vorm omzetten?**
   <p>De service biedt geen ondersteuning voor het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier naar een adaptief formulier te converteren. Zorg dat de afbeelding van het formulier altijd van hoge kwaliteit is als u het wilt converteren in Acrobat. Dit verbetert de kwaliteit van de conversie.</p> <br>

1. **sommige op XDP-Gebaseerde vormen gebruiken vormfragmenten, waar zouden deze vormfragmenten moeten worden geupload?**
   <p class="MsoNormal">Upload formulierfragmenten naar de conversiemap en zorg dat de oorspronkelijke mapstructuur behouden blijft. Relatieve paden die worden gebruikt in op XDP gebaseerde formulieren en formulierfragmenten, blijven behouden.</p> <br>

1. **steunt de dienst schema gebonden XDP vormen? Als ik XDP verbindend aan een schema heb, moet ik schema aan XDP inbedden?**
   <p>Ja, de dienst steunt schema-gebonden XDP vormen en vereist dat het schema aan de bronXDP vorm wordt ingebed. Wanneer u een schema-gebonden XDP vorm omzet, produceert de dienst een schema JSON. Het JSON-schema is structureel vergelijkbaar met het XSD-schema van XDP-bronformulieren.</p> <br>

1. **de dienst heeft er niet in geslaagd om vormen om te zetten. Wat is de reden en hoe moet dit probleem worden opgelost?**
De meest voorkomende redenen voor het mislukken van de conversie zijn:</p>
   * Voor de conversie zijn beveiligde PDF forms beschikbaar. Gebruik geen met wachtwoord beveiligde of beveiligde PDF forms voor conversie.
   * De internetverbinding wordt onderbroken. Zorg ervoor dat u tijdens de conversie verbinding hebt met internet.
   * Source PDF heeft een afbeelding van het formulier in plaats van het daadwerkelijke formulier.
   * De service is onjuist geconfigureerd, de service-URL is niet opgegeven of de service-URL is onjuist. Controleer de [ de dienstconfiguratie ](configure-service.md#configure-the-cloud-service) bij **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-configuratie is niet correct geconfigureerd. Voer een gezondheidscontrole op de configuratie IMS uit om ervoor te zorgen dat het behoorlijk werkt. Controleren of de IMS-configuratie correct is of niet:
      1. Ga naar `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Selecteer de configuratie. Klik op **[!UICONTROL Check Health]** in de koptekst en klik op **[!UICONTROL Check]** . Als dit lukt, ontvangt u een **[!UICONTROL Token retrieved successfully!]** -bericht. <br> <br>

1. **gebruikt het gebruiken van douanedoopvonten beïnvloedt omzetting?**
   <p>Wanneer een niet-interactief PDF formulier wordt geconverteerd naar een adaptief formulier, worden de fonts ingesloten in het PDF-formulier om de conversiekwaliteit te verbeteren. De ondersteuning voor het insluiten van lettertypen is beperkt tot niet-interactieve PDF forms. Voor een optimale conversie van op AcroForm en XFA gebaseerde PDF forms worden fallback-lettertypen gebruikt.</p> 
    <p>Slechts zijn de vormen beschikbaar in de folder van douanedoopvonten die in het <strong> wordt vermeld de doopvonten van de Klant folder </strong> gebied van de <strong> CQ-DAM-Handler-Gibson configuratie van de Manager van de Doopvont </strong> ingebed in niet-interactieve vorm van PDF.</p> 
    <p> </p> <br>

1. **identificeert de dienst en gebruikt doopvonten van bron PDF in output adaptieve vormen?**
   <p>De stijl en indeling van een responsief HTML-formulier wijkt doorgaans af van een PDF- of een op papier gebaseerd formulier. Om verenigbare lay-out en het stileren over de organisaties te steunen, gebruiken de adaptieve vormen <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html"> thema's om een vorm </a> te stileren. De conversieservice gebruikt de lettertypen en lettertypestijlen die zijn opgegeven in het thema dat tijdens de conversie is toegepast. U kunt lettertypen en lettertypestijlen van het thema wijzigen om de componenten van een adaptief formulier een duidelijk uiterlijk te geven.</p> <br>

1. **haalt de dienst automatisch JavaScript uit op XDP-Gebaseerde vormen en past het op overeenkomstige aanpassingsvormen toe?**
   <p>De service converteert scripts van XFA-formulieren of Acro Forms niet automatisch naar overeenkomende aangepaste formulierregels. U (vorm-auteurs) kunt de <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html"> redacteur van de Regel </a> gebruiken om interactiviteit aan een adaptieve vorm toe te voegen.</p> <br>

1. **sommige vormvoorwerpen worden niet correct omgezet in adaptieve vormcomponenten. Hoe los je het probleem op?**
   <p>De service automatede form conversion (AFCS) is opgeleid op een groot aantal formulieren. Maar op AI/ML gebaseerde toepassingen worden beperkt door hun trainingsgegevens en patronen. Er kunnen meerdere veldtypen, indelingen, patronen en context zijn die zichtbaar zijn voor menselijke perceptie, maar moeilijk zijn voor automatische herkenning. De dienst kan dergelijke voorwerpen niet identificeren of hen verkeerd erkennen. U kunt <a href="review-correct-ui-edited.md" target="_blank"> Overzicht gebruiken en </a> redacteur verbeteren om noodzakelijke wijzigingen in de vertrouwde op vorm gebaseerde lay-out van de inputvorm te maken.</p> <br/>

1. **sommige correcties worden herhaald over vormen. Kan de dienst alle dergelijke instanties in toekomstige omzettingen identificeren en bevestigen?**

   De service biedt voortdurend training voor uw formulieren en patronen. Het leert nieuwe patronen dagelijks. Het is nog niet mogelijk om automatisch toegepaste correcties toe te passen die in de verschillende formulieren worden herhaald. Voor de beschikbaarheid van een dergelijke functie moet u de pre-releaseformulieren in de gaten houden. <br/><br/>

   U kunt het metamodel gebruiken om de formulierobjecten toe te wijzen aan een aangepaste formuliercomponent van uw keuze en validaties, regels, gegevenspatronen, Help-tekst en toegankelijkheidseigenschappen voor de componenten vooraf te configureren. Alle opgegeven eigenschappen worden tijdens de conversie toegepast. U kunt het metamodel gebruiken om gemeenschappelijke eigenschappen op gebieden toe te passen. Hiermee kunt u bepaalde herhaalde problemen in verschillende formulieren verminderen.<br/><br/>

1. **wat zijn de opties voor vormen met gevoelige gegevens zoals persoonlijk identificeerbare informatie (PII) informatie?**
De service ondersteunt alleen lege of niet-ingevulde formulieren. Upload geen ingevulde formulieren of formulieren met persoonlijk identificeerbare gegevens (PII). Verwijder ook voorgevulde gegevens, persoonlijk identificeerbare informatie (PII), vertrouwelijke informatie en merkgebonden informatie in bronformulieren. <br/>

1. **waar zou de kopbal en footers moeten worden geplaatst?**
   <p>Plaats de kop- en voettekst in een sjabloon voor aangepaste formulieren. Als het bronformulier voor PDF koptekst en voettekst bevat, detecteert en vervangt de service gedetecteerde kop- en voettekst door een kop- en voettekst die beschikbaar is in een adaptieve formuliersjabloon tijdens de conversie. Als om het even welke extra kopbal of footer in de adaptieve vorm inbegrepen is, kunt u de <a href="review-correct-ui-edited.md"> Overzicht en Correcte </a> redacteur gebruiken om dergelijke kopbal of footer te bevestigen of te verwijderen.</p> <br />

1. **hoeveel tijd sparen de dienst in vergelijking met het handproces om activa (thema&#39;s, malplaatjes) te plannen, te creëren, en een adaptieve vorm te publiceren?**
   <p>De hoeveelheid tijd is afhankelijk van de grootte en complexiteit van invoerformulieren en het aantal aanvragen. De service is van plan de tijd die nodig is om waarde te bereiken aanzienlijk te verminderen door PDF forms in adaptieve formulieren te converteren in een veel sneller tempo dan bij het handmatig converteren van formulieren. </p> <br />

1. **wat te doen als ik een fout met betrekking tot bibliotheken RSA ontmoet? Het foutbericht is vergelijkbaar met het onderstaande bericht:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
De bovengenoemde fout komt voor wanneer de laarsdelegatie niet voor bibliotheken RSA/BouncyCastle wordt gevormd. Voer de volgende stappen uit om het probleem op te lossen:
   <p> </p>

   1. Stop de AEM instantie. Navigeer naar de map `[AEM installation directory]\crx-quickstart\conf\` . Open het bestand sling.properties voor bewerking. Als u `[AEM installation directory]\crx-quickstart\bin\start.bat` gebruikt om een AEM instantie te starten, bewerkt u de eigenschap sling.properties in `[AEM_root]\crx-quickstart\` .
   1. Voeg de volgende eigenschappen aan het sling.properties- dossier toe:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Sla het bestand op en sluit het. <br/>
   1. Start de AEM instantie.<br/>
   <br/>

1. **hoe te om het omhulsel van adaptieve vormtekst automatisch te veranderen?**
   <p>U kunt adaptief vanuit thema's of stijleditor gebruiken om de behuizing van een veld met een adaptief formulier te wijzigen. U kunt bijvoorbeeld de themaeditor openen en de waarde van de eigenschap Case van alle tekst van het formulier instellen op hoofdletters, kleine letters of hoofdletters. U kunt ook de optie CSS overschrijven in de themaeditor gebruiken om verschillende typen stijlen te maken.</p>

1. **kan ik de tekstmarkeringen van Adobe Sign met de dienst van de Automatede form conversion (AFCS) gebruiken?**
   <p> Wanneer u AFCS (Automatede form conversion Service) gebruikt om een PDF-formulier te converteren naar een adaptief formulier en het PDF-formulier Adobe Sign-tekstcodes heeft, worden deze codes geconverteerd naar de bijbehorende adaptieve formuliervelden en worden de ondertekenaardetails automatisch ingevuld.  Deze functie is alleen beschikbaar voor Acro Forms en adaptieve formulieren ondersteunen een beperkt aantal Adobe Sign-velden.</p>  </br>

1. **hoe te om een Adobe Sign toegelaten vorm van PDF tot stand te brengen?**
   </p>Een Adobe Sign-formulier voor PDF maken:</p>

   Voeg [ de tekstmarkeringen van Adobe Sign ](https://helpx.adobe.com/sign/using/text-tag.html) aan gebiedsnamen toe of gebruik [ Omzetten in de Vorm van Adobe Sign ](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) optie.

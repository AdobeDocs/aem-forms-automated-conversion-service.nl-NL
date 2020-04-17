---
title: 'Problemen met Automated Forms Conversion Service oplossen '
seo-title: 'Problemen met de AFCS-service (Automated Forms Conversion Service) oplossen '
description: 'Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen '
seo-description: Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 535267e20fb8e583e1c01f4160be378ffd31a4a4

---


# Problemen met Automated Forms Conversion Service oplossen


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## Algemene fouten {#commonerrors}

| Fout | Voorbeeld |
|--- |--- |
| **Foutbericht**<br> De header van het toegangstoken is niet beschikbaar. <br><br>**Reden **waarom<br>een beheerder meerdere IMS-configuraties heeft gemaakt of de IMS-configuratie de AFCS-service in Adobe Cloud niet kan bereiken.<br><br>**Resolutie**<br> als er veelvoudige configuraties zijn, schrap alle configuraties en [creeer een nieuwe configuratie](configure-service.md#obtainpubliccertificates). <br> Als er één enkele configuratie is, gebruik **[!UICONTROL Health Check]** om connectiviteit [te](configure-service.md#createintegrationoption)controleren. | ![De header van het toegangstoken is niet beschikbaar](assets/invalid-ims-configuration.png) |
| **Foutbericht** <br> Kan geen verbinding maken met de service.  <br><br>**Reden **<br>dat de onjuiste service-URL of geen service-URL wordt vermeld in de cloudservices van Automated Forms Conversion Service.<br><br>**Correctie** van de resolutie <br> Correct [Dienst URL](configure-service.md#configure-the-cloud-service) in de Diensten van de Wolk van de Omzetting van de Automated Forms. | ![Kan geen verbinding maken met de service.](assets/wrong-endpoint-configured.png) |
| **Foutbericht**<br> Het formulier kan niet worden geconverteerd door de service.  <br><br>**Reden **voor<br>netwerkconnectiviteitsproblemen aan uw kant, de service is uitgevallen vanwege gepland onderhoud of uitval in Adobe Cloud.<br><br>**Resolutie**<br> Los de kwesties van de netwerkconnectiviteit aan uw eind op en controleer de status van de dienst op https://status.adobe.com/ voor een geplande of ongeplande stroomonderbreking. | ![Kan geen verbinding maken met de service.](assets/service-failure.png) |
| **Foutbericht**<br> Het aantal pagina&#39;s is meer dan 15.  <br><br>**Reden **<br>voor het bronformulier: meer dan 15 pagina&#39;s.<br><br>**Resolutie** <br> Met Adobe Acrobat kunt u formulieren met meer dan 15 pagina&#39;s splitsen. Breng het aantal pagina&#39;s in een formulier op minder dan 15. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht**<br> Het aantal bestanden is groter dan 15.  <br><br>**Reden **voor<br>de map. De map bevat meer dan 15 formulieren.<br><br>**Resolutie**<br> Breng het aantal formulieren in een map op 15 of lager. Breng het totale aantal pagina&#39;s in een map op minder dan 50. Breng de grootte van de map naar minder dan 10 MB. Formulieren niet in een submap bewaren. Indelen van bronformulieren in een batch van 8-15 formulieren. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht**<br> De indeling van het bronbestand wordt niet ondersteund.  <br><br>**Reden **voor<br>de map met bronformulieren bevatten enkele niet-ondersteunde bestanden.<br><br>**Resolutie**<br> De service ondersteunt alleen .xdp- en .pdf-bestanden. Verwijder bestanden met een andere extensie uit de map en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/unsupported-file-formats.png) |
| **Foutbericht** <br> Gescande formulieren worden niet ondersteund.  <br><br>**Reden **<br>waarom het PDF-formulier alleen gescande afbeeldingen van het formulier bevat en geen inhoudsstructuur.<br><br>**Resolutie**<br> De service ondersteunt het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box niet. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier te converteren naar een adaptief formulier. Gebruik altijd een afbeelding van hoge kwaliteit van het formulier voor conversie in Acrobat. Het verbetert de kwaliteit van de omzetting. | ![Kan geen verbinding maken met de service.](assets/scanned-forms-error.png) |
| **Foutbericht**<br> versleuteld PDF-formulier wordt niet ondersteund.  <br><br>**Reden **voor<br>de map met versleutelde PDF-formulieren.<br><br>**Resolutie**<br> De service ondersteunt het converteren van een versleuteld PDF-formulier naar een adaptief formulier niet. Verwijder de versleuteling, upload het niet-gecodeerde formulier en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/secured-pdf-form.png) |
| **Foutbericht**<br> Kan JSON-schema naar metamodel niet parseren.  <br><br>**Reden **waarom<br>het JSON-schema dat aan de service wordt aangeboden, niet correct is opgemaakt, ongeldige tekens bevat of een ongeldige syntaxis gebruikt om componenten toe te wijzen.<br><br>**Resolutie**<br> Controleer de opmaak van het JSON-bestand. U kunt elke online JSON-validator gebruiken om de opmaak en structuur van het schema te controleren. Zie [Het standaardmetamodel](extending-the-default-meta-model.md) voor meer informatie over de syntaxis van het metamodel uitbreiden. | ![Kan geen verbinding maken met de service.](assets/invalid-meta-model-schema.png) |

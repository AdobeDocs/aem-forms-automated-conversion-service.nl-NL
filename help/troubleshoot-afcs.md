---
title: 'Problemen met Automated Forms Conversion Service oplossen '
seo-title: 'Problemen met de AFCS-service (Automated Forms Conversion Service) oplossen '
description: 'Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen '
seo-description: Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 56e4696c0372223e0b27f1c313382a2a637b6db1

---


# Problemen met Automated Forms Conversion Service oplossen


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## Algemene fouten {#commonerrors}

<!--
|Error|Example|
|--- |--- |
|**Error Message** <br> The access token header is not available. <br><br>**Reason** <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br>**Resolution** <br> If there are multiple configurations, delete all the configurations and [create a new configuration](configure-service.md#obtainpubliccertificates). <br> If there is a single configuration, use **[!UICONTROL Health Check]** to [check connectivity](configure-service.md#createintegrationoption).|![The access token header is not available](assets/invalid-ims-configuration.png)|
|**Error Message** <br> Unable to connect to the service.  <br><br>**Reason** <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br>**Resolution** <br> Correct [Service URL](configure-service.md#configure-the-cloud-service) in Automated Forms Conversion Service Cloud services.|![Unable to connect to the service.](assets/wrong-endpoint-configured.png)|
|**Error Message** <br> The service failed to convert the form.  <br><br>**Reason** <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br>**Resolution** <br> Resolve network connectivity issues at your end and check the status of the service on https://status.adobe.com/ for a planned or unplanned outage.|![Unable to connect to the service.](assets/service-failure.png)|
|**Error Message** <br> The number of pages is more than 15.  <br><br>**Reason** <br> The source form is more than 15 pages long.  <br><br>**Resolution** <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The number of files is more than 15.  <br><br>**Reason** <br>  The folder contains more than 15 forms. <br><br>**Resolution** <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The source file format is not supported.  <br><br>**Reason** <br> The folder containing source forms have some unsupported files. <br><br>**Resolution** <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion. |![Unable to connect to the service.](assets/unsupported-file-formats.png)|
|**Error Message** <br> Scanned forms are not supported.  <br><br>**Reason** <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br>**Resolution** <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion. |![Unable to connect to the service.](assets/scanned-forms-error.png)|
|**Error Message** <br> Encrypted PDF form is not supported.  <br><br>**Reason** <br> The folder contains encrypted PDF forms. <br><br>**Resolution** <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion. |![Unable to connect to the service.](assets/secured-pdf-form.png)|
|**Error Message** <br> Unable to parse meta-model JSON schema.  <br><br>**Reason** <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br>**Resolution** <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, [Extend the default meta-model](extending-the-default-meta-model.md) article for information on meta-model syntax. |![Unable to connect to the service.](assets/invalid-meta-model-schema.png)| -->

<table>
<thead>
<tr>
<th>Fout</th>
<th>Voorbeeld</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Foutbericht</strong><br> De header van het toegangstoken is niet beschikbaar. <br><br><strong>Reden</strong> waarom <br> een beheerder meerdere IMS-configuraties heeft gemaakt of de IMS-configuratie de AFCS-service in Adobe Cloud niet kan bereiken. <br><br><strong>Resolutie</strong><br> als er veelvoudige configuraties zijn, schrap alle configuraties en <a href="configure-service.md#obtainpubliccertificates">creeer een nieuwe configuratie</a>. <br> Als er één configuratie is, gebruik <strong>[!UICONTROL Health Check]</strong> om connectiviteit <a href="configure-service.md#createintegrationoption">te</a>controleren.</td>
<td><img alt="De header van het toegangstoken is niet beschikbaar" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong> <br> Kan geen verbinding maken met de service.  <br><br><strong>Reden</strong> <br> dat de onjuiste service-URL of geen service-URL wordt vermeld in de cloudservices van Automated Forms Conversion Service. <br><br><strong>Correctie</strong> van de resolutie <br> Correct <a href="configure-service.md#configure-the-cloud-service">Dienst URL</a> in de Diensten van de Wolk van de Omzetting van de Automated Forms.</td>
<td><img alt="Kan geen verbinding maken met de service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> Het formulier kan niet worden geconverteerd door de service.  <br><br><strong>Reden</strong> voor <br> netwerkconnectiviteitsproblemen aan uw kant, de service is uitgevallen vanwege gepland onderhoud of uitval in Adobe Cloud. <br><br><strong>Resolutie</strong><br> Los de kwesties van de netwerkconnectiviteit aan uw eind op en controleer de status van de dienst op <a href="https://status.adobe.com/">https://status.adobe.com/</a> voor een geplande of ongeplande stroomonderbreking.</td>
<td><img alt="Het formulier kan niet worden geconverteerd door de service." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> Het aantal pagina's is meer dan 15.  <br><br><strong>Reden</strong><br> voor het bronformulier: meer dan 15 pagina's.  <br><br><strong>Resolutie</strong> <br> Met Adobe Acrobat kunt u formulieren met meer dan 15 pagina's splitsen. Breng het aantal pagina's in een formulier op minder dan 15.</td>
<td><img alt="Het aantal pagina's is groter dan 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> Het aantal bestanden is groter dan 15.  <br><br><strong>Reden</strong> voor <br> de map. De map bevat meer dan 15 formulieren. <br><br><strong>Resolutie</strong><br> Breng het aantal formulieren in een map op 15 of lager. Breng het totale aantal pagina's in een map op minder dan 50. Breng de grootte van de map naar minder dan 10 MB. Formulieren niet in een submap bewaren. Indelen van bronformulieren in een batch van 8-15 formulieren.</td>
<td><img alt="Het aantal bestanden is groter dan 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> De indeling van het bronbestand wordt niet ondersteund.  <br><br><strong>Reden</strong> voor <br> de map met bronformulieren bevatten enkele niet-ondersteunde bestanden. <br><br><strong>Resolutie</strong><br> De service ondersteunt alleen .xdp- en .pdf-bestanden. Verwijder bestanden met een andere extensie uit de map en voer de conversie uit.</td>
<td><img alt="De bronbestandsindeling wordt niet ondersteund." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong> <br> Gescande formulieren worden niet ondersteund.  <br><br><strong>Reden</strong> <br> waarom het PDF-formulier alleen gescande afbeeldingen van het formulier bevat en geen inhoudsstructuur. <br><br><strong>Resolutie</strong><br> De service ondersteunt het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box niet. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier te converteren naar een adaptief formulier. Gebruik altijd een afbeelding van hoge kwaliteit van het formulier voor conversie in Acrobat. Het verbetert de kwaliteit van de omzetting.</td>
<td><img alt="Gescande formulieren worden niet ondersteund." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> versleuteld PDF-formulier wordt niet ondersteund.  <br><br><strong>Reden</strong> voor <br> de map met versleutelde PDF-formulieren. <br><br><strong>Resolutie</strong><br> De service ondersteunt het converteren van een versleuteld PDF-formulier naar een adaptief formulier niet. Verwijder de versleuteling, upload het niet-gecodeerde formulier en voer de conversie uit.</td>
<td><img alt="Gecodeerd PDF-formulier wordt niet ondersteund." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Foutbericht</strong><br> Kan JSON-schema naar metamodel niet parseren.  <br><br><strong>Reden</strong> waarom <br> het JSON-schema dat aan de service wordt aangeboden, niet correct is opgemaakt, ongeldige tekens bevat of een ongeldige syntaxis gebruikt om componenten toe te wijzen.  <br><br><strong>Resolutie</strong><br> Controleer de opmaak van het JSON-bestand. U kunt elke online JSON-validator gebruiken om de opmaak en structuur van het schema te controleren. Zie <a href="extending-the-default-meta-model.md">Het standaardmetamodel</a> voor meer informatie over de syntaxis van het metamodel uitbreiden.</td>
<td><img alt="Kan JSON-metamodel niet parseren" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>

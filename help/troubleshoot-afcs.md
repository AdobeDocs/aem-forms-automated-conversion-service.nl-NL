---
title: 'Problemen met Automated Forms Conversion Service oplossen '
seo-title: 'Problemen met de AFCS-service (Automated Forms Conversion Service) oplossen '
description: 'Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen '
seo-description: Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: c413c5dc2da3a3e7e116b3355c63620f9dab17f8

---


# Problemen met Automated Forms Conversion Service oplossen

Het document bevat basisstappen voor het oplossen van problemen voor algemene fouten.

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## Algemene fouten {#commonerrors}

| Fout | Voorbeeld |
|--- |--- |
| **Foutbericht**<br> De header van het toegangstoken is niet beschikbaar. <br><br> **Reden** waarom <br> een beheerder meerdere IMS-configuraties heeft gemaakt of de IMS-configuratie de AFCS-service in Adobe Cloud niet kan bereiken. <br><br>**Resolutie **<br>als er veelvoudige configuraties zijn, schrap alle configuraties en[creeer een nieuwe configuratie](configure-service.md#obtainpubliccertificates).<br>Als er één configuratie is, gebruik** Gezondheidscontrole **om connectiviteit[te](configure-service.md#createintegrationoption)controleren. | ![De header van het toegangstoken is niet beschikbaar](assets/invalid-ims-configurations.png) |
| **Foutbericht** <br> Kan geen verbinding maken met de service.  <br><br>**Reden **<br>dat de onjuiste service-URL of geen service-URL wordt vermeld in de cloudservices van Automated Forms Conversion Service.<br><br>**Correctie** van de resolutie <br> Correct [Dienst URL](configure-service.md#configure-the-cloud-service) in de Diensten van de Wolk van de Omzetting van de Automated Forms. | ![Kan geen verbinding maken met de service.](assets/wrong-service-url-configured.png) |
| **Foutbericht**<br> Het formulier kan niet worden geconverteerd door de service.  <br><br>**Reden **voor<br>netwerkconnectiviteitsproblemen aan uw kant, de service is uitgevallen vanwege gepland onderhoud of uitval in Adobe Cloud.<br><br>**Resolutie**<br> Los de kwesties van de netwerkconnectiviteit aan uw eind op en controleer de status van de dienst op https://status.adobe.com/ voor een geplande of ongeplande stroomonderbreking. | ![Kan geen verbinding maken met de service.](assets/conversion-failure.png) |
| **Foutbericht**<br> Het aantal pagina&#39;s is meer dan 15.  <br><br>**Reden **<br>voor het bronformulier: meer dan 15 pagina&#39;s.<br><br>**Resolutie** <br> Met Adobe Acrobat kunt u formulieren met meer dan 15 pagina&#39;s splitsen. Breng het aantal pagina&#39;s in een formulier op minder dan 15. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht**<br> Het aantal bestanden is groter dan 15.  <br><br>**Reden **voor<br>de map. De map bevat meer dan 15 formulieren.<br><br>**Resolutie**<br> Breng het aantal formulieren in een map op 15 of lager. Breng het totale aantal pagina&#39;s in een map op minder dan 50. Breng de grootte van de map naar minder dan 10 MB. Formulieren niet in een submap bewaren. Indelen van bronformulieren in een batch van 8-15 formulieren. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht**<br> De indeling van het bronbestand wordt niet ondersteund.  <br><br>**Reden **voor<br>de map met bronformulieren bevatten enkele niet-ondersteunde bestanden.<br><br>**Resolutie**<br> De service ondersteunt alleen .xdp- en .pdf-bestanden. Verwijder bestanden met een andere extensie uit de map en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/unsupported-file-formats.png) |
| **Foutbericht** <br> Gescande formulieren worden niet ondersteund.  <br><br>**Reden **<br>waarom het PDF-formulier alleen gescande afbeeldingen van het formulier bevat en geen inhoudsstructuur.<br><br>**Resolutie**<br> De service ondersteunt het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptieve out-of-the-box niet. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier te converteren naar een adaptief formulier. Gebruik altijd een afbeelding van hoge kwaliteit van het formulier voor conversie in Acrobat. Het verbetert de kwaliteit van de omzetting. | ![Kan geen verbinding maken met de service.](assets/scanned-forms-error.png) |
| **Foutbericht**<br> versleuteld PDF-formulier wordt niet ondersteund.  <br><br>**Reden **voor<br>de map met versleutelde PDF-formulieren.<br><br>**Resolutie**<br> De service ondersteunt het converteren van een versleuteld PDF-formulier naar een adaptief formulier niet. Verwijder de versleuteling, upload het niet-gecodeerde formulier en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/secured-pdf-form.png) |
| **Foutbericht**<br> Kan JSON-schema naar metamodel niet parseren.  <br><br>**Reden **waarom<br>het JSON-schema dat aan de service wordt aangeboden, niet correct is opgemaakt, ongeldige tekens bevat of een ongeldige syntaxis gebruikt om componenten toe te wijzen.<br><br>**Resolutie**<br> Controleer de opmaak van het JSON-bestand. U kunt elke online JSON-validator gebruiken om de opmaak en structuur van het schema te controleren. Zie [Het standaardmetamodel](extending-the-default-meta-model.md) voor meer informatie over de syntaxis van het metamodel uitbreiden. | ![Kan geen verbinding maken met de service.](assets/invalid-meta-model-schema.png) |

<!--

<table>
<thead>
<tr>
<th>Error</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Error Message</strong> <p> The access token header is not available. </p><br><strong>Reason</strong> <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br><strong>Resolution</strong> <br> If there are multiple configurations, delete all the configurations and <a href="configure-service.md#obtainpubliccertificates">create a new configuration</a>. <br> If there is a single configuration, use <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="The access token header is not available" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service Cloud services.</td>
<td><img alt="Unable to connect to the service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The service failed to convert the form.  <br><br><strong>Reason</strong> <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br><strong>Resolution</strong> <br> Resolve network connectivity issues at your end and check the status of the service on <a href="https://status.adobe.com/">https://status.adobe.com/</a> for a planned or unplanned outage.</td>
<td><img alt="The service failed to convert the form." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of pages is more than 15.  <br><br><strong>Reason</strong> <br> The source form is more than 15 pages long.  <br><br><strong>Resolution</strong> <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15.</td>
<td><img alt="The number of pages is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of files is more than 15.  <br><br><strong>Reason</strong> <br>  The folder contains more than 15 forms. <br><br><strong>Resolution</strong> <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms.</td>
<td><img alt="The number of files is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The source file format is not supported.  <br><br><strong>Reason</strong> <br> The folder containing source forms have some unsupported files. <br><br><strong>Resolution</strong> <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion.</td>
<td><img alt="The source file format is not supported." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Scanned forms are not supported.  <br><br><strong>Reason</strong> <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br><strong>Resolution</strong> <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion.</td>
<td><img alt="Scanned forms are not supported." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Encrypted PDF form is not supported.  <br><br><strong>Reason</strong> <br> The folder contains encrypted PDF forms. <br><br><strong>Resolution</strong> <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion.</td>
<td><img alt="Encrypted PDF form is not supported." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to parse meta-model JSON schema.  <br><br><strong>Reason</strong> <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br><strong>Resolution</strong> <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, <a href="extending-the-default-meta-model.md">Extend the default meta-model</a> article for information on meta-model syntax.</td>
<td><img alt="Unable to parse meta-model JSON schema" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
-->
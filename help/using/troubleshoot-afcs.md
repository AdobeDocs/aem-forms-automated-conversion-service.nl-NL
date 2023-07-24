---
title: Problemen oplossen voor de service voor automatische conversie van formulieren
description: Veelvoorkomende problemen met de service voor automatische conversie van formulieren en hun oplossingen
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
contentOwner: khsingh
exl-id: e8406ed9-37f5-4f26-be97-ad042f9ca57c
source-git-commit: e95b4ed35f27f920b26c05f3398529f825948f1f
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 89%

---

# Problemen oplossen voor de service voor automatische conversie van formulieren

Het document bevat basisstappen voor het oplossen van veelvoorkomende problemen.

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## Veelvoorkomende fouten {#commonerrors}

| Fout | Voorbeeld |
|--- |--- |
| **Foutbericht** <br> Koptekst van toegangstoken is niet beschikbaar. <br><br> **Reden** <br> Een beheerder heeft meerdere IMS-configuraties gemaakt of IMS-configuratie kan de AFCS-service op Adobe Cloud niet bereiken. <br><br>**Oplossing** <br> Als er meerdere configuraties zijn, verwijder dan alle configuraties en [maak een nieuwe configuratie aan](configure-service.md#obtainpubliccertificates). <br> Als er één configuratie is, gebruik dan **Statuscontrole** om [de verbinding te controleren](configure-service.md#createintegrationoption). | ![Koptekst van toegangstoken is niet beschikbaar](assets/invalid-ims-configurations.png) |
| **Foutbericht** <br>Kan geen verbinding maken met de service.  <br><br>**Reden** <br> Onjuiste service-URL of er wordt geen service-URL vermeld in de Cloud-services van de service voor de automatische conversie van formulieren. <br><br>**Oplossing** <br> Pas de [service-URL](configure-service.md#configure-the-cloud-service) aan in de Cloud-services van de service voor de automatische conversie van formulieren. | ![Kan geen verbinding maken met de service.](assets/wrong-service-url-configured.png) |
| **Foutbericht** <br> De service kan het formulier niet converteren.  <br><br>**Reden** <br> U heeft problemen met netwerkverbinding, de service is niet beschikbaar vanwege gepland onderhoud of u ziet een onderbreking op Adobe Cloud. <br><br>**Oplossing** <br> Los problemen met uw netwerkverbinding op en controleer de status van de service op https://status.adobe.com/ voor geplande of ongeplande onderbrekingen. | ![Kan geen verbinding maken met de service.](assets/conversion-failure.png) |
| **Foutbericht** <br> Er zijn meer dan 15 pagina&#39;s.  <br><br>**Reden** <br> Het bronformulier bestaat uit meer dan 15 pagina&#39;s.  <br><br>**Oplossing** <br> Gebruik Adobe Acrobat om formulieren van meer dan 15 pagina&#39;s te splitsen. Zorg dat het aantal pagina&#39;s van een formulier minder dan 15 is. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht** <br> Er zijn meer dan 15 bestanden.  <br><br>**Reden** <br>  De map bevat meer dan 15 formulieren. <br><br>**Oplossing** <br> Zorg dat er 15 of minder formulieren in de map zitten. Zorg dat het totale aantal pagina&#39;s in een map minder dan 50 is. Zorg dat de map minder dan 10 MB groot is. Bewaar formulieren niet in submappen. Organiseer bronformulieren in een reeks van 8-15 formulieren. | ![Kan geen verbinding maken met de service.](assets/number-of-pages.png) |
| **Foutbericht** <br> De indeling van het bronbestand wordt niet ondersteund.  <br><br>**Reden** <br> De map met bronformulieren bevat niet-ondersteunde bestanden. <br><br>**Oplossing** <br> De service ondersteunt alleen .xdp- en .pdf-bestanden. Verwijder bestanden met een andere extensie uit de map en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/unsupported-file-formats.png) |
| **Foutbericht** <br> Gescande formulieren worden niet ondersteund.  <br><br>**Reden** <br> Het PDF-formulier bevat alleen gescande afbeeldingen van het formulier en bevat geen inhoudsstructuur. <br><br>**Oplossing** <br> De service biedt geen ondersteuning voor het converteren van gescande formulieren of een afbeelding van een formulier naar een adaptief standaardformulier. Met Adobe Acrobat kunt u de afbeelding van een formulier echter converteren naar een PDF-formulier. Gebruik vervolgens de service om het PDF-formulier naar een adaptief formulier te converteren. Zorg dat de afbeelding van het formulier altijd van hoge kwaliteit is als u het wilt converteren in Acrobat. Dit verbetert de kwaliteit van de conversie. | ![Kan geen verbinding maken met de service.](assets/scanned-forms-error.png) |
| **Foutbericht** <br> Versleuteld PDF-formulier wordt niet ondersteund.  <br><br>**Reden** <br>De map bevat versleutelde PDF-formulieren. <br><br>**Oplossing** <br> De service biedt geen ondersteuning voor het converteren van een versleuteld PDF-formulier naar een adaptief formulier. Verwijder de versleuteling, upload het niet-versleutelde formulier en voer de conversie uit. | ![Kan geen verbinding maken met de service.](assets/secured-pdf-form.png) |
| **Foutbericht** <br> Kan meta-model JSON-schema niet parseren.  <br><br>**Reden** <br> Het JSON-schema dat aan de service wordt geleverd is niet correct geformatteerd, bevat ongeldige tekens of gebruikt ongeldige syntaxis om componenten toe te wijzen.  <br><br>**Oplossing** <br> Controleer de formattering van het JSON-bestand. U kunt elke online JSON-validatie gebruiken om de opmaak en structuur van het schema te controleren. Raadpleeg het artikel [Het standaard meta-model uitbreiden](extending-the-default-meta-model.md) voor meer informatie over meta-model-syntaxis. | ![Kan geen verbinding maken met de service.](assets/invalid-meta-model-schema.png) |
| **Fout (alleen in omgevingen op locatie)** <br> De **[!UICONTROL Source Language]** wordt niet de juiste taal van een adaptief formulier weergegeven. <br><br>**Reden** <br> De eigenschap jcr:language van het adaptieve formulier wordt niet correct ingesteld.  <br><br>**Resolutie** <br> CRX-DE-lijst openen, navigeren naar `/content/forms/af/`, opent u de `jcr:content` en stel de waarde van het knooppunt in op de juiste taal. Voor de lijst met ondersteunde talen raadpleegt u [Ondersteuning voor lokalisatie toevoegen voor niet-ondersteunde landinstellingen](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html#add-localization-support-for-non-supported-locales). | ![Kan geen verbinding maken met de service.](assets/aem-forms-translation-project-language-unavailable.png) |

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

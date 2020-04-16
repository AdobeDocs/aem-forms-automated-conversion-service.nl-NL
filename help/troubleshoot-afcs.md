---
title: 'Problemen met Automated Forms Conversion Service oplossen '
seo-title: 'Problemen met de AFCS-service (Automated Forms Conversion Service) oplossen '
description: 'Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen '
seo-description: Gemeenschappelijke AFCS-kwesties en de bijbehorende oplossingen
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 638d2adec39a4ecba335ae7bdebebd8bf9ab2274

---


# Problemen met Automated Forms Conversion Service oplossen


Het artikel bevat informatie over installatie-, configuratie- en beheerproblemen die zich kunnen voordoen in een productieomgeving van de Automated Forms Conversion Service. Het document bevat ook basisstappen voor het oplossen van problemen en uitleg voor algemene foutberichten.

## Algemene fouten {#commonerrors}

| Fout | Voorbeeld |
|--- |--- |
| **Foutbericht**<br> De header van het toegangstoken is niet beschikbaar. <br><br>**Reden **waarom<br>een beheerder meerdere IMS-configuraties heeft gemaakt of de IMS-configuratie de AFCS-service in Adobe Cloud niet kan bereiken.<br><br>**Resolutie**<br> als er veelvoudige configuraties zijn, schrap alle configuraties en [creeer een nieuwe configuratie](configure-service.md#obtainpubliccertificates). <br> Als er enige configuratie is, gebruik **[!UICONTROL Health Check]** om connectiviteit [te](configure-service.md#createintegrationoption)controleren. | ![De header van het toegangstoken is niet beschikbaar](assets/invalid-ims-configuration.png) |
| **Foutbericht** <br> Kan geen verbinding maken met de service.  <br><br>**Reden **<br>dat de onjuiste service-URL of geen service-URL wordt vermeld in de cloudservices van Automated Forms Conversion Service.<br><br>**Correctie** van de resolutie <br> Correct [Dienst URL](configure-service.md#configure-the-cloud-service) in de Diensten van de Wolk van de Omzetting van de Automated Forms. | ![Kan geen verbinding maken met de service.](assets/wrong-endpoint-configured.png) |
| **Foutbericht** <br> Kan geen verbinding maken met de service.  <br><br>**Reden **<br>dat de onjuiste service-URL of geen service-URL wordt vermeld in de cloudservices van Automated Forms Conversion Service.<br><br>**Correctie** van de resolutie <br> Correct [Dienst URL](configure-service.md#configure-the-cloud-service) in de Diensten van de Wolk van de Omzetting van de Automated Forms. | ![Kan geen verbinding maken met de service.](assets/wrong-endpoint-configured.png) |

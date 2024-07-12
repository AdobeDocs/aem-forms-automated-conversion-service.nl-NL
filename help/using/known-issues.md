---
title: Bekende problemen
description: bekende problemen en beperkingen voor de service Automatede form conversion (AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 35f59e02-e38e-473a-94c8-123e0a85ac8e
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Bekende problemen en beperkingen {#known-issues-limitations}

Voordat u de AEM Forms Automatede form conversion-service (AFCS) gaat gebruiken, moet u de volgende bekende problemen en beperkingen controleren:

## Bekende problemen {#known-issues}

* De map met formulieren voor conversie mag uit maximaal 15 formulieren en uit maximaal 50 pagina&#39;s bestaan. De bronmap mag niet groter zijn dan 10 MB. Maak geen submappen in de bronmap.
* Sommige vormvoorwerpen zijn gemakkelijk zichtbaar aan het menselijke oog maar zijn [ moeilijk om voor de dienst ](styles-and-pattern-considerations-and-best-practices.md) te identificeren. Het overzicht van het gebruik [ en correcte redacteur ](review-correct-ui-edited.md) om dergelijke vormvoorwerpen te identificeren en om te zetten.
* Editor controleren en corrigeren:

   * Heeft geen handeling voor ongedaan maken. Met de knop Opslaan worden de wijzigingen permanent opgeslagen.
   * Biedt geen ondersteuning voor herhaalbare deelvensters voor op XFA gebaseerde formulieren.
   * Als u een lijst in een lijst gebruikend de Redacteur van het Overzicht en van de Correctie wijzigt, past de rijbreedte niet automatisch aan en de tekst zou over aan de volgende rij van de lijst kunnen spill.
   * De functie **[!UICONTROL Auto-detect multi-column layout from input forms]** werkt niet met de redacteur van het Overzicht en van het Correct en Fragments van de Vorm.
   * De scripthandtekening die is gemaakt met de redacteur voor revisie en correctie kan niet worden geladen voor gepubliceerde adaptieve formulieren.


* Voor XFA-formulieren:
   * Het uitpakken van fragmenten uit een XFA-formulier wordt niet ondersteund.
   * XFA-scripts worden niet ondersteund. Bijvoorbeeld, manuscripten voor automatisch het produceren van waarden voor een drop-down component.
   * Meta-model werkt niet voor de keuzegroep
   * De optie Keuzegroepen met één teken wordt niet geïdentificeerd
   * Wanneer het brondocument een dynamisch XFA (.XDP) is en het [ gedrag van eigenschappen XFA in een adaptieve vorm ](https://helpx.adobe.com/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr) bepaalt, dan wordt het aanwezigheidsbezit van brondocument niet geëerd. Een veld in een brondocument is bijvoorbeeld gemarkeerd als verborgen en een script maakt het veld zichtbaar, maar het veld blijft zichtbaar in het adaptieve uitvoerformulier.

* Wanneer u **invoerAcroForm van het Gebruik als Document van Verslag (DoR) voor geproduceerde adaptieve vormen** optie gebruikt, overweeg het volgende:

<table>
    <tr>
        <td>Binding en gegevens gaan verloren voor samengestelde tekstvelden. Een samengesteld tekstveld heeft meerdere tekstvakken die met elkaar zijn uitgelijnd. In een AcroForm wordt bijvoorbeeld een creditcardnummer gesplitst in meerdere tekstvakken en heeft elk tekstvak een aparte binding. Wanneer het AcroForm-formulier wordt geconverteerd naar een adaptief formulier, heeft het geconverteerde adaptieve formulier één binding voor alle tekstvakken. Voordat u een AcroForm-formulier omzet in een adaptief formulier, kunt u als tijdelijke oplossing het AcroForm-formulier aanpassen en het enkele tekstvak gebruiken om creditcardnummers te accepteren.</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>Binding en gegevens gaan verloren voor samengestelde datumvelden. Een samengesteld datumveld bestaat uit drie verschillende velden. Een geboorteveld in een AcroForm wordt bijvoorbeeld opgedeeld in drie afzonderlijke velden. Het adaptieve formulier bevat een uit-de-doos datumkiezer. Als u de datumkiezer-component van het adaptieve formulier wilt gebruiken terwijl de binding van het AcroForm behouden blijft, wijzigt u het AcroForm-formulier zodat het formulier met één datum wordt geconverteerd naar een adaptief formulier.</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>Als de grootte van de selectievakjes groter is dan de bijbehorende tekst, worden de selectievakjes niet gedetecteerd en gaat de binding in het AcroForm verloren. Wijzig het AcroForm om de grootte van de selectievakjes kleiner te maken dan de bijbehorende tekst.</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>Als de invoervelden niet worden uitgelijnd op het overeenkomstige tekstveld, wordt het invoerveld niet gedetecteerd.  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>De service converteert alle selectievakjes van een AcroForm-formulier naar afzonderlijke keuzegroepen. Er worden afzonderlijke keuzesegroepen gemaakt om bindingen met AcroForm te behouden. Voeg geen keuzesegroepen in de aangepaste vorm samen. Het zal leiden tot het verlies van bindingen. Als u de keuzegroepen samenvoegt, zet u het formulier opnieuw om de verloren bindingen te herstellen. </td>
        <td></td>
    </tr>
    <tr >
        <td>De grenzen van sommige lijsten worden uitgebreid uit de pagina in automatisch geproduceerd document van verslag (DoR). </td>
        <td></td>
    </tr>
</table>

## Beperkingen {#limitations}

* PDF forms met een complexe dynamische indeling, velden met gestippelde omtrek of gevulde velden worden niet ondersteund.
* Afbeeldingen en tekst in de afbeeldingen worden niet geïdentificeerd. Voeg handmatig afbeeldingen toe aan geconverteerde formulieren.
* XDP-illustraties worden niet ondersteund.
* PDF forms die groter zijn dan 15 pagina&#39;s, worden niet ondersteund.
* Gecodeerde, met een wachtwoord beveiligde en beveiligde documenten worden niet geconverteerd. Verwijder codering of wachtwoorden voordat u de conversie uitvoert.
* Complexe tabellen, zoals tabellen zonder kader, geneste tabellen en tabellen met plaatsaanduidingswaarden, worden niet ondersteund. Gebruik de aangepaste formuliereditor om na de conversie complexe tabellen toe te voegen of te wijzigen. Alleen eenvoudige tabellen met lege velden, juiste kopteksten en duidelijke grenzen worden ondersteund.
* De service converteert alleen de taalformulieren Engels, Frans, Duits, Spaans, Italiaans en Portugees naar adaptieve formulieren. U kunt omgezette adaptieve vormen in een andere taal vertalen gebruikend [ AEM vertaalwerkschema ](https://helpx.adobe.com/nl/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).
* AEM 6.4 Forms biedt geen ondersteuning voor automatische detectie van meerkolomindeling van invoerformulieren.
* Informatie die is gecodeerd met kleuren in het PDF-bronformulier, wordt niet overgedragen naar het adaptieve formulier.
* Kleuren van het PDF-bronformulier worden niet overgedragen naar adaptieve formulierthema&#39;s.
* Gekleurde PDF forms worden behandeld als grijswaardenformulieren en velden worden dienovereenkomstig gedetecteerd.

---
title: Übersicht über die Edge-Implementierung
description: Richten Sie das Adobe Experience Platform-Schema, den Datensatz und den Datenstrom ein, die erforderlich sind, um Streaming-Mediendaten über die Edge Network zu erfassen.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 5%

---

# Übersicht über die Edge-Implementierung

Mit Adobe Experience Platform Edge Network können Sie Daten, die für mehrere Produkte bestimmt sind, an einen einzelnen Endpunkt senden, der dann die entsprechenden Informationen an jedes Produkt weiterleitet. Dies ist die empfohlene Methode zur Implementierung der Streaming Media Collection und der einzige Ansatz, der sowohl Adobe Analytics als auch Customer Journey Analytics von einer einzigen Implementierung aus unterstützt.

Im Gegensatz zum älteren Media SDK-Ansatz, der für jede Adobe-Lösung eine produktspezifische Instrumentierung erforderte, verwendet eine Edge-Implementierung ein gemeinsames XDM-Datenmodell und einen einzigen Datenstrom. Daten fließen von Ihrer SDK oder API zu Edge Network, das sie dann an die im Datenstrom konfigurierten Adobe-Produkte weiterleitet (Analytics, CJA, AJO oder RTCDP). Das bedeutet, dass das Wechseln oder Hinzufügen nachgelagerter Produkte zu einem späteren Zeitpunkt keine erneute Instrumentierung Ihrer Medienereignisse erfordert.

Unabhängig davon, welche Codebasis Sie verwenden, müssen Sie zunächst die auf dieser Seite beschriebene Plattformeinrichtung abschließen: Erstellen eines Schemas, Erstellen eines Datensatzes und Konfigurieren eines Datenstroms.

## Voraussetzungen

1. **Vervollständigen Sie die allgemeinen Voraussetzungen.** Siehe [Allgemeine Voraussetzungen](/help/getting-started/prereqs.md).

1. **Bestätigen einer kompatiblen Adobe-Lösung.** Es muss eine funktionierende Implementierung aus mindestens einem der folgenden Elemente vorhanden sein:
   * [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=de): Das primäre Berichtsziel für Edge-basierte Mediendaten
   * [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de): Wird zusammen mit oder anstelle von CJA über denselben Datenstrom unterstützt
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de) oder [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=de): Fügen Sie den **[!UICONTROL Adobe Experience Platform]**-Service zu Ihrem Datenstrom hinzu, wenn Sie eine dieser Konfigurationen durchführen

## Einrichten des Schemas in Adobe Experience Platform

Um die Datenerfassung in allen Anwendungen zu standardisieren, die Adobe Experience Platform verwenden, hat Adobe den offenen, öffentlich dokumentierten Experience-Datenmodell (XDM)-Standard erstellt.

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Schemas, wie unter [Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en) beschrieben.

1. Wählen Sie auf der Seite mit den **[!UICONTROL „Erlebnisereignis]** als Basisklasse für das Schema aus.

   ![Feldergruppen hinzugefügt](assets/schema-experience-event.png)

1. Klicken Sie auf **[!UICONTROL Weiter]**.

1. Geben Sie einen Anzeigenamen und eine Beschreibung für das Schema an und wählen Sie dann **[!UICONTROL Beenden]**.

1. Wählen Sie im Bereich **[!UICONTROL Komposition]** im Abschnitt **[!UICONTROL Feldergruppen]** die Option **[!UICONTROL Hinzufügen]** aus, suchen Sie dann nach den folgenden Feldergruppen und fügen Sie sie zum Schema hinzu:
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nachdem Sie die Feldergruppen hinzugefügt haben, werden sie im Abschnitt **[!UICONTROL Feldergruppen]** angezeigt:

   ![Feldergruppen hinzugefügt](assets/schema-field-groups-added.png)

1. Klicken Sie **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern.

1. (Optional) Sie können bestimmte Felder in der Schema-Benutzeroberfläche ausblenden. Diese Felder sind Server-berechnete Berichtsfelder, die Adobe im Backend ausfüllt - sie werden nicht von Ihrer SDK oder API gesendet und wirken sich nicht auf die Datenerfassung aus. Das Ausblenden hat keine funktionalen Auswirkungen, sondern reduziert nur das visuelle Rauschen beim Durchsuchen des Schemas in der AEP-Benutzeroberfläche. Diese Felder beziehen sich nur auf die Felder in der `MediaAnalytics Interaction Details` Feldergruppe.

   +++ Erweitern Sie , um Anweisungen zu Feldern anzuzeigen, die Sie ausblenden können.

   1. Wählen Sie **[!UICONTROL Bereich]** Struktur“ das Feld `Media Collection Details` und dann **[!UICONTROL Verwandte Felder verwalten]** aus.

      ![Verwalten von zugehörigen Feldern](assets/manage-related-fields.png)

   1. Aktivieren Sie die Option **[!UICONTROL Anzeigenamen für Felder anzeigen]** und aktualisieren Sie dann das Schema wie folgt:

      * Blenden Sie im Feld `Media Collection Details` > `Advertising Details` die folgenden Berichtsfelder aus: `Ad Completed`, `Ad Started` und `Ad Time Played`.

      * Blenden Sie im Feld `Media Collection Details` > `Advertising Pod Details` das folgende Berichtsfeld aus: `Ad Break ID`

      * Blenden Sie im Feld `Media Collection Details` > `Chapter Details` die folgenden Berichtsfelder aus: `Chapter Completed`, `Chapter ID`, `Chapter Started` und `Chapter Time Played`.

      * Blenden Sie im Feld `Media Collection Details` das Feld `List Of States` aus.

        ![Status der Mediensammlung ausblenden](assets/schema-hide-media-collection-states.png)

      * Blenden Sie im Feld `Media Collection Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set` und `Player State Time`.

        ![Felder zum Ausblenden](assets/schema-hide-listofstates.png)

      * Blenden Sie im Feld `Media Collection Details` > `Qoe Data Details` die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`,, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` und `Total Stalling Duration`.

      * Blenden Sie im Feld `Media Collection Details` > `Session Details` die folgenden Berichtsfelder aus: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Chapter Count`, `Content Time Spent`, `Media Segment Views`, `Media Session ID`, `Media Starts`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr` `Total Pause Duration` `Unique Time Played` `Video Segment`, `Content Starts`, und .

   1. Wählen **[!UICONTROL Bestätigen]**, um Ihre Änderungen zu speichern.

   1. Aktivieren Sie im Bereich **[!UICONTROL Struktur]** die Option **[!UICONTROL Anzeigenamen für Felder anzeigen]** und wählen Sie dann das `List Of Media Collection Downloaded Content Events` aus.

   1. Wählen Sie **[!UICONTROL Verknüpfte Felder verwalten]** und aktualisieren Sie das Schema wie folgt:

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` die folgenden Berichtsfelder aus: `Ad Completed`, `Ad Started` und `Ad Time Played`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` das folgende Berichtsfeld aus: `Ad Break ID`

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` die folgenden Berichtsfelder aus: `Chapter Completed`, `Chapter ID`, `Chapter Started` und `Chapter Time Played`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` das Feld `List Of States` aus.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set` und `Player State Time`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`,, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` und `Total Stalling Duration`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` die folgenden Berichtsfelder aus: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Time Spent`, `Estimated Streams`, `Media Downloaded Flag`, `Chapter Count`, `Content Starts`, `Media Session ID`, `Federated Data`, `Media Segment Views`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Content Completes`, `Pause Events`, `Pause Impacted Streams` `Pccr` `Pev3` `Total Pause Duration` `Unique Time Played` `Video Segment`, und .

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` das Feld `Media Session ID` aus.

   1. Wählen **[!UICONTROL Bestätigen]**, um Ihre Änderungen zu speichern.

   1. Wählen Sie **[!UICONTROL Bereich]** Struktur“ das Feld `Media Reporting Details` und dann **[!UICONTROL Verwandte Felder verwalten]** aus.

   1. Aktivieren Sie die Option **[!UICONTROL Anzeigenamen für Felder anzeigen]** und aktualisieren Sie dann das Schema wie folgt:

      * Blenden Sie im Feld `Media Reporting Details` die folgenden Felder aus: `Error Details`, `List Of States End`, `List of States Start` und `Media Session ID`.

   1. Wählen **[!UICONTROL Bestätigen]** > **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern.

   +++

1. (Optional) Sie können Ihrem Schema benutzerdefinierte Metadaten hinzufügen. Auf diese Weise können Sie zusätzliche, benutzerdefinierte Metadaten für bestimmte Anforderungen oder Kontexte einfügen. Weitere Informationen zu benutzerdefinierten Metadaten mit der Media Edge-API finden Sie unter [Unterstützung benutzerdefinierter Metadaten](custom-metadata.md).

   +++ Erweitern Sie , um Anweisungen zum Hinzufügen benutzerdefinierter Metadaten zu Ihrem Schema anzuzeigen.

   1. Suchen Sie den Mandantennamen der Organisation, indem Sie **[!UICONTROL Kontoinformationen]** > **[!UICONTROL Zugewiesene]** > [!UICONTROL _&#x200B;**Organisationsname**&#x200B;_] > **[!UICONTROL Mandant]**.

      Benutzerdefinierte Felder werden über diesen Pfad empfangen. (Beispiel: Mandantenname: _dcbl → myCustomField-Pfad: _dcbl.myCustomField.)

   1. Fügen Sie eine benutzerdefinierte Feldergruppe zu Ihrem definierten Medienschema hinzu.

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. Fügen Sie alle benutzerdefinierten Felder, die Sie verfolgen möchten, zur Feldergruppe hinzu.

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [Verwenden Sie den generierten &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties) für das benutzerdefinierte Feld in Ihrer Anfrage-Payload.

      ![add-custom-metadata](assets/custom-fields-path.png)

   +++

## Datensatz in Adobe Experience Platform erstellen

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Datensatzes, wie im [Handbuch zur Benutzeroberfläche von Datensätzen](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=de#create) beschrieben.

   Wählen Sie bei der Auswahl eines Schemas für Ihren Datensatz das zuvor erstellte Schema aus.

## Konfigurieren eines Datenstroms in Adobe Experience Platform

1. Erstellen Sie einen neuen Datenstrom, wie in [Konfigurieren eines Datenstroms](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de) beschrieben.

   Wählen Sie beim Erstellen des Datenstroms die folgenden Optionen aus:

   * Wählen Sie im Feld **[!UICONTROL Ereignisschema]** das Schema aus, das Sie in erstellt haben ([&#x200B; des Schemas in Adobe Experience Platform &#x200B;](#set-up-the-schema-in-adobe-experience-platform).

     >[!IMPORTANT]
     >
     >Wählen Sie **[!UICONTROL Speichern]** aus, wählen Sie nicht **[!UICONTROL Speichern und Zuordnung hinzufügen]**. Die Auswahl **[!UICONTROL Speichern und Zuordnung hinzufügen]** verursacht Zuordnungsfehler für das Zeitstempelfeld.

     ![Erstellen eines Datenstroms und Auswählen eines Schemas](assets/datastream-create-schema.png)

   * Fügen Sie die entsprechenden Services basierend auf Ihrer Adobe-Lösung zum Datenstrom hinzu. Informationen zum Hinzufügen eines Services finden Sie unter „Hinzufügen von Services zu einem Datenstrom“ in [Konfigurieren eines Datenstroms](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      * **[!UICONTROL Adobe Analytics]** (bei Verwendung von Adobe Analytics): Definieren Sie eine Report Suite wie in [Erstellen einer Report Suite](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite) beschrieben.

      * **[!UICONTROL Adobe Experience Platform]** (bei Verwendung von Customer Journey Analytics, Adobe Journey Optimizer oder Real-Time Customer Data Platform)

     ![Fügen Sie den Adobe Analytics-Service hinzu](assets/datastream-add-service.png)

   * Erweitern Sie **[!UICONTROL Erweiterte Optionen]** und aktivieren Sie dann die Option **[!UICONTROL Media Analytics]**.

     ![Media Analytics-Option](assets/datastream-media-check.png)

## Wählen Sie Ihre Implementierungsmethode

Wenn das Schema, der Datensatz und der Datenstrom eingerichtet sind, implementieren Sie eine der folgenden Code-Basen, um mit dem Senden von Streaming-Mediendaten an die Edge Network zu beginnen. Jede Seite behandelt die für Streaming-Medien spezifische Einrichtung. Der Code pro Ereignis und pro Variable wird in „Ereignisse[&#x200B; und „Variablen](/help/implementation/events/overview.md) [&#x200B; &#x200B;](/help/implementation/variables/overview.md).

**In-Code**-Implementierungen schreiben SDK-Aufrufe direkt in den Quellcode Ihrer Anwendung. **Verwenden von Tags** -Implementierungen verwenden [Adobe Experience Platform-Tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home) mit denen Sie Tracking-Regeln konfigurieren und bereitstellen können, ohne den Anwendungs-Code zu ändern. Wählen Sie den Ansatz aus, der zu Ihrem Bereitstellungs-Workflow passt.

| Codebase | In-Code | Verwenden von Tags |
|---|---|---|
| Web | [Web SDK](web-sdk.md) | [Web SDK-Tag-Erweiterung](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS (Tags)](ios-tags.md) |
| Android | [Android](android.md) | [Android (Tags)](android-tags.md) |
| Roku | [Roku Edge](roku.md) | — |
| API | [Media Edge-API](media-edge-api.md) | — |

## Nächster Schritt

Nachdem Sie mit der Datenerfassung begonnen haben, können Sie das Reporting konfigurieren:

* [Einrichten von Berichten für Edge-Implementierungen](/help/reporting/setup/edge-reporting.md) (Customer Journey Analytics)
* [Einrichten des Reportings für reine Analytics-Implementierungen](/help/reporting/setup/analytics-reporting.md) (wenn Ihr Datenstrom Adobe Analytics speist)

>[!MORELIKETHIS]
>
>* [Unterstützung benutzerdefinierter Metadaten](custom-metadata.md)
>* [XDM-Berichtsschema](reporting-schema.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

---
title: Implementieren von Adobe-Streaming-Mediendiensten mit Edge Network
description: Erfahren Sie, wie Adobe Streaming Media Services mit Experience Platform Edge implementiert werden können.
feature: Streaming Media
role: User, Admin, Developer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 9%

---

# Implementieren der Streaming-Mediensammlung mit der Edge Network

Mit Adobe Experience Platform Edge Network können Sie Daten, die für mehrere Produkte bestimmt sind, an einen zentralen Ort senden. Experience Edge leitet die entsprechenden Informationen an die gewünschten Produkte weiter. Mit diesem Konzept können Sie Implementierungsaufgaben zusammenfassen, insbesondere, wenn mehrere Datenlösungen vorhanden sind.

Die folgende Abbildung zeigt, wie das Add-on „Streaming Media Collection“ implementiert werden kann, um mithilfe von Experience Platform Edge Daten in Analysis Workspace verfügbar zu machen, entweder in Adobe Analytics oder Customer Journey Analytics:

![CJA-Workflow](assets/streaming-media-edge.png)

Einen Überblick über alle Implementierungsoptionen, einschließlich Implementierungsmethoden, die nicht Experience Platform Edge verwenden, finden Sie unter [Implementieren von Streaming-Mediendiensten für Adobe Analytics oder Customer Journey Analytics](/help/implementation/overview.md).

Unabhängig davon, ob Sie Adobe Experience Platform Web SDK, Adobe Experience Platform Mobile SDK, Adobe Experience Platform Roku SDK oder die API zum Implementieren der Streaming Media Collection mit Experience Edge verwenden, müssen Sie zunächst die folgenden Abschnitte ausfüllen:

## Einrichten des Schemas in Adobe Experience Platform

Um die Datenerfassung für die Verwendung in allen Anwendungen zu standardisieren, die Adobe Experience Platform nutzen, hat Adobe das offene und öffentlich dokumentierte Standard Experience-Datenmodell (XDM) erstellt.

So erstellen Sie ein Schema und richten es ein:

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Schemas, wie unter [Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=de) beschrieben.

1. Wählen Sie auf der Seite mit den Schemadetails beim Erstellen des Schemas [!UICONTROL **Erlebnisereignis**] aus, wenn Sie die Basisklasse für das Schema auswählen.

   ![Feldergruppen hinzugefügt](assets/schema-experience-event.png)

1. Klicken Sie auf [!UICONTROL **Weiter**].

1. Geben Sie einen Anzeigenamen und eine Beschreibung für das Schema an und wählen Sie dann [!UICONTROL **Beenden**].

1. Wählen Sie im Bereich [!UICONTROL **Komposition**] im Abschnitt [!UICONTROL **Feldergruppen**] die Option [!UICONTROL **Hinzufügen**] aus, suchen Sie dann nach den folgenden neuen Feldergruppen und fügen Sie sie dem Schema hinzu:
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nachdem Sie die Feldergruppen hinzugefügt haben, sollten sie wie folgt im Abschnitt [!UICONTROL **Feldergruppen**] angezeigt werden:

   ![Feldergruppen hinzugefügt](assets/schema-field-groups-added.png)

1. Klicken Sie [!UICONTROL **Speichern**], um Ihre Änderungen zu speichern.

1. (Optional) Sie können bestimmte Felder ausblenden, die nicht von der Media Edge-API verwendet werden. Das Ausblenden dieser Felder erleichtert das Lesen und Verstehen des Schemas, es ist jedoch nicht erforderlich. Diese Felder beziehen sich nur auf die Felder in der `MediaAnalytics Interaction Details` Feldergruppe.

   +++ Hier erweitern, um Anweisungen zu Feldern anzuzeigen, die Sie ausblenden können.

   1. Wählen Sie [!UICONTROL **Bereich**] Struktur“ das Feld `Media Collection Details` und dann [!UICONTROL **Verwandte Felder verwalten**] aus.

      ![Verwalten von zugehörigen Feldern](assets/manage-related-fields.png)

   1. Aktivieren Sie die Option [!UICONTROL **Anzeigenamen für Felder anzeigen**] und aktualisieren Sie dann das Schema wie folgt:

      * Blenden Sie im Feld `Media Collection Details` > `Advertising Details` die folgenden Berichtsfelder aus: `Ad Completed`, `Ad Started` und `Ad Time Played`.

      * Blenden Sie im Feld `Media Collection Details` > `Advertising Pod Details` das folgende Berichtsfeld aus: `Ad Break ID`

      * Blenden Sie im Feld `Media Collection Details` > `Chapter Details` die folgenden Berichtsfelder aus: `Chapter Completed`, `Chapter ID`, `Chapter Started` und `Chapter Time Played`.

      * Blenden Sie im Feld `Media Collection Details` das Feld `List Of States` aus.

        ![Status der Mediensammlung ausblenden](assets/schema-hide-media-collection-states.png)

      * Blenden Sie im Feld `Media Collection Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set` und `Player State Time`.

        ![Felder zum Ausblenden](assets/schema-hide-listofstates.png)

      * Blenden Sie im Feld `Media Collection Details` > `Qoe Data Details` die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`,, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` und `Total Stalling Duration`.

      * Blenden Sie im Feld `Media Collection Details` > `Session Details` die folgenden Berichtsfelder aus: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3` `Pccr` `Total Pause Duration` `Unique Time Played`, `Video Segment`, und .

   1. Wählen [!UICONTROL **Bestätigen**], um Ihre Änderungen zu speichern.

   1. Aktivieren Sie im Bereich [!UICONTROL **Struktur**] die Option [!UICONTROL **Anzeigenamen für Felder anzeigen**] und wählen Sie dann das `List Of Media Collection Downloaded Content Events` aus.

   1. Wählen Sie [!UICONTROL **Verknüpfte Felder verwalten**] und aktualisieren Sie das Schema wie folgt:


      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` die folgenden Berichtsfelder aus: `Ad Completed`, `Ad Started` und `Ad Time Played`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` das folgende Berichtsfeld aus: `Ad Break ID`

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` die folgenden Berichtsfelder aus: `Chapter Completed`, `Chapter ID`, `Chapter Started` und `Chapter Time Played`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` das Feld `List Of States` aus.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set` und `Player State Time`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`,, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` und `Total Stalling Duration`.

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` die folgenden Berichtsfelder aus: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams` `Pccr` `Pev3` `Total Pause Duration` `Unique Time Played` `Video Segment`, und .

      * Blenden Sie im Feld `List Of Media Collection Downloaded Content Events` > `Media Details` das Feld `Media Session ID` aus.

   1. Wählen [!UICONTROL **Bestätigen**], um Ihre Änderungen zu speichern.

   1. Wählen Sie [!UICONTROL **Bereich**] Struktur“ das Feld `Media Reporting Details` und dann [!UICONTROL **Verwandte Felder verwalten**] aus.

   1. Aktivieren Sie die Option [!UICONTROL **Anzeigenamen für Felder anzeigen**] und aktualisieren Sie dann das Schema wie folgt:

      * Blenden Sie im Feld `Media Reporting Details` die folgenden Felder aus: `Error Details`, `List Of States End`, `List of States Start` und `Media Session ID`.

   1. Wählen [!UICONTROL **Bestätigen**] > [!UICONTROL **Speichern**], um Ihre Änderungen zu speichern.

   +++

1. (Optional) Sie können Ihrem Schema benutzerdefinierte Metadaten hinzufügen. Auf diese Weise können Sie zusätzliche, benutzerdefinierte Metadaten einbeziehen, die für bestimmte Anforderungen oder Kontexte angepasst werden können. Diese Flexibilität ist in Szenarien nützlich, in denen vorhandene Schemata die gewünschten Datenpunkte nicht abdecken. (Sie können auch mit benutzerdefinierten Metadaten mit Media Edge-APIs arbeiten. Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Metadaten mit Media Edge-APIs](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/custom-metadata/).)

   +++ Erweitern Sie hier , um Anweisungen zum Hinzufügen benutzerdefinierter Metadaten zu Ihrem Schema anzuzeigen.

   1. Suchen Sie den Namen des Mandanten der Organisation, indem Sie [!UICONTROL **Kontoinformationen**] > [!UICONTROL **Zugewiesene**] > [!UICONTROL _**Organisationsname**_] > [!UICONTROL **Mandant**] auswählen.

      Diese benutzerdefinierten Felder werden über diesen Pfad empfangen. (Beispiel: Mandantenname: _dcbl → myCustomField-Pfad: _dcbl.myCustomField.)

   1. Fügen Sie eine benutzerdefinierte Feldergruppe zu Ihrem definierten Medienschema hinzu.

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. Fügen Sie alle benutzerdefinierten Felder, die Sie verfolgen möchten, zur Feldergruppe hinzu.

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [Verwenden Sie den generierten &#x200B;](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties) für das benutzerdefinierte Feld in Ihrer Anfrage-Payload.

      ![add-custom-metadata](assets/custom-fields-path.png)

   +++

1. Fahren Sie mit [Erstellen eines Datensatzes in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform) fort.

## Datensatz in Adobe Experience Platform erstellen

1. Stellen Sie sicher, dass Sie ein Schema wie in [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform) beschrieben einrichten.

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Datensatzes, wie im [Handbuch zur Benutzeroberfläche von Datensätzen](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=de#create) beschrieben.

   Wählen Sie bei der Auswahl eines Schemas für Ihren Datensatz das zuvor erstellte Schema aus, wie unter [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform) beschrieben.

1. Fahren Sie mit [Konfigurieren eines Datenstroms in Customer Journey Analytics &#x200B;](#configure-a-datastream-in-adobe-experience-platform).

## Konfigurieren eines Datenstroms in Adobe Experience Platform

1. Stellen Sie sicher, dass Sie einen Datensatz wie in [Erstellen eines Datensatzes in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform) beschrieben erstellt haben.

1. Erstellen Sie einen neuen Datenstrom, wie in [Konfigurieren eines Datenstroms](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de) beschrieben.

   Stellen Sie beim Erstellen des Datenstroms sicher, dass Sie die folgenden Konfigurationen auswählen:

   * Achten Sie im Feld [!UICONTROL **Ereignisschema**] beim Erstellen des Datenstroms darauf, dass Sie das Schema auswählen, das Sie in erstellt haben [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Wählen Sie [!UICONTROL **Speichern**] aus.

     >[!IMPORTANT]
     >
     >Wählen Sie nicht [!UICONTROL **Speichern und Zuordnung hinzufügen**] da dies zu Zuordnungsfehlern für das Zeitstempelfeld führt.

     ![Erstellen eines Datenstroms und Auswählen eines Schemas](assets/datastream-create-schema.png)

   * Fügen Sie dem Datenstrom einen der folgenden Services hinzu, je nachdem, ob Sie Adobe Analytics oder Customer Journey Analytics verwenden:

      * [!UICONTROL **Adobe Analytics**] (bei Verwendung von Adobe Analytics)

        Wenn Sie Adobe Analytics verwenden, stellen Sie sicher, dass Sie eine Report Suite definieren, wie in [Erstellen einer Report Suite](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite) beschrieben.

      * [!UICONTROL **Adobe Experience Platform**] (bei Verwendung von Customer Journey Analytics)

     Informationen zum Hinzufügen eines Services zu einem Datenstrom finden Sie im Abschnitt „Hinzufügen von Services zu einem Datenstrom“ in [Konfigurieren eines &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de#view-details)&quot;.

     ![Fügen Sie den Adobe Analytics-Service hinzu](assets/datastream-add-service.png)

      * Erweitern Sie [!UICONTROL **Erweiterte Optionen**] und aktivieren Sie dann die Option [!UICONTROL **Media Analytics**].

     ![Media Analytics-Option](assets/datastream-media-check.png)

1. Sie können jetzt die [Media Edge-API](/help/implementation/edge/implementation-edge-api.md) oder [Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md) implementieren, um mit der Erfassung von Medienanalysedaten zu beginnen.

   Nachdem Sie einige Daten erfasst haben, können Sie [Verbindung in Customer Journey Analytics erstellen](#create-a-connection-in-customer-journey-analytics).

## Erstellen einer Verbindung in Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.

1. Stellen Sie sicher, dass Sie einen Datenstrom erstellt haben, wie in [Konfigurieren eines Datenstroms in Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform) beschrieben.

1. Erstellen Sie in Customer Journey Analytics eine Verbindung, wie in [Verbindung erstellen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=de) beschrieben.

   Beim Erstellen der Verbindung sind die folgenden Konfigurationsoptionen erforderlich, um die Streaming Media-Sammlung zu implementieren:

   1. Wählen Sie den zuvor erstellten Datensatz aus, wie unter [Erstellen eines Datensatzes in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform) beschrieben.

   1. Stellen Sie sicher [!UICONTROL **dass die Einstellung „Alle neuen**] importieren“ aktiviert ist.

1. Fahren Sie mit [Datenansicht in Customer Journey Analytics erstellen“ &#x200B;](#create-a-new-data-view-in-customer-journey-analytics).

## Erstellen einer Datenansicht in Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.

1. Stellen Sie sicher, dass Sie eine Verbindung in Customer Journey Analytics erstellt haben, wie in [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics) beschrieben.

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie unter [Erstellen oder Bearbeiten einer Datenansicht](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de) beschrieben.

   Beim Erstellen der Datenansicht sind die folgenden Konfigurationsoptionen für die Implementierung der Streaming Media Collection erforderlich:

   1. Wählen [!UICONTROL **im Feld**] die zuvor erstellte Verbindung aus, wie unter [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics) beschrieben.

      Es kann bis zu 15 Minuten dauern, bis die von Ihnen erstellte Verbindung zur Auswahl verfügbar ist.

   1. Suchen Sie auf der [!UICONTROL **Komponenten**] im Abschnitt [!UICONTROL **Schemafelder**] nach jeder Komponente, die in den Tabellen unten aufgeführt ist, und ziehen Sie sie in das Bedienfeld [!UICONTROL **Metriken**]. Wenn mehrere Felder mit demselben Namen vorhanden sind, verwenden Sie den XDM-Pfad, um sicherzustellen, dass es sich um das richtige Feld handelt.

      **Hauptinhalt - Inhaltsmetriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Medienstarts | mediaReporting.sessionDetails.isViewed |
      | Mediensegmentansichten | mediaReporting.sessionDetails.hasSegmentView |
      | Inhaltsstarts | mediaReporting.sessionDetails.isPlayed |
      | Inhalt abgeschlossen | mediaReporting.sessionDetails.isCompleted |
      | Inhaltsbesuchszeit | mediaReporting.sessionDetails.timePlayed |
      | Besuchszeit für Medien | mediaReporting.sessionDetails.totalTimePlayed |
      | Eindeutige Spielzeit | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10% Fortschrittsmarkierung | mediaReporting.sessionDetails.hasProgress10 |
      | Zielgruppendurchschnitt pro Minute | mediaReporting.sessionDetails.averageMinuteAudience |


      **Kapitel und Anzeigen - Kapitel und Anzeigenmetriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Kapitel gestartet | mediaReporting.chapterDetails.isStarted |
      | Kapitel abgeschlossen | mediaReporting.chapterDetails.isCompleted |
      | Kapitelzeit | mediaReporting.chapterDetails.timePlayed |
      | Anzeige gestartet | mediaReporting.advertisingDetails.isStarted |
      | Anzeige abgeschlossen | mediaReporting.advertisingDetails.isCompleted |
      | Anzeigenspielzeit | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE-Metriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Zeit bis Start | mediaReporting.qoeDataDetails.timeToStart |
      | Drops vor dem Start | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Von Puffer betroffene Streams | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Von Bitratenänderung betroffene Streams | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Bitratenänderungen | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Durchschnittliche Bitrate | mediaReporting.qoeDataDetails.bitrateAverage |
      | Gelöschte Frames | mediaReporting.qoeDataDetails.droppedFrames |
      | Fehler | mediaReporting.qoeDataDetails.errorCount |
      | Von Fehlern betroffene Streams | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Von Dropped Frames betroffene Streams | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **Player-Status - Player-Statusmetriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Player-Status festgelegt | mediaReporting.states.isSet |
      | Anzahl der Player-Status | mediaReporting.states.count |
      | Player-Statuszeit | mediaReporting.states.time |


   1. Aktualisieren Sie die Beschriftungen (im [!UICONTROL **Kontextbeschriftungen**] Dropdown-Menü) für die Komponenten in der folgenden Tabelle. Suchen Sie nach Komponenten, die sich noch nicht im Bedienfeld Metriken befinden, und ziehen Sie sie in das Bedienfeld.

      | Name der Komponente | Kontext-Label |
      |---------|----------|
      | Zeitüberschreitung des Mediensitzungs-Servers | Medien: Sekunden seit letztem Aufruf |
      | Besuchszeit für Medien | Medien: Besuchszeit für Medien |
      | Gesamtpufferdauer | Medien: Gesamtdauer des Puffers |
      | Zeit bis Start | Medien: Zeit bis zum Start |
      | Pausierung – Gesamtdauer | Medien: Pausierung - Gesamtdauer |

   1. Um Ihrem Customer Journey Analytics-Projekt Aufschlüsselungen hinzuzufügen, fügen Sie die folgenden Dimensionen zum Bedienfeld [!UICONTROL **Dimensionen**] hinzu:

      | XDM-Pfad | Name der Komponente |
      |---------|----------|
      | mediaReporting.states.name | Player-Statusname |
      | mediaReporting.sessionDetails.ID | Mediensitzungs-ID |

      Zusätzlich zu den Dimensionen in dieser Tabelle können Sie beliebige andere Dimensionen hinzufügen, die Sie für die Filterung von Daten nach in Customer Journey Analytics-Projekten verfügbar machen möchten.

1. Wählen Sie [!UICONTROL **Speichern und fortfahren**] > [!UICONTROL **Speichern und beenden**] um Ihre Änderungen zu speichern.

1. Fahren Sie mit [Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics &#x200B;](#create-and-configure-a-project-in-customer-journey-analytics).

## Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics

1. Stellen Sie sicher, dass Sie eine Datenansicht in Customer Journey Analytics erstellt haben, wie in [Erstellen einer Datenansicht in Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics) beschrieben.

1. Wählen Sie in Customer Journey Analytics auf der Registerkarte [!UICONTROL **Workspace**] im Bereich [!UICONTROL **Projekte**] die Option [!UICONTROL **Projekt erstellen**].

1. Wählen Sie [!UICONTROL **Leeres Projekt**] > [!UICONTROL **Erstellen**] aus.

1. Wählen Sie im neuen Projekt die Datenansicht aus, die Sie zuvor erstellt haben.

   Beim Erstellen von Bedienfeldern in Ihrem Projekt können Sie alle Komponenten verwenden, die Sie Ihrer Datenansicht hinzugefügt haben, wie in [Erstellen einer Datenansicht in Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics) beschrieben.

   Die folgenden vier Bedienfelder sind Beispiele für Bedienfelder, die Sie erstellen können:

   ![Hauptinhaltsbedienfeld](assets/main-content-panel.png)

   ![Kapitel- und Anzeigen-Bedienfeld](assets/chapter-and-ads-panel.png)

   ![QoE-Bedienfeld](assets/qoe-panel.png)

   ![Player-State-Panel](assets/player-state-panel.png)

1. Wählen Sie das Symbol **Bedienfelder** in der linken Leiste aus und ziehen Sie dann das Bedienfeld [!UICONTROL **Gleichzeitige Medienbetrachter**] und das Bedienfeld [!UICONTROL **Bei Medienwiedergabe verbrachte Zeit**].

   Die beiden Bedienfelder sollten wie folgt aussehen:

   ![Bedienfeld „Gleichzeitige Medienbetrachter“](assets/media-concurrent-viewers-panels.png)

   ![Panel „Verbrachte Zeit bei der Medienwiedergabe“](assets/media-playback-time-spent-panels.png)

1. (Bedingt) Wenn Sie benutzerdefinierte Metadaten zu Ihrem Schema hinzugefügt haben, wie in Schritt 8 von [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform) beschrieben, müssen Sie die Persistenz für die benutzerdefinierten Felder festlegen, wie in [Persistenzkomponenteneinstellungen](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) im Customer Journey Analytics-Handbuch beschrieben.

   Wenn Daten in Customer Journey Analytics eingehen, ist die Dimension Benutzerspezifische Benutzer-ID verfügbar.

   ![setup-custom-metadata](assets/custom-metadata-dimension.png)

   >[!NOTE]
   >
   >Wenn Sie Adobe Analytics als Upstream für Ihren Datenstrom einrichten, sind die benutzerdefinierten Metadaten auch in ContextData mit dem Namen vorhanden, den Sie im Schema festgelegt haben (ohne das Mandantenpräfix, z. B. myCustomField). Dadurch können alle für ContextData verfügbaren Adobe Analytics-Funktionen verwendet werden, z. B[&#x200B; „Erstellen einer Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules).

1. Geben Sie das Projekt frei, wie unter [Freigeben von Projekten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=de) beschrieben.

   >[!NOTE]
   >
   >   Wenn die Benutzenden, für die Sie freigeben möchten, nicht verfügbar sind, stellen Sie sicher, dass die Benutzenden in der Adobe Admin Console Benutzer- und Administratorzugriff auf Customer Journey Analytics haben.


1. Fahren Sie fort mit [Daten an Experience Platform Edge senden](#send-data-to-experience-platform-edge).

## Senden von Daten an Experience Platform Edge

Je nach Datentyp, den Sie an Experience Platform Edge senden möchten, können Sie eine der folgenden Methoden verwenden:

### Web: Verwenden der Adobe Experience Platform Web SDK

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Senden von Web-Daten an Edge mit Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)

* [Migrieren zu Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobile: Verwenden der Adobe Experience Platform Mobile SDK

Verwenden Sie die folgenden Dokumentationsressourcen, um die Implementierung für iOS und Android abzuschließen:

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API-Referenz](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrieren zu Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku: Adobe Experience Platform Roku SDK

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main)

* [Migrieren zu Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API: Web und andere

Die -API ist derzeit die einzige unterstützte Möglichkeit, Web-Daten an Experience Platform Edge zu senden.

Die API ist auch verfügbar, wenn Sie eine benutzerdefinierte Implementierung der Edge-APIs verwenden möchten.

Weitere Informationen zur Media Edge-API finden Sie in den folgenden Ressourcen:

* [Übersicht über die Media Edge-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Erste Schritte mit der Media Edge-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Handbuch zur Fehlerbehebung bei der Media Edge-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Verwenden der Open API-Spezifikationsdatei für Media Edge-APIs](https://developer.adobe.com/data-collection-apis/docs/api/media-edge/)

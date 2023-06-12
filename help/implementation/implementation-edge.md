---
title: Erste Schritte beim Einrichten einer Implementierung für Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Adobe Streaming Media implementieren.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 29d58b41-9a49-4b71-bdc5-4e2848cd3236
source-git-commit: bcab6a94547b79a565dc2303ab640dc1b8994bd4
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 11%

---

# Installieren von Media Analytics mit Experience Platform Edge

Mit Adobe Experience Platform Edge können Sie Daten, die für mehrere Produkte bestimmt sind, an einen zentralen Ort senden. Experience Edge leitet die entsprechenden Informationen an die gewünschten Produkte weiter. Mit diesem Konzept können Sie Implementierungsaufgaben zusammenfassen, insbesondere, wenn mehrere Datenlösungen vorhanden sind.

Die folgende Abbildung zeigt eine Media Analytics-Implementierung, die Experience Platform Edge verwendet:

![Edge-Implementierung](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>Derzeit können Sie Daten nur mit dem Adobe Experience Platform Mobile SDK an Experience Edge senden.


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

Führen Sie die folgenden Abschnitte aus, um Media Analytics mit Experience Platform Edge zu implementieren:

* [Report Suite definieren](#define-a-report-suite)
* [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform)
* [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform)
* [Konfigurieren eines Datenspeichers in Adobe Experience Platform](#configure-a-datastream-in-adobe-experience-platform)
* [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics)
* [Datenansicht in Customer Journey Analytics erstellen](#create-a-data-view-in-customer-journey-analytics)
* [Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics)
* [Senden von Daten an Experience Platform Edge mit der Edge-Erweiterung](#send-data-to-experience-platform-edge-with-the-edge-extension)

## Report Suite definieren

>[!NOTE]
>
>Eine Report Suite ist nur erforderlich, wenn Sie Adobe Analytics verwenden. Eine Report Suite ist nicht erforderlich, wenn Sie Customer Journey Analytics für die Berichterstellung verwenden möchten.

Wenn Sie planen, Adobe Analytics für die Berichterstellung zu verwenden, benötigen Sie eine Report Suite zur Verwendung mit Ihrer Streaming-Medien-Implementierung. Informationen zum Definieren einer Report Suite finden Sie unter [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

Nachdem eine Report Suite definiert wurde, fahren Sie mit [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

## Einrichten des Schemas in Adobe Experience Platform

Um die Datenerfassung für die Verwendung in allen Anwendungen zu standardisieren, die Adobe Experience Platform nutzen, hat Adobe das offene und öffentlich dokumentierte Standard Experience-Datenmodell (XDM) erstellt.

So erstellen und richten Sie ein Schema ein:

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Schemas, wie unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   Wählen Sie beim Erstellen des Schemas [!UICONTROL **XDM ExperienceEvent**] von [!UICONTROL **Schema erstellen**] Dropdown-Menü.

1. Im [!UICONTROL **Komposition**] im [!UICONTROL **Feldergruppen**] Bereich, wählen Sie [!UICONTROL **Hinzufügen**], suchen Sie dann nach den folgenden neuen Feldergruppen und fügen Sie sie zum Schema hinzu:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nachdem Sie die Feldergruppen hinzugefügt haben, sollten sie im [!UICONTROL **Feldergruppen**] wie folgt:

   ![Feldergruppen hinzugefügt](assets/schema-field-groups-added.png)

1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `endUserIds` > `_experience` Feldergruppe und wählen Sie [!UICONTROL **Zugehörige Felder verwalten**].

   ![Schaltfläche &quot;Zugeordnete Felder verwalten&quot;](assets/manage-related-fields.png)

1. Aktualisieren Sie das Schema wie folgt:

   * Im `Adobe Analytics ExperienceEvent Template` Feldergruppe, alle Felder außer `EndUserIDs`.

   * Im `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` Feldergruppe, alle Felder mit Ausnahme der `Identifier` -Feld.

   * Im `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` Feldergruppe, alle Felder mit Ausnahme der `Identifier` -Feld.

     ![Ausblenden von Feldern](assets/schema-hide-fields.png)

1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `Implementation Details` Feldergruppe, wählen Sie [!UICONTROL **Zugehörige Felder verwalten**] und aktualisieren Sie dann das Schema wie folgt:

   * Im `Implementation Details` > `Implementation details` Feldergruppe, alle Felder außer `version`.

     ![Ausblenden von Feldern](assets/schema-hide-fields2.png)

1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `Media Collection Details` Feldergruppe, wählen Sie [!UICONTROL **Zugehörige Felder verwalten**] und aktualisieren Sie dann das Schema wie folgt:

   * Im `Media Collection Details` Feldergruppe, die `List Of States` Feldergruppe.

     ![Anzeigen von Mediensammlungsstatus](assets/schema-hide-media-collection-states.png)

   * Im `Media Collection Details` > `Advertising Details` -Feldergruppe die folgenden Berichtsfelder ausblenden: `Ad Completed`, `Ad Started`und `Ad Time Played`.

   * Im `Media Collection Details` > `Advertising Pod Details` Feldergruppe, blenden Sie das folgende Berichtsfeld aus: `Ad Break ID`

   * Im `Media Collection Details` > `Chapter Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Chapter ID`, `Chapter Completed`, `Chapter Started`und `Chapter Time Played`.

   * Im `Media Collection Details` > `Qoe Data Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`und `Total Stalling Duration`.

   * Im `Media Collection Details` > `Session Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`und `Pccr`.

   * Im `Media Collection Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` Feldergruppen, blenden Sie die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set`und `Player State Time`.

     ![Ausblenden von Feldern](assets/schema-hide-listofstates.png)

1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `List Of Media Collection Downloaded Content Events` Feldergruppe, wählen Sie [!UICONTROL **Zugehörige Felder verwalten**] und aktualisieren Sie dann das Schema wie folgt:

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` Feldergruppe, die `List Of States` Feldergruppe.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` -Feldergruppe die folgenden Berichtsfelder ausblenden: `Ad Completed`, `Ad Started`und `Ad Time Played`.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` Feldergruppe, blenden Sie das folgende Berichtsfeld aus: `Ad Break ID`

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Chapter ID`, `Chapter Completed`, `Chapter Started`und `Chapter Time Played`.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`und `Total Stalling Duration`.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` Feldergruppe, blenden Sie die folgenden Berichtsfelder aus: `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`und `Pccr`.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` Feldergruppen, blenden Sie die folgenden Berichtsfelder aus: `Player State Count`, `Player State Set`und `Player State Time`.

   * Im `List Of Media Collection Downloaded Content Events` > `Media Details`  Feldergruppe, die `Media Session ID` -Feld.

1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `Media Reporting Details` Feldergruppe, wählen Sie [!UICONTROL **Zugehörige Felder verwalten**] und aktualisieren Sie dann das Schema wie folgt:

   * Im `Media Reporting Details` Feldergruppe, blenden Sie die folgenden Feldergruppen aus: `Error Details`, `List Of States End`, `List of States Start`, `Playhead`und `Media Session ID`.

1. Auswählen [!UICONTROL **Bestätigen**] > [!UICONTROL **Speichern**]  , um Ihre Änderungen zu speichern.

1. Fahren Sie mit [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

## Datensatz in Adobe Experience Platform erstellen

1. Stellen Sie sicher, dass Sie ein Schema wie in [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Datensatzes, wie unter [Handbuch zur Benutzeroberfläche von Datensätzen](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=de#create).

   Wählen Sie bei der Auswahl eines Schemas für Ihren Datensatz das zuvor von Ihnen erstellte Schema aus, wie unter [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Fahren Sie mit [Konfigurieren eines Datenspeichers in Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Konfigurieren eines Datenspeichers in Adobe Experience Platform

1. Stellen Sie sicher, dass Sie einen Datensatz erstellt haben, wie unter [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

1. Erstellen Sie einen neuen Datastream wie in [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de).

   Stellen Sie beim Erstellen des Datastreams sicher, dass Sie die folgenden Konfigurationsoptionen auswählen:

   * Im [!UICONTROL **Ereignisschema**] beim Erstellen des Datastreams das Schema auswählen, das Sie in [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Wählen Sie [!UICONTROL **Speichern**] aus.

     >[!IMPORTANT]
     >
         > Nicht auswählen [!UICONTROL **Zuordnung speichern und hinzufügen**] weil dies zu Zuordnungsfehlern für das Feld &quot;Zeitstempel&quot;führt.
     
     ![Erstellen Sie einen Datenspeicher und wählen Sie ein Schema aus.](assets/datastream-create-schema.png)

   * Fügen Sie je nachdem, ob Sie Adobe Analytics oder Customer Journey Analytics verwenden, einen der folgenden Dienste zum Datastream hinzu:

      * [!UICONTROL **Adobe Analytics**] (bei Verwendung von Adobe Analytics)

        Wenn Sie Adobe Analytics verwenden, stellen Sie sicher, dass Sie eine Report Suite wie im Abschnitt beschrieben definieren [Report Suite definieren](#define-a-report-suite) in diesem Artikel.

      * [!UICONTROL **Adobe Experience Platform**] (bei Verwendung von Customer Journey Analytics)

     Informationen zum Hinzufügen eines Dienstes zu einem Datastream finden Sie im Abschnitt &quot;Dienste zu einem Datastream hinzufügen&quot;unter [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Hinzufügen des Adobe Analytics-Dienstes](assets/datastream-add-service.png)

   * Erweitern [!UICONTROL **Erweiterte Optionen**], und aktivieren Sie dann die [!UICONTROL **Media Analytics**] -Option.

     ![Media Analytics-Option](assets/datastream-media-check.png)

1. Fahren Sie mit [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Erstellen einer Verbindung in Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.


1. Stellen Sie sicher, dass Sie einen Datastream erstellt haben, wie in [Konfigurieren eines Datenspeichers in Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. Erstellen Sie in Customer Journey Analytics eine Verbindung, wie unter [Verbindung erstellen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=de).

   Beim Erstellen der Verbindung sind für die Implementierung von Streaming-Medien die folgenden Konfigurationsoptionen erforderlich:

   1. Wählen Sie den zuvor erstellten Datensatz aus, wie unter [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

   1. Stellen Sie sicher, dass [!UICONTROL **Alle neuen Daten importieren**] -Einstellung aktiviert ist.

1. Fahren Sie mit [Datenansicht in Customer Journey Analytics erstellen](#create-a-new-data-view-in-customer-journey-analytics).

## Datenansicht in Customer Journey Analytics erstellen

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.

1. Stellen Sie sicher, dass Sie eine Verbindung in Customer Journey Analytics wie in [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie unter [Datenansicht erstellen oder bearbeiten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de).

   Beim Erstellen der Datenansicht sind für die Implementierung von Streaming-Medien die folgenden Konfigurationsoptionen erforderlich:

   1. Im [!UICONTROL **Verbindung**] -Feld die zuvor von Ihnen erstellte Verbindung aus, wie in [Erstellen einer Verbindung in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

      Es kann bis zu 15 Minuten dauern, bis die von Ihnen erstellte Verbindung ausgewählt werden kann.

   1. Im [!UICONTROL **Komponenten**] im [!UICONTROL **Schemafelder**] nach jeder Komponente suchen, die in den Tabellen unten aufgeführt ist, und ziehen Sie sie in die [!UICONTROL **Metriken**] Bereich. Wenn mehrere Felder mit demselben Namen vorhanden sind, verwenden Sie den XDM-Pfad, um sicherzustellen, dass es sich um das richtige Feld handelt.

      **Hauptinhalt - Inhaltsmetriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Medienstarts | mediaReporting.sessionDetails.isViewed |
      | Mediensegmentansichten | mediaReporting.sessionDetails.hasSegmentView |
      | Inhaltsstarts | mediaReporting.sessionDetails.isPlayed |
      | Inhaltsbeendigungen | mediaReporting.sessionDetails.isCompleted |
      | Inhaltsbesuchszeit | mediaReporting.sessionDetails.timePlayed |
      | Besuchszeit für Medien | mediaReporting.sessionDetails.totalTimePlayed |
      | Eindeutige Spielzeit | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10 % Fortschrittsmarkierung | mediaReporting.sessionDetails.hasProgress10 |
      | Zielgruppendurchschnitt pro Minute | mediaReporting.sessionDetails.averageMinuteAudience |


      **Kapitel und Anzeigen - Metriken für Kapitel und Anzeigen**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Kapitel gestartet | mediaReporting.chapterDetails.isStarted |
      | Kapitel abgeschlossen | mediaReporting.chapterDetails.isCompleted |
      | Wiedergabe des Kapitels | mediaReporting.chapterDetails.timePlayed |
      | Anzeigenstarts | mediaReporting.advertisingDetails.isStarted |
      | Anzeige abgeschlossen | mediaReporting.advertisingDetails.isCompleted |
      | Wiedergabezeit der Anzeige | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE-Metriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Zeit bis Start | mediaReporting.qoeDataDetails.timeToStart |
      | Drops vor Start | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
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
      | Player-Statusset | mediaReporting.states.isSet |
      | Player-Statusanzahl | mediaReporting.states.count |
      | Player-Statuszeit | mediaReporting.states.time |


   1. Aktualisieren Sie die Beschriftungen (im [!UICONTROL **Kontextbezeichnungen**] Dropdown-Menü) für die Komponenten in der folgenden Tabelle. Suchen Sie nach Komponenten, die sich noch nicht im Metrikbereich befinden, und ziehen Sie sie in den Bereich.

      | Name der Komponente | Kontextkennzeichnung |
      |---------|----------|
      | Zeitüberschreitung des Mediensitzungs-Servers | Medien: Sekunden seit dem letzten Aufruf |
      | Besuchszeit für Medien | Medien: Besuchszeit für Medien |
      | Gesamtpufferdauer | Medien: Gesamtpufferdauer |
      | Zeit bis Start | Medien: Zeit bis Start |
      | Pausierung – Gesamtdauer | Medien: Pausierung - Gesamtdauer |

   1. Um Ihrem Customer Journey Analytics-Projekt Aufschlüsselungen hinzuzufügen, fügen Sie die folgenden Dimensionen zum [!UICONTROL **Dimensionen**] Bereich:

      | XDM-Pfad | Name der Komponente |
      |---------|----------|
      | mediaReporting.states.name | Player-Statusname |
      | mediaReporting.sessionDetails.ID | Mediensitzungs-ID |

      Zusätzlich zu den Dimensionen in dieser Tabelle können Sie beliebige weitere Dimensionen hinzufügen, die Sie zum Filtern von Daten in Customer Journey Analytics-Projekten bereitstellen möchten.

1. Auswählen [!UICONTROL **Speichern und fortfahren**] > [!UICONTROL **Speichern und beenden**] , um Ihre Änderungen zu speichern.

1. Fahren Sie mit [Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics

1. Stellen Sie sicher, dass Sie eine Datenansicht in Customer Journey Analytics erstellt haben, wie in [Datenansicht in Customer Journey Analytics erstellen](#create-a-new-data-view-in-customer-journey-analytics).

1. In Customer Journey Analytics wird im [!UICONTROL **Arbeitsbereich**] im [!UICONTROL **Projekte**] Bereich, auswählen [!UICONTROL **Projekt erstellen**].

1. Auswählen [!UICONTROL **Leeres Projekt**] > [!UICONTROL **Erstellen**].

1. Wählen Sie im neuen Projekt die zuvor erstellte Datenansicht aus.

   Beim Erstellen von Bedienfeldern in Ihrem Projekt können Sie alle Komponenten verwenden, die Sie Ihrer Datenansicht hinzugefügt haben, wie unter [Datenansicht in Customer Journey Analytics erstellen](#create-a-new-data-view-in-customer-journey-analytics).

   Die folgenden vier Bedienfelder sind Beispiele für Bedienfelder, die Sie erstellen können:

   ![Hauptinhaltsbereich](assets/main-content-panel.png)

   ![Bedienfeld &quot;Kapitel und Anzeigen&quot;](assets/chapter-and-ads-panel.png)

   ![QoE-Bedienfeld](assets/qoe-panel.png)

   ![Platzierungsstatusbereich](assets/player-state-panel.png)

1. Wählen Sie die **Bedienfelder** Symbol in der linken Leiste und ziehen Sie dann in die [!UICONTROL **Gleichzeitige Medienbetrachter**] und [!UICONTROL **Medienwiedergabedauer**] Bereich.

   Die beiden Bedienfelder sollten wie folgt aussehen:

   ![Bedienfeld &quot;Gleichzeitige Medienbetrachter&quot;](assets/media-concurrent-viewers-panels.png)

   ![Zeitfenster für die Medienwiedergabe](assets/media-playback-time-spent-panels.png)

1. Geben Sie das Projekt wie unter [Freigeben von Projekten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=de).

   >[!NOTE]
   >
   >   Wenn die Benutzer, für die Sie freigeben möchten, nicht verfügbar sind, stellen Sie sicher, dass die Benutzer über Benutzer- und Administratorzugriff auf Customer Journey Analytics in der Adobe Admin Console verfügen.

1. Fahren Sie mit [Daten an Experience Platform Edge senden](#send-data-to-experience-platform-edge).

## Senden von Daten an Experience Platform Edge mit dem AEP Mobile SDK

Sie können das mobile Adobe Experience Platform SDK verwenden, um mobile Daten an Experience Platform Edge zu senden. (Alternativ können Sie eine benutzerdefinierte Implementierung der Edge-APIs verwenden.<!-- Waiting for link from John -->)

Verwenden Sie die folgenden Dokumentationsressourcen, um die Implementierung für iOS und Android abzuschließen:

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API-Referenz](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migration zu Adobe Streaming Media für Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)


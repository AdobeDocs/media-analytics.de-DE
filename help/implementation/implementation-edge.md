---
title: Erste Schritte beim Einrichten einer Implementierung für Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Adobe Streaming Media implementieren.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a5d458f6c2826941cb01d1cbd5850851c769a2ab
workflow-type: tm+mt
source-wordcount: '1960'
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

Sie können das mobile Adobe Experience Platform SDK verwenden, um mobile Daten an Experience Platform Edge zu senden. (Alternativ können Sie eine benutzerdefinierte Implementierung der Edge-APIs verwenden.<!-- I guess we don't need/want to document this? -->)

Verwenden Sie die folgenden Dokumentationsressourcen, um die Implementierung abzuschließen:


| Mobilbetriebssystem | Ressourcen  |
|---------|----------|
| **iOS** | Die folgenden Ressourcen stehen zum Senden von iOS-Mobildaten zur Verfügung: <ul><li>[Mobile SDK mithilfe der Datenerfassungs-Benutzeroberfläche konfigurieren](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/getting-started.md)</li><li>[Migration vom Media SDK zum Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/migration-guide.md)</li><li>[Referenz zur Edge Media-API](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/api-reference.md)</li></ul> |
| **Android** | Die folgenden Ressourcen stehen zum Senden von Android-Mobildaten zur Verfügung: <ul><li>[Mobile SDK mithilfe der Datenerfassungs-Benutzeroberfläche konfigurieren](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/getting-started.md)</li><li>[Migration vom Media SDK zum Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/migration-guide.md)</li><li>[Referenz zur Edge Media-API](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/api-reference.md)</li></ul> |


<!--

+++Adobe Experience Platform Mobile SDK

If you plan to use the Mobile SDK extension in Adobe Experience Platform Data Collection to send data to Edge, complete the following sections:

### Create a mobile property

Create a mobile property, as described in [Set up a mobile property](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/). 

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/mobile-sdk/overview.html?lang=en 

The Adobe Experience Platform Mobile SDK helps power Adobe's Experience Cloud solutions and services in your mobile apps. It is available for Android, iOS, and various cross-platform development frameworks. Configuration is handled through Adobe Experience Platform Data Collection.
>[!IMPORTANT]
>
>An Adobe Analytics extension is also available in Adobe Experience Platform Data Collection. If you install this extension, you do not take advantage of XDM or the Edge Network.

### Register the extensions and load your tag configuration

Use code in your app to register the necessary extensions and load your tag configuration. For more information, see [Set up the configuration](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Implement and test fuctionality

Implement and test app functionality using a combination of tags data elements, rules, additional extensions, and SDK API calls. Inspect, validate, and debug data collection and experiences for your mobile application.

For more information, see [Use the sample application](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Extend and validate your mobile app implementation

Before pushing the mobile app extension to your production environment, first validate that it works.

(What are the steps to do this?)

-->

<!--

+++Adobe Experience Platform Web SDK (Coming soon)

>[!NOTE]
>
>The Adobe Experience Platform Web SDK is not yet available. This page will be updated when it becomes available.

<!-- Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/web-sdk/overview.html?lang=en -->

<!-- Use the Web SDK extension in Adobe Experience Platform Data Collection to send data to Edge.

You can use the [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html) to send data to Adobe Analytics. This implementation method works by translating the [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) into a format used by Analytics.

You can send data to Experience Edge directly using the Web SDK, or through the Web SDK extension in Tags. -->

<!-- ### Web SDK

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK workflow](../../assets/websdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td> 4</td>
<td><b>Install the prebuilt standalone version</b>. You can reference the library (<code>alloy.js</code>) on the CDN directly on your page or download and host it on your own infrastructure. Alternatively, you can use the NPM package.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-2%3A-installing-the-prebuilt-standalone-version">Installing the prebuilt standalone version</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-3%3A-using-the-npm-package">Using the NPM package</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>6</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>7</td>
<td><b>Configure the Web SDK</b>. Ensure the library that you installed in step 4 is properly configured with the datastream ID (formerly known as edge configuration id (<code>edgeConfigId</code>)), organization id (<code>orgId</code>), and other available options.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en">Configure the Web SDK</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Execute commands</b> and/or <b>track events</b>. After the base code has been implemented on your webpage, you can begin executing commands and tracking events with the SDK.
</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/executing-commands.html?lang=en">Execute commands</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en">Track events</a></td>
</tr>

<tr>
<td>9</td><td><b>Extend and validate your implementation</b> before pushing it out to production.</td><td></td> 
</tr>
</table>


### Web SDK extension

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK extension workflow](../../assets/websdk-extension-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td>4</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<tr>
<td>5</td> 
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>6</td>
<td><b>Create a tag property</b>. Properties are overarching containers used to reference tag management data.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#for-web">Create or configure a tag property for web</a></td>
</tr>

<tr>
<td>7</td> 
<td><b>Install and configure the Web SDK extension</b> in your tag property. Configure the Web SDK extension to send data to the datastream configured in step 4.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html?lang=en">Adobe Experience Platform Web SDK extension overview</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Iterate, validate, and publish</b> to production. Add the tag property to your web site. Then use data elements, rules, and so on, to customize your implementation.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=en">Publishing overview</a></td>
</tr>

</table>


### Additional resources

Tags can be highly customized. Learn more about how you can get the most out of Adobe Analytics by including the right data in your implementation.

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#): Learn how the interface works and what extensions are available.

-   [Adobe Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/web-sdk.html?lang=en)


+++

-->


<!--

### Adobe Experience Platform SDK

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>4</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Create a mobile property</b>. A property is a container that you fill with extensions, rules, data elements, and libraries.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/">Set up a mobile property</a></tr>

<tr>
<td>6</td>
<td><b>Install the Adobe Experience Platform Edge Network extension</b> in the mobile tag property and configure the datastream in the extension.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/edge-network/">Adobe Experience Platform Edge Network</a>
</tr>

<tr>
<td>7</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>9</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>


### Adobe Analytics extension.

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-analytics-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Install the Adobe Analytics extension</b> in the mobile tag property and configure the extension to point to your report suite.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/adobe-analytics/">Adobe Analytics extension for mobile property</a>
</tr>

<tr>
<td>4</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>6</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>

### Additional resources

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#)

-   [Mobile SDK documentation](https://developer.adobe.com/client-sdks/documentation/)

-->

<!--

+++

+++Edge Network Server API

Send data directly to Edge using an API.

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/edge-api/overview.html?lang=en 

If you are unable to use the Adobe Experience Platform [Web SDK](../web-sdk/overview.md) or [Mobile SDK](../mobile-sdk/overview.md), you can send data to the Edge Network directly through an API.

See [Edge Network Server API documentation](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html), and an example [integrating with Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/interacting-other-adobe-solutions/interacting-adobe-analytics.html).

+++ 

-->


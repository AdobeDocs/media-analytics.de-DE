---
title: Implementieren des Add-ons für Streaming-Mediensammlung mit dem Edge Network
description: Erfahren Sie, wie das Streaming Media Collection Add-on mit Experience Platform Edge implementiert werden kann.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 9%

---

# Implementieren des Add-ons für Streaming-Mediensammlung mit dem Edge Network

Mit Adobe Experience Platform Edge Network können Sie Daten, die für mehrere Produkte bestimmt sind, an einen zentralen Ort senden. Experience Edge leitet die entsprechenden Informationen an die gewünschten Produkte weiter. Mit diesem Konzept können Sie Implementierungsaufgaben zusammenfassen, insbesondere, wenn mehrere Datenlösungen vorhanden sind.

Die folgende Abbildung zeigt, wie das Adobe Streaming-Mediensammlungs-Add-on implementiert werden kann, um Experience Platform Edge zu verwenden und Daten in Analysis Workspace verfügbar zu machen, entweder in Adobe Analytics oder Customer Journey Analytics:

![CJA-Workflow](assets/streaming-media-edge.png)

Einen Überblick über alle Implementierungsoptionen, einschließlich Implementierungsmethoden, die Experience Platform Edge nicht verwenden, finden Sie unter [Implementieren des Streaming Media Collection Add-ons](/help/implementation/overview.md).

Unabhängig davon, ob Sie das Adobe Experience Platform Web SDK, das Adobe Experience Platform Mobile SDK, das Adobe Experience Platform Roku SDK oder die API verwenden, um das Streaming Media Collection Add-on mit Experience Edge zu implementieren, müssen Sie zunächst die folgenden Abschnitte ausführen:

## Einrichten des Schemas in Adobe Experience Platform

Um die Datenerfassung für die Verwendung in allen Anwendungen zu standardisieren, die Adobe Experience Platform nutzen, hat Adobe das offene und öffentlich dokumentierte Standard Experience-Datenmodell (XDM) erstellt.

Erstellen und Einrichten eines Schemas:

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Schemas, wie unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. Wählen Sie auf der Seite Schemadetails beim Erstellen des Schemas die Option [!UICONTROL **Erlebnisereignis**] bei der Auswahl der Basisklasse für das Schema.

   ![Feldergruppen hinzugefügt](assets/schema-experience-event.png)

1. Klicken Sie auf [!UICONTROL **Weiter**].

1. Geben Sie einen Anzeigenamen und eine Beschreibung für das Schema an und wählen Sie dann [!UICONTROL **Beenden**].

1. Im [!UICONTROL **Komposition**] im [!UICONTROL **Feldergruppen**] Bereich, wählen Sie [!UICONTROL **Hinzufügen**], suchen Sie dann nach den folgenden neuen Feldergruppen und fügen Sie sie zum Schema hinzu:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nachdem Sie die Feldergruppen hinzugefügt haben, sollten sie im [!UICONTROL **Feldergruppen**] wie folgt:

   ![Feldergruppen hinzugefügt](assets/schema-field-groups-added.png)

1. Auswählen [!UICONTROL **Speichern**] , um Ihre Änderungen zu speichern.

1. (Optional) Sie können bestimmte Felder ausblenden, die nicht von der Media Edge-API verwendet werden. Das Ausblenden dieser Felder erleichtert das Lesen und Verstehen des Schemas, ist jedoch nicht erforderlich. Diese Felder beziehen sich nur auf die Felder im `MediaAnalytics Interaction Details` fieldgroup.

+++ Erweitern Sie hier , um Anweisungen zu Feldern anzuzeigen, die Sie ausblenden können.

   1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `Media Collection Details` und wählen Sie [!UICONTROL **Zugehörige Felder verwalten**].

      ![manage-related-fields](assets/manage-related-fields.png)

   1. Aktivieren Sie die Option zum [!UICONTROL **Anzeigenamen für Felder anzeigen**] und aktualisieren Sie dann das Schema wie folgt:

      * Im `Media Collection Details` > `Advertising Details` -Feld die folgenden Berichtsfelder ausblenden: `Ad Completed`, `Ad Started`, und `Ad Time Played`.

      * Im `Media Collection Details` > `Advertising Pod Details` das folgende Berichtsfeld ausblenden: `Ad Break ID`

      * Im `Media Collection Details` > `Chapter Details` -Feld die folgenden Berichtsfelder ausblenden: `Chapter Completed`, `Chapter ID`, `Chapter Started`, und `Chapter Time Played`.

      * Im `Media Collection Details` -Feld, das `List Of States` -Feld.

        ![Anzeigen von Mediensammlungsstatus](assets/schema-hide-media-collection-states.png)

      * Im `Media Collection Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` -Feld die folgenden Berichtsfelder ausblenden: `Player State Count`, `Player State Set`, und `Player State Time`.

        ![Ausblenden von Feldern](assets/schema-hide-listofstates.png)

      * Im `Media Collection Details` > `Qoe Data Details` -Feld die folgenden Berichtsfelder ausblenden: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration`, und `Total Stalling Duration`.

      * Im `Media Collection Details` > `Session Details` -Feld die folgenden Berichtsfelder ausblenden: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played`, und `Video Segment`.

   1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

   1. Im [!UICONTROL **Struktur**] -Bereich, aktivieren Sie die Option [!UICONTROL **Anzeigenamen für Felder anzeigen**] und wählen Sie dann die `List Of Media Collection Downloaded Content Events` -Feld.

   1. Auswählen [!UICONTROL **Zugehörige Felder verwalten**] und aktualisieren Sie dann das Schema wie folgt:


      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` -Feld die folgenden Berichtsfelder ausblenden: `Ad Completed`, `Ad Started`, und `Ad Time Played`.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` das folgende Berichtsfeld ausblenden: `Ad Break ID`

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` -Feld die folgenden Berichtsfelder ausblenden: `Chapter Completed`, `Chapter ID`, `Chapter Started`, und `Chapter Time Played`.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` -Feld, das `List Of States` -Feld.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` und `Media Collection Details` > `List Of States Start` -Feld die folgenden Berichtsfelder ausblenden: `Player State Count`, `Player State Set`, und `Player State Time`.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` -Feld die folgenden Berichtsfelder ausblenden: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration`, und `Total Stalling Duration`.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` -Feld die folgenden Berichtsfelder ausblenden: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played`, und `Video Segment`.

      * Im `List Of Media Collection Downloaded Content Events` > `Media Details`  -Feld, das `Media Session ID` -Feld.

   1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

   1. Im [!UICONTROL **Struktur**] Bereich, wählen Sie die `Media Reporting Details` Feld auswählen [!UICONTROL **Zugehörige Felder verwalten**].

   1. Aktivieren Sie die Option zum [!UICONTROL **Anzeigenamen für Felder anzeigen**] und aktualisieren Sie dann das Schema wie folgt:

      * Im `Media Reporting Details` -Feld die folgenden Felder ausblenden: `Error Details`, `List Of States End`, `List of States Start`, und `Media Session ID`.

   1. Auswählen [!UICONTROL **Bestätigen**] > [!UICONTROL **Speichern**]  , um Ihre Änderungen zu speichern.

1. Fahren Sie mit [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

## Datensatz in Adobe Experience Platform erstellen

1. Stellen Sie sicher, dass Sie ein Schema wie in [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Datensatzes, wie unter [Handbuch zur Benutzeroberfläche von Datensätzen](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=de#create).

   Wählen Sie bei der Auswahl eines Schemas für Ihren Datensatz das zuvor von Ihnen erstellte Schema aus, wie unter [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Fahren Sie mit [Konfigurieren eines Datenspeichers in Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Konfigurieren eines Datenspeichers in Adobe Experience Platform

1. Stellen Sie sicher, dass Sie einen Datensatz erstellt haben, wie unter [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

1. Erstellen Sie einen neuen Datastream, wie unter [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de).

   Stellen Sie beim Erstellen des Datastreams sicher, dass Sie die folgenden Konfigurationsoptionen vornehmen:

   * Im [!UICONTROL **Ereignisschema**] beim Erstellen des Datastreams das Schema auswählen, das Sie in [Einrichten des Schemas in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Wählen Sie [!UICONTROL **Speichern**] aus.

     >[!IMPORTANT]
     >
         > Nicht auswählen [!UICONTROL **Zuordnung speichern und hinzufügen**] weil dies zu Zuordnungsfehlern für das Feld &quot;Zeitstempel&quot;führt.
     
     ![Erstellen von Datenspeichern und Auswählen von Schemata](assets/datastream-create-schema.png)

   * Fügen Sie je nachdem, ob Sie Adobe Analytics oder Customer Journey Analytics verwenden, einen der folgenden Dienste zum Datastream hinzu:

      * [!UICONTROL **Adobe Analytics**] (bei Verwendung von Adobe Analytics)

        Wenn Sie Adobe Analytics verwenden, stellen Sie sicher, dass Sie eine Report Suite definieren, wie unter [Erstellen einer Report Suite](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * [!UICONTROL **Adobe Experience Platform**] (bei Verwendung von Customer Journey Analytics)

     Informationen zum Hinzufügen eines Dienstes zu einem Datastream finden Sie im Abschnitt &quot;Dienste zu einem Datastream hinzufügen&quot;unter [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Hinzufügen des Adobe Analytics-Dienstes](assets/datastream-add-service.png)

   * Erweitern [!UICONTROL **Erweiterte Optionen**], und aktivieren Sie dann die [!UICONTROL **Media Analytics**] -Option.

     ![Media Analytics-Option](assets/datastream-media-check.png)

1. Sie sind jetzt bereit, die [Media Edge-API](/help/implementation/edge/implementation-edge-api.md) oder [Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md) , um mit der Erfassung von Medienanalysedaten zu beginnen.

   Nachdem Sie einige Daten erfasst haben, können Sie [Erstellen einer Verbindung im Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Erstellen einer Verbindung in Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.


1. Stellen Sie sicher, dass Sie einen Datastream erstellt haben, wie in [Konfigurieren eines Datenspeichers in Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. Erstellen Sie unter Customer Journey Analytics eine Verbindung, wie unter [Verbindung erstellen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=de).

   Beim Erstellen der Verbindung sind für die Implementierung des Add-ons für die Streaming-Mediensammlung die folgenden Konfigurationsoptionen erforderlich:

   1. Wählen Sie den zuvor erstellten Datensatz aus, wie unter [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

   1. Stellen Sie sicher, dass [!UICONTROL **Alle neuen Daten importieren**] -Einstellung aktiviert ist.

1. Fahren Sie mit [Erstellen einer Datenansicht unter Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Erstellen einer Datenansicht unter Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.

1. Stellen Sie sicher, dass Sie eine Verbindung unter Customer Journey Analytics erstellt haben, wie unter [Erstellen einer Verbindung im Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie unter [Datenansicht erstellen oder bearbeiten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de).

   Beim Erstellen der Datenansicht sind für die Implementierung des Streaming-Mediensammlungs-Add-ons die folgenden Konfigurationsoptionen erforderlich:

   1. Im [!UICONTROL **Verbindung**] -Feld die zuvor von Ihnen erstellte Verbindung aus, wie in [Erstellen einer Verbindung im Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

      Es kann bis zu 15 Minuten dauern, bis die von Ihnen erstellte Verbindung ausgewählt werden kann.

   1. Im [!UICONTROL **Komponenten**] in der [!UICONTROL **Schemafelder**] nach jeder Komponente suchen, die in den Tabellen unten aufgeführt ist, und ziehen Sie sie in die [!UICONTROL **Metriken**] Bedienfeld. Wenn mehrere Felder mit demselben Namen vorhanden sind, verwenden Sie den XDM-Pfad, um sicherzustellen, dass es sich um das richtige Feld handelt.

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
      | 10% Fortschrittsmarkierung | mediaReporting.sessionDetails.hasProgress10 |
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

      | Name der Komponente | Kontext-Label |
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

1. Fahren Sie mit [Erstellen und Konfigurieren eines Projekts im Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Erstellen und Konfigurieren eines Projekts im Customer Journey Analytics

1. Stellen Sie sicher, dass Sie eine Datenansicht in Customer Journey Analytics erstellt haben, wie unter [Erstellen einer Datenansicht unter Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

1. In Customer Journey Analytics im [!UICONTROL **Workspace**] in der [!UICONTROL **Projekte**] Bereich, auswählen [!UICONTROL **Projekt erstellen**].

1. Auswählen [!UICONTROL **Leeres Projekt**] > [!UICONTROL **Erstellen**].

1. Wählen Sie im neuen Projekt die zuvor erstellte Datenansicht aus.

   Beim Erstellen von Bedienfeldern in Ihrem Projekt können Sie alle Komponenten verwenden, die Sie Ihrer Datenansicht hinzugefügt haben, wie unter [Erstellen einer Datenansicht unter Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

   Die folgenden vier Bedienfelder sind Beispiele für Bedienfelder, die Sie erstellen können:

   ![Hauptinhaltsbereich](assets/main-content-panel.png)

   ![Bedienfeld &quot;Kapitel und Anzeigen&quot;](assets/chapter-and-ads-panel.png)

   ![QoE-Bedienfeld](assets/qoe-panel.png)

   ![Platzierungsstatusbereich](assets/player-state-panel.png)

1. Wählen Sie die **Bedienfelder** Symbol in der linken Leiste, und ziehen Sie dann in die [!UICONTROL **Gleichzeitige Medienbetrachter**] und [!UICONTROL **Medienwiedergabedauer**] Bedienfeld.

   Die beiden Bedienfelder sollten wie folgt aussehen:

   ![Bedienfeld &quot;Gleichzeitige Medienbetrachter&quot;](assets/media-concurrent-viewers-panels.png)

   ![Zeitfenster für die Medienwiedergabe](assets/media-playback-time-spent-panels.png)

1. Geben Sie das Projekt wie unter [Freigeben von Projekten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   Wenn die Benutzer, für die Sie freigeben möchten, nicht verfügbar sind, stellen Sie sicher, dass die Benutzer über einen Benutzer- und Administratorzugriff auf Customer Journey Analytics in der Adobe Admin Console verfügen.

1. Fahren Sie mit [Daten an Experience Platform Edge senden](#send-data-to-experience-platform-edge).

## Daten an Experience Platform Edge senden

Je nach Datentyp, den Sie an Experience Platform Edge senden möchten, können Sie eine der folgenden Methoden verwenden:

### Web: Verwenden des Adobe Experience Platform Web SDK

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Webdaten mit dem Adobe Experience Platform Web SDK an Edge senden](/help/implementation/edge/edge-web-sdk.md)

* [Migrieren zur Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobile: Verwenden des Adobe Experience Platform Mobile SDK

Verwenden Sie die folgenden Dokumentationsressourcen, um die Implementierung für iOS und Android abzuschließen:

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API-Referenz](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrieren zur Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku: Adobe Experience Platform Roku SDK

* [Erste Schritte](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main)

* [Migrieren zur Adobe Streaming Media for Edge Network-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API: Web und andere

Die API ist derzeit die einzige unterstützte Methode zum Senden von Webdaten an Experience Platform Edge.

Die API ist auch verfügbar, wenn Sie eine benutzerdefinierte Implementierung der Edge-APIs verwenden möchten.

Weitere Informationen zur Media Edge-API finden Sie in den folgenden Ressourcen:

* [Übersicht über die Media Edge API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Erste Schritte mit der Media Edge-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Handbuch zur Fehlerbehebung bei Media Edge API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Verwenden der Open API Specification-Datei für Media Edge-APIs](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)

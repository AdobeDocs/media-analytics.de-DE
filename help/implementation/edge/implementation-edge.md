---
title: Installieren von Media Analytics mit Experience Platform Edge
description: Erfahren Sie, wie Sie Adobe-Streaming-Medien mit Experience Platform Edge implementieren.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 798a2b155742476f0bf648b482c75e0b03449977
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 10%

---

# Installieren von Media Analytics mit Experience Platform Edge

Mit Adobe Experience Platform Edge können Sie Daten, die für mehrere Produkte bestimmt sind, an einen zentralen Ort senden. Experience Edge leitet die entsprechenden Informationen an die gewünschten Produkte weiter. Mit diesem Konzept können Sie Implementierungsaufgaben zusammenfassen, insbesondere, wenn mehrere Datenlösungen vorhanden sind.

Die folgende Abbildung zeigt, wie eine Media Analytics-Implementierung Experience Platform Edge verwenden kann, um Daten in Analysis Workspace entweder in Adobe Analytics oder Customer Journey Analytics verfügbar zu machen:

![CJA-Workflow](assets/cja-implementation.png)

Eine Übersicht über alle Implementierungsoptionen, einschließlich Implementierungsmethoden, die Experience Platform Edge nicht verwenden, finden Sie unter [Streaming-Medien für Adobe Analytics oder Customer Journey Analytics implementieren](/help/implementation/overview.md).

>[!IMPORTANT]
>
>Streaming-Medien sind noch nicht in das AEP Web SDK integriert.

Unabhängig davon, ob Sie das Mobile SDK oder die API verwenden, um Streaming-Medien mit Experience Edge zu implementieren, müssen Sie zunächst die folgenden Abschnitte ausführen:

## Einrichten des Schemas in Adobe Experience Platform

Um die Datenerfassung für die Verwendung in allen Anwendungen zu standardisieren, die Adobe Experience Platform nutzen, hat Adobe das offene und öffentlich dokumentierte Standard Experience-Datenmodell (XDM) erstellt.

Erstellen und Einrichten eines Schemas:

1. Beginnen Sie in Adobe Experience Platform mit der Erstellung des Schemas, wie unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   Wählen Sie beim Erstellen des Schemas [!UICONTROL **XDM ExperienceEvent**] aus dem [!UICONTROL **Schema erstellen**] Dropdown-Menü.

1. Im [!UICONTROL **Komposition**] im [!UICONTROL **Feldergruppen**] Bereich, wählen Sie [!UICONTROL **Hinzufügen**], suchen Sie dann nach den folgenden neuen Feldergruppen und fügen Sie sie zum Schema hinzu:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nachdem Sie die Feldergruppen hinzugefügt haben, sollten sie im [!UICONTROL **Feldergruppen**] wie folgt:

   ![Feldergruppen hinzugefügt](assets/schema-field-groups-added.png)

1. Auswählen [!UICONTROL **Bestätigen**] , um Ihre Änderungen zu speichern.

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

        Wenn Sie Adobe Analytics verwenden, stellen Sie sicher, dass Sie eine Report Suite wie im Abschnitt beschrieben definieren [Report Suite definieren](#define-a-report-suite) in diesem Artikel.

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

   Beim Erstellen der Verbindung sind für die Implementierung von Streaming-Medien die folgenden Konfigurationsoptionen erforderlich:

   1. Wählen Sie den zuvor erstellten Datensatz aus, wie unter [Datensatz in Adobe Experience Platform erstellen](#create-a-dataset-in-adobe-experience-platform).

   1. Stellen Sie sicher, dass [!UICONTROL **Alle neuen Daten importieren**] -Einstellung aktiviert ist.

1. Fahren Sie mit [Erstellen einer Datenansicht unter Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Erstellen einer Datenansicht unter Customer Journey Analytics

>[!NOTE]
>
>Das folgende Verfahren ist nur erforderlich, wenn Sie Customer Journey Analytics verwenden.

1. Stellen Sie sicher, dass Sie eine Verbindung unter Customer Journey Analytics erstellt haben, wie unter [Erstellen einer Verbindung im Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie unter [Datenansicht erstellen oder bearbeiten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de).

   Beim Erstellen der Datenansicht sind für die Implementierung von Streaming-Medien die folgenden Konfigurationsoptionen erforderlich:

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

1. Fahren Sie mit [Erstellen und Konfigurieren eines Projekts im Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Erstellen und Konfigurieren eines Projekts im Customer Journey Analytics

1. Stellen Sie sicher, dass Sie eine Datenansicht in Customer Journey Analytics erstellt haben, wie unter [Erstellen einer Datenansicht unter Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

1. In Customer Journey Analytics im [!UICONTROL **Arbeitsbereich**] in der [!UICONTROL **Projekte**] Bereich, auswählen [!UICONTROL **Projekt erstellen**].

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

### Mobile: Verwenden des mobilen Adobe Experience Platform-SDK

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

Weitere Informationen zur Medien-Edge-API finden Sie in den folgenden Ressourcen:

* [Übersicht über die Media Edge-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Erste Schritte mit der Media Edge API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Handbuch zur Fehlerbehebung bei Media Edge API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Verwenden der Open API Specification-Datei für Media Edge-APIs](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)

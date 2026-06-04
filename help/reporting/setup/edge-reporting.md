---
title: Einrichten von Berichten für Edge-Implementierungen
description: Konfigurieren Sie Customer Journey Analytics für Berichte zu Streaming-Mediendaten, die über Edge Network erfasst wurden.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 18%

---

# Einrichten von Berichten für Edge-Implementierungen

Nachdem Sie die Streaming Media-Sammlung über die Edge Network implementiert haben, konfigurieren Sie Customer Journey Analytics so, dass Berichte zu den erfassten Daten erstellt werden. Auf dieser Seite wird beschrieben, wie Sie eine Verbindung, eine Datenansicht und ein Projekt für Streaming-Medien erstellen.

>[!NOTE]
>
>Auf dieser Seite wird das Reporting in Customer Journey Analytics beschrieben, dem empfohlenen Ziel für Edge-Implementierungen. Wenn Ihr Datenstrom stattdessen Streaming-Mediendaten an Adobe Analytics sendet, finden Sie weitere Informationen unter [Einrichten von Berichten für reine Analytics-Implementierungen](analytics-reporting.md).

* **Voraussetzungen**: Schließen Sie eine Edge-Implementierung ab und erfassen Sie einige Daten. Siehe die Übersicht über die Edge-Implementierung ](/help/implementation/edge/overview.md)0) und die von Ihnen gewählte Implementierungsmethode.[

## Erstellen einer Verbindung in Customer Journey Analytics

1. Erstellen Sie in Customer Journey Analytics eine Verbindung, wie in [Verbindung erstellen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=de) beschrieben.

   Beim Erstellen der Verbindung sind die folgenden Auswahlen für Streaming-Medien erforderlich:

   1. Wählen Sie den Datensatz aus, den Sie während der Implementierung erstellt haben.

   1. Stellen Sie sicher **[!UICONTROL dass die Einstellung „Alle neuen]** importieren“ aktiviert ist.

1. Fahren Sie mit [Datenansicht in Customer Journey Analytics erstellen“ ](#create-a-data-view-in-customer-journey-analytics).

## Erstellen einer Datenansicht in Customer Journey Analytics

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie in [Erstellen oder Bearbeiten einer Datenansicht](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de) beschrieben.

   1. Wählen **[!UICONTROL im Feld]** die zuvor erstellte Verbindung aus.

      Es kann bis zu 15 Minuten dauern, bis eine neue Verbindung ausgewählt werden kann.

   1. Suchen Sie auf der **[!UICONTROL Komponenten]** im Abschnitt **[!UICONTROL Schemafelder]** in den Tabellen unten nach jeder Komponente und ziehen Sie sie in das Bedienfeld **[!UICONTROL Metriken]**. Wenn mehrere Felder mit demselben Namen vorhanden sind, verwenden Sie den XDM-Pfad, um das richtige Feld zu bestätigen.

      **Hauptinhalt - Inhaltsmetriken**

      | Name der Komponente | XDM-Pfad |
      |----------|---------|
      | Medienstarts | mediaReporting.sessionDetails.isViewed |
      | Mediensegmentansichten | mediaReporting.sessionDetails.hasSegmentView |
      | Inhaltsstarts | mediaReporting.sessionDetails.isPlayed |
      | Inhaltsabschlüsse | mediaReporting.sessionDetails.isCompleted |
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

   1. Aktualisieren Sie die Beschriftungen (im **[!UICONTROL Kontextbeschriftungen]** Dropdown-Menü) für die Komponenten in der folgenden Tabelle. Suchen Sie nach Komponenten, die sich noch nicht im Bedienfeld Metriken befinden, und ziehen Sie sie in das Bedienfeld.

      | Name der Komponente | Kontext-Label |
      |---------|----------|
      | Zeitüberschreitung des Mediensitzungs-Servers | Medien: Sekunden seit letztem Aufruf |
      | Besuchszeit für Medien | Medien: Besuchszeit für Medien |
      | Gesamtpufferdauer | Medien: Gesamtdauer des Puffers |
      | Zeit bis Start | Medien: Zeit bis zum Start |
      | Pausierung – Gesamtdauer | Medien: Pausierung - Gesamtdauer |

   1. Um Ihrem Projekt Aufschlüsselungen hinzuzufügen, fügen Sie die folgenden Dimensionen zum Bedienfeld **[!UICONTROL Dimensionen]** hinzu:

      | XDM-Pfad | Name der Komponente |
      |---------|----------|
      | mediaReporting.states.name | Player-Statusname |
      | mediaReporting.sessionDetails.ID | Mediensitzungs-ID |

      Zusätzlich zu den Dimensionen in dieser Tabelle können Sie alle anderen Dimensionen hinzufügen, nach denen Sie Daten in Ihren Projekten filtern möchten.

1. Wählen Sie **[!UICONTROL Speichern und fortfahren]** > **[!UICONTROL Speichern und beenden]** um Ihre Änderungen zu speichern.

1. Fahren Sie mit [Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics ](#create-and-configure-a-project-in-customer-journey-analytics).

## Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics

1. Wählen Sie in Customer Journey Analytics auf der Registerkarte **[!UICONTROL Workspace]** im Bereich **[!UICONTROL Projekte]** die Option **[!UICONTROL Projekt erstellen]**.

1. Wählen Sie **[!UICONTROL Leeres Projekt]** > **[!UICONTROL Erstellen]** aus.

1. Wählen Sie im neuen Projekt die Datenansicht aus, die Sie zuvor erstellt haben.

   Beim Erstellen von Bedienfeldern in Ihrem Projekt können Sie alle Komponenten verwenden, die Sie Ihrer Datenansicht hinzugefügt haben.

1. Wählen Sie das Symbol **Bedienfelder** in der linken Leiste aus und ziehen Sie dann das Bedienfeld **[!UICONTROL Gleichzeitige Medienbetrachter]** und das Bedienfeld **[!UICONTROL Bei Medienwiedergabe verbrachte Zeit]**.

1. (Bedingt) Wenn Sie benutzerdefinierte Metadaten zu Ihrem Schema hinzugefügt haben, legen Sie die Persistenz für die benutzerdefinierten Felder fest, wie in [Persistenzkomponenteneinstellungen](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) im Customer Journey Analytics-Handbuch beschrieben.

1. Geben Sie das Projekt frei, wie unter [Freigeben von Projekten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en) beschrieben.

   >[!NOTE]
   >
   >Wenn die Benutzenden, für die Sie freigeben möchten, nicht verfügbar sind, stellen Sie sicher, dass die Benutzenden in der Adobe Admin Console Benutzer- und Administratorzugriff auf Customer Journey Analytics haben.

>[!MORELIKETHIS]
>
>* [Medien-Bedienfelder in Workspace](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [Dimensions-Übersicht](/help/reporting/dimensions/overview.md)
>* [Metriken - Übersicht](/help/reporting/metrics/overview.md)

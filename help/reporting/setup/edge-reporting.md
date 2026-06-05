---
title: Einrichten von Berichten für Edge-Implementierungen
description: Konfigurieren Sie Customer Journey Analytics für Berichte zu Streaming-Mediendaten, die über Edge Network erfasst wurden.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 8%

---

# Einrichten von Berichten für Edge-Implementierungen

Nachdem Sie die Streaming Media-Sammlung über die Edge Network implementiert haben, konfigurieren Sie Customer Journey Analytics so, dass Berichte zu den erfassten Daten erstellt werden.

>[!NOTE]
>
>Auf dieser Seite wird das Reporting in Customer Journey Analytics beschrieben, dem empfohlenen Ziel für Edge-Implementierungen. Wenn Ihr Datenstrom stattdessen Streaming-Mediendaten an Adobe Analytics sendet, finden Sie weitere Informationen unter [Einrichten von Berichten für reine Analytics-Implementierungen](analytics-reporting.md).

* **Voraussetzungen**: Schließen Sie eine Edge-Implementierung ab und erfassen Sie einige Daten. Siehe die Übersicht über die Edge-Implementierung [&#128279;](/help/implementation/edge/overview.md)0) und die von Ihnen gewählte Implementierungsmethode.

## Erstellen einer Verbindung in Customer Journey Analytics

1. Erstellen Sie in Customer Journey Analytics eine Verbindung, wie in [Verbindung erstellen](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-connections/create-connection) beschrieben. Stellen Sie beim Erstellen der Verbindung sicher **[!UICONTROL dass das Kontrollkästchen „Alle neuen Daten]**&quot; aktiviert ist.

## Erstellen einer Datenansicht in Customer Journey Analytics

1. Erstellen Sie in Customer Journey Analytics eine Datenansicht, wie in [Erstellen oder Bearbeiten einer Datenansicht](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/create-dataview) beschrieben.

   1. Wählen **[!UICONTROL im Feld]** die zuvor erstellte Verbindung aus. Es kann bis zu 15 Minuten dauern, bis neue Verbindungen angezeigt werden.

   1. Suchen Sie auf der Registerkarte **[!UICONTROL Komponenten]** im Abschnitt **[!UICONTROL Schemafelder]** nach jeder Komponente in der unten stehenden Tabelle und ziehen Sie sie in das entsprechende Bedienfeld **[!UICONTROL Dimensionen]** oder **[!UICONTROL Metriken]**. Wenn mehrere Felder mit demselben Namen vorhanden sind, verwenden Sie den XDM-Pfad, um das richtige Feld zu bestätigen. Wenden Sie die Kontextbeschriftung an, die in der Dropdown **[!UICONTROL Liste „Kontextbeschriftungen]** in den Komponenteneinstellungen angezeigt wird.

      | Komponente | Typ | XDM-Pfad | Kontext-Label |
      |---|---|---|---|
      | [Inhalt](/help/reporting/dimensions/content.md) | Dimension | `mediaReporting.sessionDetails.name` | Medien: Inhalts-ID |
      | [Inhaltsname](/help/reporting/dimensions/content-name.md) | Dimension | `mediaReporting.sessionDetails.friendlyName` | Medien: Videoname |
      | [Inhaltslänge](/help/reporting/dimensions/content-length.md) | Dimension | `mediaReporting.sessionDetails.length` | Medien: Videolänge |
      | [Anzeigen](/help/reporting/dimensions/show.md) | Dimension | `mediaReporting.sessionDetails.show` | Medien: Anzeigen |
      | [Staffel](/help/reporting/dimensions/season.md) | Dimension | `mediaReporting.sessionDetails.season` | Medien: Staffel |
      | [Folge](/help/reporting/dimensions/episode.md) | Dimension | `mediaReporting.sessionDetails.episode` | Medien: Folge |
      | Ereignistyp | Dimension | `eventType` | Medien: Ereignistyp |
      | [Besuchszeit für Inhalt](/help/reporting/metrics/content-time-spent.md) | Metrik | `mediaReporting.sessionDetails.timePlayed` | Medien: Besuchszeit für Inhalt |
      | [Besuchszeit für Medien](/help/reporting/metrics/media-time-spent.md) | Metrik | `mediaReporting.sessionDetails.totalTimePlayed` | Medien: Besuchszeit für Medien |
      | [Pausierung insgesamt](/help/reporting/metrics/total-pause-duration.md) | Metrik | `mediaReporting.sessionDetails.pauseTime` | Medien: Pausierung - Gesamtdauer |
      | [Zeit bis zum Start](/help/reporting/metrics/time-to-start.md) | Metrik | `mediaReporting.qoeDataDetails.timeToStart` | Medien: Zeit bis zum Start |
      | [Gesamtdauer des Puffers](/help/reporting/metrics/total-buffer-duration.md) | Metrik | `mediaReporting.qoeDataDetails.bufferTime` | Medien: Gesamtdauer des Puffers |
      | Timeout des Mediensitzungs-Servers | Metrik | `mediaReporting.sessionDetails.secondsSinceLastCall` | Medien: Sekunden seit letztem Aufruf |

      >[!IMPORTANT]
      >
      >Die Kontextbeschriftungen in dieser Tabelle sind erforderlich, damit die Bedienfelder für Streaming-Medien funktionieren. Customer Journey Analytics verwendet diese Metriken zur automatischen Berechnung der **gleichzeitige Viewer** und **Wiedergabedauer** abgeleiteten Metriken (verwendet von den Bedienfeldern [Gleichzeitige Medienbetrachter](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) und [Mit Medienwiedergabe verbrachte Zeit](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)) und zum Ausfüllen der Berichtsoptionen im Bedienfeld [Medien-Zielgruppendurchschnitt pro Minute](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel).

      An dieser Stelle können Sie Ihrer [&#x200B; beliebige andere &#x200B;](/help/reporting/dimensions/overview.md)Dimensionen[&#x200B; oder &#x200B;](/help/reporting/metrics/overview.md) hinzufügen. Jede Seite listet den XDM-Pfad für diese Komponente auf.

1. Wählen Sie **[!UICONTROL Speichern und fortfahren]** → **[!UICONTROL Speichern und]**) aus, um Ihre Änderungen zu speichern.

## Erstellen und Konfigurieren eines Projekts in Customer Journey Analytics

1. Wählen Sie in Customer Journey Analytics auf der Registerkarte **[!UICONTROL Workspace]** im Bereich **[!UICONTROL Projekte]** die Option **[!UICONTROL Projekt erstellen]**.

1. Wählen Sie **[!UICONTROL Leeres Projekt]** → **[!UICONTROL Erstellen]** aus.

1. Wählen Sie im neuen Projekt die Datenansicht aus, die Sie zuvor erstellt haben.

   Beim Erstellen von Bedienfeldern in Ihrem Projekt können Sie alle Komponenten verwenden, die Sie Ihrer Datenansicht hinzugefügt haben.

1. Wählen Sie in der linken Leiste das **Bedienfelder** aus und ziehen Sie dann die Bedienfelder **[!UICONTROL Medien-Zielgruppendurchschnitt pro Minute]**, **[!UICONTROL Medien-gleichzeitige Betrachter]** und **[!UICONTROL Medienwiedergabezeit]**.

1. (Bedingt) Wenn Sie benutzerdefinierte Metadaten zu Ihrem Schema hinzugefügt haben, legen Sie die Persistenz für die benutzerdefinierten Felder fest, wie in [Persistenzkomponenteneinstellungen](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) im Customer Journey Analytics-Handbuch beschrieben.

1. Geben Sie das Projekt frei, wie unter [Freigeben von Projekten](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en) beschrieben.

   >[!NOTE]
   >
   >Wenn die Benutzenden, für die Sie freigeben möchten, nicht verfügbar sind, stellen Sie sicher, dass die Benutzenden in der Adobe Admin Console Benutzer- und Administratorzugriff auf Customer Journey Analytics haben.

## Verfügbare Medienbedienfelder in Customer Journey Analytics

Analysis Workspace in Customer Journey Analytics umfasst drei dedizierte Medienbedienfelder für Kunden mit dem Add-on „Streaming Media Collection“. Diese Bedienfelder bieten vorgefertigte Visualisierungen für die gängigsten Reporting-Anforderungen für Streaming-Medien.

* **[Medien-Zielgruppendurchschnitt pro Minute](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**: Vergleicht die durchschnittliche Nutzung von Inhalten in Programmen beliebiger Länge oder Genres. Unterstützt sowohl bestimmte Inhaltsmodi (dauerbasiert) als auch benutzerdefinierte Zeitraummodi und ermöglicht die nachträgliche Aktualisierung von Klassifizierungen der Dauer.
* **[Gleichzeitige Medienbetrachter](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**: Analysiert gleichzeitige Betrachter im Zeitverlauf, um Spitzen bei gleichzeitigen Betrachtern und Abfallpunkten zu ermitteln. Unterstützt eine konfigurierbare Granularität und Serienaufschlüsselung nach Segmenten, Dimensionen oder Datumsbereichen.
* **[Bei Medienwiedergabe verbrachte Zeit](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**: Analysiert die Wiedergabedauer im Zeitverlauf mit Details zu Spitzen- und Tiefstzeiten. Unterstützt konfigurierbare Granularität und Ausgabeformat (Stunden oder Minuten).

>[!MORELIKETHIS]
>
>* [Dimensions-Übersicht](/help/reporting/dimensions/overview.md)
>* [Metriken - Übersicht](/help/reporting/metrics/overview.md)

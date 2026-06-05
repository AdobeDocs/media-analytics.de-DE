---
title: Einrichten des Reportings für reine Analytics-Implementierungen
description: Aktivieren Sie die Media Report Suite-Module in Adobe Analytics, damit Streaming-Mediendaten erfasst und gemeldet werden können.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 11%

---

# Einrichten des Reportings für reine Analytics-Implementierungen

Bevor eine reine Analytics-Implementierung Streaming-Mediendaten erfassen kann, muss jede Report Suite, die diese Daten erhält, so konfiguriert werden, dass die entsprechenden Medienmodule aktiviert werden. Auf dieser Seite wird beschrieben, wie Sie diese Module aktivieren und wo Sie die resultierenden Berichte finden.

* **Voraussetzungen**: Eine Adobe Analytics-Implementierung. Siehe [Nur Analytics-Implementierung - Übersicht](/help/implementation/analytics-only/overview.md) und die ausgewählte Implementierungsmethode.

## Aktivieren von Medienberichten für eine Report Suite

Jede Report Suite, die Medienmetriken erfasst, muss konfiguriert werden, bevor Mediendaten gesendet werden.

1. Navigieren Sie in [](https://experience.adobe.com/analytics) zu **[!UICONTROL Admin]** → **[!UICONTROL Report Suites]**.
1. Wählen Sie die Report Suites aus, die Mediendaten erfassen. Wählen Sie **[!UICONTROL Einstellungen bearbeiten]** → **[!UICONTROL Medienverwaltung]** → **[!UICONTROL Medienberichte]**.

   ![Screenshot des Report Suite Manager-Menüs](assets/media-reporting.png)

1. Aktivieren Sie auf **[!UICONTROL Seite]** Medienberichte“ die gewünschten Streaming-Medienmodule (siehe unten).

1. Wählen Sie **[!UICONTROL Speichern] aus**

   Wenn diese Report Suite bereits für die Erfassung von Mediendaten konfiguriert ist, wird nach Auswahl von **[!UICONTROL Speichern]** eine zusätzliche Konfigurationsseite angezeigt. Wenn die Seite **[!UICONTROL Media-Core-Messung]** angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

## Verfügbare Streaming-Medienmodule

Die Medienmessung enthält folgende Module:

* **[!UICONTROL Media Core]**: Erforderlich für das Tracking aller Streaming-Medien. Es reserviert Lösungsvariablen für die Inhaltswiedergabe und Sitzungsdaten.

  +++Auswählen, um Dimensionen und Metriken anzuzeigen

   * **Dimensionen:**
      * [[!UICONTROL Inhalt]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL Inhaltskanal]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Inhaltslänge (variabel)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Inhaltsname (Variable)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL Name des Inhalts-Players]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL Inhaltssegment]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL Content-Typ]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Medienpfad]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL Mediensitzungs-ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Stream-Typ]](/help/reporting/dimensions/stream-type.md)
   * **Metriken:**
      * [[!UICONTROL Zielgruppendurchschnitt pro Minute]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Inhalt abgeschlossen]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Inhaltswiederaufnahmen]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Inhaltssegmentansichten]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Ereignisse anhalten]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL Betroffene Streams angehalten]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL Fortschrittsmarken]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL Pausierung insgesamt]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL Eindeutige Wiedergabezeit]](/help/reporting/metrics/unique-time-played.md)

  +++

* **[!UICONTROL Medienanzeigen]**: Ermöglicht das Tracking von Anzeigen innerhalb des Medieninhalts.

  +++Auswählen, um Dimensionen, Klassifizierungen und Metriken anzuzeigen

   * **Dimensionen:**
      * [[!UICONTROL Anzeige]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Anzeige in Pod-Position]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL Anzeigenlänge (variabel)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL Anzeigename (Variable)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL Player-Namen hinzufügen]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL Anzeigen-Pod]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL Kampagnen-ID]](/help/reporting/dimensions/campaign-id.md)
   * **Klassifizierungsdimensionen:**
      * [[!UICONTROL Asset-ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL Inhaltsbewertung]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative-ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL Datum der Erstausstrahlung]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL Erstes digitales Datum]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Pod-Name]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Position des Pods]](/help/reporting/dimensions/pod-position.md)
   * **Metriken:**
      * [[!UICONTROL Anzeige abgeschlossen]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL Anzeigenstarts]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL Besuchszeit für Anzeige]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL Besuchszeit für Medien]](/help/reporting/metrics/media-time-spent.md)

  +++

* **[!UICONTROL Medienkapitel]**: Aktiviert das Tracking von Kapiteln innerhalb von Medieninhalten.

  +++Auswählen, um Dimensionen, Klassifizierungen und Metriken anzuzeigen

   * **Dimension:**
      * [[!UICONTROL Kapitel]](/help/reporting/dimensions/chapter.md)
   * **Klassifizierungsdimensionen:**
      * [[!UICONTROL Kapitellänge]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL Kapitelname]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL Kapitelversatz]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL Kapitelposition]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL Urheber]](/help/reporting/dimensions/originator.md)
   * **Metriken:**
      * [[!UICONTROL Kapitel abgeschlossen]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL Kapitelstarts]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL Besuchszeit für Kapitel]](/help/reporting/metrics/chapter-time-spent.md)

  +++

* **[!UICONTROL Medienqualität]**: Ermöglicht das Tracking von Wiedergabequalitätsdaten, einschließlich Pufferung, Bitrate und Fehlerereignissen.

  +++Auswählen, um Dimensionen und Metriken anzuzeigen

   * **Dimensionen:**
      * [[!UICONTROL Durchschnittliche Bitrate]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL Bitratenänderungen]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL Pufferereignisse]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL Dropped Frames]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL Fehler]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL Externe Fehler-IDs]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL Player SDK-Fehler-IDs]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL Zeit bis zum Start]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL Gesamtdauer des Puffers]](/help/reporting/dimensions/total-buffer-duration.md)
   * **Metriken:**
      * [[!UICONTROL Durchschnittliche Bitrate]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL Von Bitratenänderung betroffene Streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL Pufferereignisse]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL Vom Puffer betroffene Streams]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL Von Dropped Frames betroffene Streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Dropped Frames]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Drops vor dem Start]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Fehlerereignisse]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL Von Fehlern betroffene Streams]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Zeit bis zum Start]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Gesamtdauer des Puffers]](/help/reporting/metrics/total-buffer-duration.md)

  +++

* **[!UICONTROL Videometadaten]**: Ermöglicht das Tracking von Standard-Videoinhaltsattributen wie Sendung, Staffel und Genre.

  +++Auswählen, um Dimensionen und Metriken anzuzeigen

   * **Dimensionen:**
      * [[!UICONTROL Anzeigenladevorgänge]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL Teil des Tages]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Folge]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Medien-Feed-Typ]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Netzwerk]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL Staffel]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL Anzeigen]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL Typ anzeigen]](/help/reporting/dimensions/show-type.md)
   * **metric:**
      * [[!UICONTROL Autorisiert]](/help/reporting/metrics/authorized.md)

  +++

* **[!UICONTROL Audio-Metadaten]**: Ermöglicht das Tracking von Standard-Audioinhaltsattributen wie Interpret, Album und Sender.

  +++Auswählen, um Dimensionen anzuzeigen

   * **Dimensionen:**
      * [[!UICONTROL Album]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Künstler]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL author]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Beschriftung]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Veröffentlicher]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Station]](/help/reporting/dimensions/station.md)

  +++

* **[!UICONTROL Player-Status-Tracking]**: Ermöglicht die Messung von Standard-Player-Benutzeroberflächenstatus wie Vollbild, Untertitel und Bild in Bild.

  +++Auswählen, um Metriken anzuzeigen

   * **Metriken:**
      * [[!UICONTROL Geschlossene Untertitelanzahl]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL Gesamtdauer für verdeckte Untertitel]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL Anzahl der Vollbilder]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL Gesamtdauer im Vollbildmodus]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL Anzahl der Fokussierungen]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL Gesamtdauer des Fokus]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL Anzahl der Stummschaltungen]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL Gesamtdauer der Stummschaltung]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL Anzahl der Bilder im Bild]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL Gesamtdauer des Bildes]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL Von verdeckten Untertiteln betroffene Streams]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL Vom Vollbildmodus betroffene Streams]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL Von im Fokus betroffene Streams]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL Von Stummschaltung betroffene Streams]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL Vom Bild betroffene Ströme in Bild]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

  +++

## Verfügbare Medienbedienfelder in Adobe Analytics

Analysis Workspace umfasst drei dedizierte Medien-Bedienfelder für Kunden mit dem Add-on Adobe Analytics for Streaming Media . Diese Bedienfelder bieten vorgefertigte Visualisierungen für die gängigsten Reporting-Anforderungen für Streaming-Medien.

* **[Medien-Zielgruppendurchschnitt pro Minute](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)**: Vergleicht die durchschnittliche Nutzung von Inhalten in Programmen beliebiger Länge oder Genres. Unterstützt sowohl bestimmte Inhaltsmodi (dauerbasiert) als auch benutzerdefinierte Zeitraummodi und ermöglicht die nachträgliche Aktualisierung von Klassifizierungen der Dauer.
* **[Gleichzeitige Medienbetrachter](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)**: Analysiert gleichzeitige Betrachter im Zeitverlauf, um Spitzen bei gleichzeitigen Betrachtern und Abfallpunkten zu ermitteln. Unterstützt eine konfigurierbare Granularität und Serienaufschlüsselung nach Segmenten, Dimensionen oder Datumsbereichen.
* **[Bei Medienwiedergabe verbrachte Zeit](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)**: Analysiert die Wiedergabedauer im Zeitverlauf mit Details zu Spitzen- und Tiefstzeiten. Unterstützt konfigurierbare Granularität und Ausgabeformat (Stunden oder Minuten).

>[!MORELIKETHIS]
>
>* [Dimensions-Übersicht](/help/reporting/dimensions/overview.md)
>* [Metriken - Übersicht](/help/reporting/metrics/overview.md)

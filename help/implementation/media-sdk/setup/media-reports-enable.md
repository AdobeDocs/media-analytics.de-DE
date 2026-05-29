---
title: Aktivierung von Medienberichten
description: Erfahren Sie mehr über die Media Report Suite, die Medienmetriken erfasst.  Führen Sie diese Schritte aus, um Medienberichte zu konfigurieren, bevor Mediendaten gesendet werden.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# Aktivierung von Medienberichten

Jede Report Suite, die Medienmetriken erfasst, muss konfiguriert werden, bevor Mediendaten gesendet werden.

1. Navigieren Sie in [](https://experience.adobe.com/analytics) zu **[!UICONTROL Admin]** → **[!UICONTROL Report Suites]**.
1. Wählen Sie die Report Suites aus, die Mediendaten erfassen. Wählen Sie **[!UICONTROL Einstellungen bearbeiten]** → **[!UICONTROL Medienverwaltung]** → **[!UICONTROL Medienberichte]**.

   ![Screenshot des Report Suite Manager-Menüs](assets/media-reporting.png)

1. Aktivieren Sie auf **[!UICONTROL Seite]** Medienberichte“ die gewünschten Komponenten für Streaming-Medien (siehe unten).

1. Wählen Sie **[!UICONTROL Speichern] aus**

   Wenn diese Report Suite bereits zur Erfassung von Mediendaten konfiguriert ist, wird eine zusätzliche Konfigurationsseite angezeigt, nachdem Sie auf **[!UICONTROL Speichern]** klicken. Wenn die Seite **[!UICONTROL Media-Core-Messung]** angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

## Verfügbare Streaming-Medienmodule

Die Medienmessung enthält folgende Module:

* **[!UICONTROL Media Core]**: Erforderlich für das Tracking aller Streaming-Medien. Es reserviert Lösungsvariablen für die Inhaltswiedergabe und Sitzungsdaten.
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
* **[!UICONTROL Medienanzeigen]**: Ermöglicht das Tracking von Anzeigen innerhalb des Medieninhalts.
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
* **[!UICONTROL Medienkapitel]**: Aktiviert das Tracking von Kapiteln innerhalb von Medieninhalten.
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
* **[!UICONTROL Medienqualität]**: Ermöglicht das Tracking von Wiedergabequalitätsdaten, einschließlich Pufferung, Bitrate und Fehlerereignissen.
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
* **[!UICONTROL Videometadaten]**: Ermöglicht das Tracking von Standard-Videoinhaltsattributen wie Sendung, Staffel und Genre.
   * **Dimensionen:**
      * [!UICONTROL Anzeigenladevorgänge]
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
* **[!UICONTROL Audio-Metadaten]**: Ermöglicht das Tracking von Standard-Audioinhaltsattributen wie Interpret, Album und Sender.
   * **Dimensionen:**
      * [[!UICONTROL Album]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Künstler]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL author]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Beschriftung]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Veröffentlicher]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Station]](/help/reporting/dimensions/station.md)
* **[!UICONTROL Player-Status-Tracking]**: Ermöglicht die Messung von Standard-Player-Benutzeroberflächenstatus wie Vollbild, Untertitel und Bild in Bild.
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

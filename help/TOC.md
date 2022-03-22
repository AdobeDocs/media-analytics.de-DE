---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics für Streaming Media
breadcrumb-title: Media Analytics-Anleitung
user-guide-description: Implementieren von Adobe Analytics für Streaming-Medien. Beinhaltet auch Informationen zum Media SDK und zur Media Collection API.
sub-product: media analytics
source-git-commit: 534f6f77d69a8fe3574c214cd56d2f77758c1643
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 100%

---


# Adobe Analytics für Streaming Media {#using}

+ [Messen von Streaming-Medien in Adobe Analytics](media-overview.md)
+ [Unterstützte Geräte und Plattformen](measurement-options/supported-devices.md)
+ Einführung in Analytics für Streaming-Medien {#intro-to-ava}
   + [Voraussetzungen](intro-to-ava/prereqs.md)
   + Implementierungspfade {#implementation-paths}
      + [Überblick](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Client-seitig](intro-to-ava/implementation-paths/client-side-path.md)
      + Andere Implementierungspfade {#other-paths}
         + Milestone-Tracking des Medienmoduls {#mm-milestone-tracking}
            + [Übersicht zu Milestone](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migrieren von Meilensteinen zu Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migration von Milestone zu Custom Link](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Custom Link in Analytics {#cl-in-aa}
            + [Implementierungshandbuch für benutzerdefinierte Links](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Audience Manager-Aktivierung](intro-to-ava/am-enablement.md)
+ Media Analytics-SDK {#sdk-implement}
   + [Häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK](sdk-implement/end-of-support-faqs.md)
   + [SDKs herunterladen](sdk-implement/download-sdks.md)
   + Einrichtung und Konfiguration {#setup}
      + [Überblick](sdk-implement/setup/setup-overview.md)
      + [Android einrichten](sdk-implement/setup/set-up-android.md)
      + [Einrichten von iOS](sdk-implement/setup/set-up-ios.md)
      + JavaScript einrichten {#setup-javascript}
         + [Einrichten von JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Einrichten von JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Einrichten von Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Roku einrichten](sdk-implement/setup/set-up-roku.md)
   + Tracking der Wiedergabe von Streaming-Medien {#track-av-playback}
      + [Überblick](sdk-implement/track-av-playback/track-core-overview.md)
      + Tracking der Core-Wiedergabe von Streaming-Medien {#track-core}
         + [Tracking von Core-Wiedergaben in Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Tracking von Core-Wiedergaben in iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Tracking von Core-Wiedergaben in JavaScript {#track-core-javascript}
            + [Tracking von Core-Wiedergaben in JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Tracking von Core-Wiedergaben in JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Tracking von Core-Wiedergaben in Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Tracking von Core-Wiedergaben in Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Puffer-Tracking {#track-buffering}
         + [Puffer-Tracking in Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Puffer-Tracking in iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Puffer-Tracking in JavaScript {#track-buffering-js}
            + [Puffer-Tracking in JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Puffer-Tracking in JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Puffer-Tracking in Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Puffer-Tracking in Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Suchen-Tracking {#track-seeking}
         + [Suchen-Tracking in Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Suchen-Tracking in iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Suchen-Tracking in JavaScript {#track-seeking-js}
            + [Suchen-Tracking in JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Suchen-Tracking in JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Suchen-Tracking in Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Suchen-Tracking in Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Standard-Metadaten implementieren {#impl-std-metadata}
         + [Standard-Metadaten in Android implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standard-Metadaten in iOS implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-Metadatenschlüssel](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Standard-Metadaten in JavaScript implementieren {#impl-std-md-js}
            + [Standard-Metadaten in JavaScript 2.x implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Standard-Metadaten in JavaScript 3.x implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Standard-Metadaten in Chromecast implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standard-Metadatenparameter – Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Standard-Metadaten in Roku implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standard-Metadatenparameter – Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Anzeigen verfolgen {#track-ads}
      + [Überblick](sdk-implement/track-ads/track-ads-overview.md)
      + [Tracking von Anzeigen in Android](sdk-implement/track-ads/track-ads-android.md)
      + [Tracking von Anzeigen in iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Tracking von Anzeigen in JavaScript {#track-ads-js}
         + [Tracking von Anzeigen in JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Tracking von Anzeigen in JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Tracking von Anzeigen in Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Tracking von Anzeigen in Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Standard-Anzeigenmetadaten implementieren {#impl-std-ad-metadata}
         + [Standardmäßige Anzeigenmetadaten in Android implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Standard-Anzeigenmetadaten in iOS implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Standard-Anzeigenmetadaten in JavaScript implementieren {#impl-std-ad-md-js}
            + [Standard-Anzeigenmetadaten in JavaScript 2.x implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Standard-Anzeigenmetadaten in JavaScript 3.x implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Standard-Anzeigenmetadaten in Roku implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Kapitel und Segmente verfolgen {#track-chapters}
      + [Überblick](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Tracking von Kapiteln und Segmenten in Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Tracking von Kapiteln und Segmenten in iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Tracking von Kapiteln und Segmenten in JavaScript {#track-chapters-js}
         + [Tracking von Kapiteln und Segmenten in JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Tracking von Kapiteln und Segmenten in JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Tracking von Kapiteln und Segmenten in Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Tracking von Kapiteln und Segmenten in Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Erlebnisqualität verfolgen {#track-qos}
      + [Überblick](sdk-implement/track-qos/track-qos-overview.md)
      + [Tracking der Erlebnisqualität in Android](sdk-implement/track-qos/track-qos-android.md)
      + [Tracking der Erlebnisqualität in iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Tracking der Erlebnisqualität in JavaScript {#track-qos-js}
         + [Tracking der Erlebnisqualität in JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Tracking der Erlebnisqualität in JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Tracking der Erlebnisqualität in Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Tracking der Erlebnisqualität in Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Fehler-Tracking {#track-errors}
      + [Überblick](sdk-implement/track-errors/track-errors-overview.md)
      + [Tracking von Fehlern in Android](sdk-implement/track-errors/track-errors-android.md)
      + [Tracking von Fehlern in iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Tracking von Fehlern in JavaScript {#track-errors-js}
         + [Tracking von Fehlern in JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Tracking von Fehlern in JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Tracking von Fehlern in Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Tracking von Fehlern in Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Opt-out und Datenschutz](sdk-implement/opt-out-privacy.md)
   + Tracking-Szenarien {#tracking-scenarios}
      + [VOD-Wiedergabe ohne Anzeigen](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD-Wiedergabe mit Pre-roll-Anzeigen](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [VOD-Wiedergabe mit übersprungenen Anzeigen](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [VOD-Wiedergabe mit einem Kapitel](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [VOD-Wiedergabe mit einem übersprungenen Kapitel](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD-Wiedergabe mit Suche im Hauptinhalt](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [VOD-Wiedergabe mit Pufferung](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Mehrere parallele VOD-Tracker](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Ein VOD-Tracker für mehrere Sitzungen](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Live-Hauptinhalt](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Live-Hauptinhalt mit sequentieller Verfolgung](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validierung {#validation}
      + [Validierungsübersicht](sdk-implement/validation/validation-overview.md)
      + [Test 1: Standardwiedergabe](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Medienunterbrechung](sdk-implement/validation/test2-media-interrupt.md)
      + [Details zum Testaufruf](sdk-implement/validation/test-call-details.md)
      + [Beschreibungen der Heartbeat-Parameter](sdk-implement/validation/heartbeat-params.md)
      + Debugging {#debugging}
         + [SDK-Debugging](sdk-implement/validation/debugging/sdk-debugging.md)
   + Analytics in OTT-Apps {#analytics-with-ott}
      + [App-Zustände verfolgen](sdk-implement/analytics-with-ott/track-app-states.md)
      + [App-Aktionen verfolgen](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Festlegen von Benutzer-IDs](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT und Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT und Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK-Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Behandlung von Anwendungsunterbrechungen während der Wiedergabe](sdk-implement/cookbook/app-interrupts.md)
      + [Beheben von „main:play“ zwischen Anzeigen](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Wiederaufnehmen von inaktiven Sitzungen](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracking in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migration von Media Analytics 1.x zu 2.x {#va-1x-to-2x}
      + [Migrationsübersicht](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Codevergleich: 1.x gegenüber 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [API-Konversion von 1.x zu 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Migration vom Media Analytics SDK zu Launch {#sdk-to-launch}
      + [Migration vom SDK zu Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Handbücher zur Migration vom SDK zu Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [Überblick](media-collection-api/mc-api-overview.md)
   + API-Referenz {#mc-api-ref}
      + [Sitzungsanfrage](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Ereignisanfrage](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Anfrageparameter](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Ereignistypen und -beschreibungen](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON-Validierungsschemas](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementieren der API {#mc-api-impl}
      + [Schnellstart](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Einstellen des HTTP-Anfragetyps in Ihrem Player](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Beziehen einer Sitzungs-ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementieren einer Ereignisanfrage](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validieren von Ereignisanfragen](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Senden von Ping-Ereignissen](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Senden von QoE-Daten](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Unterstützung benutzerspezifischer Metadaten](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Timeout-Bedingungen](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Steuern der Ereignisreihenfolge](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Zeitleisten für das Medien-Tracking {#mc-api-timelines}
      + [Zeitlicher Ablauf 1: Wiedergabe bis zum Ende des Inhalts](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Zeitlicher Ablauf 2: Verlassen der Sitzung durch Anwender](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Zeitlicher Ablauf 3: Kapitel](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Medien-Stream-Zuordnung](media-analytics-cookbook/media-dimensions.md)
+ Metriken und Metadaten {#metrics-and-metadata}
   + [Parameter für Streaming-Medien](metrics-and-metadata/audio-video-parameters.md)
   + [Anzeigenparameter](metrics-and-metadata/ad-parameters.md)
   + [Kapitelparameter](metrics-and-metadata/chapter-parameters.md)
   + [Player-Statusparameter](metrics-and-metadata/player-state-parameters.md)
   + [Qualitätsparameter](metrics-and-metadata/quality-parameters.md)
   + [Segmente](metrics-and-metadata/segments.md)
   + [Berechnete Metriken](metrics-and-metadata/calculated-metrics.md)
+ Berichterstattung und Analyse {#media-reports}
   + [Aktivierung von Medienberichten](media-reports/media-reports-enable.md)
   + Standard-Medienberichte {#media-default-reports}
      + [Übersicht über die Standardberichte](media-reports/media-default-reports/default-reports-overview.md)
      + [Medien-Übersicht](media-reports/media-default-reports/media-reports-overview.md)
      + [Medien-Detail](media-reports/media-default-reports/media-reports-detail.md)
      + [Bericht über Medientagesabschnitt](media-reports/media-default-reports/media-reports-daypart.md)
      + [Bericht über gleichzeitige Medienbetrachter](media-reports/media-default-reports/media-concurrent-viewers.md)
   + Media Workspace-Bedienfelder {#media-workspace-panels}
   + [Bedienfeld „Medien-Zielgruppendurchschnitt pro Minute“](media-reports/media-workspace-panels/average-minute-audience.md)
   + [Bedienfeld „Gleichzeitige Medienbetrachter“](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Bedienfeld „Bei Medienwiedergabe verbrachte Zeit“](media-reports/media-workspace-panels/media-playback-time-spent.md)
   + [Vorlagen für Media Workspace](media-reports/media-workspace-templates.md)
   + [Abrufen von Daten zu gleichzeitigem Betrachten über API](media-reports/media-default-reports/get-concurrent-json20.md)
   + [Abrufen der bei der Medienwiedergabe verbrachten Zeit über API](media-reports/media-default-reports/get-mediaplaybacktimespent-json20.md)
+ [Tracking heruntergeladener Inhalte](media-collection-api/track-downloaded-content.md)
+ Player-Status-Tracking {#player-state-tracking}
   + [Überblick](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Standardmäßige und benutzerdefinierte Status](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementierung und Reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Beispiele für Player-Status-Tracking](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
+ Zusätzliche Ressourcen {#additional-resources}
   + [Versionshinweise](additional-resources/release-notes.md)

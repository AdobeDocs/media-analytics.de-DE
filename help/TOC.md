---
audience: end-user
user-guide-title: Adobe Analytics for Audio and Video
product: adobe analytics
sub-product: media analytics
translation-type: tm+mt
source-git-commit: ec98c87e31ce0265698d6da37a50c6d25d7155d3

---


# Adobe Analytics for Audio and Video {#using}

+ [Audio- und Videomessung in Adobe Analytics](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [Übersicht zu Milestone](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrieren von Meilensteinen zu Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migration von Milestone zu Custom Link](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Custom Link in Analytics {#cl-in-aa}
      + [Implementierungshandbuch für benutzerspezifische Links](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Einführung in Audio- und Videoanalysen {#intro-to-ava}
   + [Voraussetzungen](intro-to-ava/prereqs.md)
   + Implementierungspfade {#implementation-paths}
      + [Überblick](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Client-seitig](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Audience Manager-Aktivierung](intro-to-ava/am-enablement.md)
+ Media Analytics-SDK {#sdk-implement}
   + [SDKs herunterladen](sdk-implement/download-sdks.md)
   + Einrichtung und Konfiguration {#setup}
      + [Überblick](sdk-implement/setup/setup-overview.md)
      + [Android einrichten](sdk-implement/setup/set-up-android.md)
      + [Einrichten von iOS](sdk-implement/setup/set-up-ios.md)
      + [JavaScript einrichten](sdk-implement/setup/set-up-js.md)
      + [Einrichten von Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Roku einrichten](sdk-implement/setup/set-up-roku.md)
   + Tracking von Audio- und Videowiedergaben {#track-av-playback}
      + [Überblick](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [Core-Wiedergabe unter Android verfolgen](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Core-Wiedergabe unter iOS verfolgen](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Core-Wiedergabe auf JavaScript verfolgen](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Core-Wiedergabe auf Chromecast verfolgen](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Core-Wiedergabe auf Roku verfolgen](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [Nachverfolgen der Pufferung unter Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Nachverfolgen der Pufferung unter iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Pufferung auf JavaScript verfolgen](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Pufferung auf Chromecast verfolgen](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Pufferung auf Roku verfolgen](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [Suchen unter Android verfolgen](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Suchen unter iOS verfolgen](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Suche nach JavaScript verfolgen](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Suche nach Chromecast verfolgen](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Suche nach Roku verfolgen](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Standard-Metadaten implementieren {#impl-std-metadata}
         + [Standard-Metadaten in Android implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standard-Metadaten in iOS implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-Metadatenschlüssel](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Standard-Metadaten in JavaScript implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Standard-Metadaten in Chromecast implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standard-Metadatenparameter - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Standard-Metadaten in Roku implementieren](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standard-Metadatenparameter - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Anzeigen verfolgen {#track-ads}
      + [Überblick](sdk-implement/track-ads/track-ads-overview.md)
      + [Anzeigen unter Android verfolgen](sdk-implement/track-ads/track-ads-android.md)
      + [Anzeigen unter iOS verfolgen](sdk-implement/track-ads/track-ads-ios.md)
      + [Anzeigen auf JavaScript verfolgen](sdk-implement/track-ads/track-ads-js.md)
      + [Anzeigen auf Chromecast verfolgen](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Anzeigen auf Roku verfolgen](sdk-implement/track-ads/track-ads-roku.md)
      + Standard-Anzeigenmetadaten implementieren {#impl-std-ad-metadata}
         + [Standard-Anzeigenmetadaten in Android implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Standard-Anzeigenmetadaten in iOS implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Standard-Anzeigenmetadaten in JavaScript implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Standard-Anzeigenmetadaten in Roku implementieren](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Kapitel und Segmente verfolgen {#track-chapters}
      + [Überblick](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Kapitel und Segmente unter Android verfolgen](sdk-implement/track-chapters/track-chapters-android.md)
      + [Kapitel und Segmente unter iOS verfolgen](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Kapitel und Segmente auf JavaScript verfolgen](sdk-implement/track-chapters/track-chapters-js.md)
      + [Kapitel und Segmente auf Chromecast verfolgen](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Kapitel und Segmente nach Roku verfolgen](sdk-implement/track-chapters/track-chapters-roku.md)
   + Erlebnisqualität verfolgen {#track-qos}
      + [Überblick](sdk-implement/track-qos/track-qos-overview.md)
      + [Verfolgen der Qualität von Erlebnissen unter Android](sdk-implement/track-qos/track-qos-android.md)
      + [Verfolgen der Qualität von Erlebnissen unter iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Verfolgen der Qualität von Erfahrung mit JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Track Quality of Experience on Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Track Quality of Experience on Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [Überblick](sdk-implement/track-errors/track-errors-overview.md)
      + [Verfolgen von Fehlern unter Android](sdk-implement/track-errors/track-errors-android.md)
      + [Fehler unter iOS verfolgen](sdk-implement/track-errors/track-errors-ios.md)
      + [Fehler bei JavaScript verfolgen](sdk-implement/track-errors/track-errors-js.md)
      + [Verfolgen von Fehlern bei Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Fehler bei Roku verfolgen](sdk-implement/track-errors/track-errors-roku.md)
   + [Ausschluss und Datenschutz](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
      + [VOD-Wiedergabe ohne Anzeigen](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD-Wiedergabe mit Pre-Roll-Anzeigen](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
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
      + [Test 2: Medienunterbrechung](sdk-implement/validation/test2-media-interrupt.md)
      + [Details zu Testaufrufen](sdk-implement/validation/test-call-details.md)
      + [Beschreibungen der Heartbeat-Parameter](sdk-implement/validation/heartbeat-params.md)
      + Debugging {#debugging}
         + [SDK-Debugging](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Adobe Debug konfigurieren](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Neuen Debug-Bericht erstellen](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Debug-Dashboard und -Berichte](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [App-Zustände verfolgen](sdk-implement/analytics-with-ott/track-app-states.md)
      + [App-Aktionen verfolgen](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Benutzer-IDs festlegen](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT und Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT und Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Behandlung von Anwendungsunterbrechungen während der Wiedergabe](sdk-implement/cookbook/app-interrupts.md)
      + [Beheben von „main:play“ zwischen Anzeigen](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Wiederaufnehmen inaktiver Sitzungen](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracking in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [Migrationsübersicht](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Codevergleich: 1.x bis 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [API-Konversion von  1.x zu 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK to Launch Migration {#sdk-to-launch}
      + [SDK to Launch Migration](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Handbuch SDK zum Starten der Migrationsplattform {#sdk-to-launch-migration-platforms}
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
   + Media Tracking Timelines {#mc-api-timelines}
      + [Zeitlicher Ablauf 1: Wiedergabe bis zum Ende des Inhalts](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Zeitlicher Ablauf 2: Verlassen der Sitzung durch Anwender](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Zeitlicher Ablauf 3: Kapitel](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Heruntergeladene Inhalte verfolgen](media-collection-api/track-downloaded-content.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Medienstream-Zuordnung](media-analytics-cookbook/media-dimensions.md)
+ Metriken und Metadaten {#metrics-and-metadata}
   + [Audio- und Videoparameter](metrics-and-metadata/audio-video-parameters.md)
   + [Anzeigenparameter](metrics-and-metadata/ad-parameters.md)
   + [Kapitelparameter](metrics-and-metadata/chapter-parameters.md)
   + [Qualitätsparameter](metrics-and-metadata/quality-parameters.md)
   + [Segmente](metrics-and-metadata/segments.md)
   + [Berechnete Metriken](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [Aktivierung von Medienberichten](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [Übersicht über Standardberichte](media-reports/media-default-reports/default-reports-overview.md)
      + [Medien-Übersicht](media-reports/media-default-reports/media-reports-overview.md)
      + [Medien-Detail](media-reports/media-default-reports/media-reports-detail.md)
      + [Medien-Tagesbericht](media-reports/media-default-reports/media-reports-daypart.md)
      + [Gleichzeitige Medienbetrachter](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [JSON-Daten des Berichts „Gleichzeitige Videozuschauer“ abrufen](media-reports/media-default-reports/get-concurrent-json.md)
   + [Vorlagen für den Arbeitsbereich](media-reports/media-workspace-templates.md)
+ [Federated Analytics](federated-analytics.md)
+ Zusätzliche Ressourcen {#additional-resources}
   + [Ressourcen](additional-resources/doc-updates.md)

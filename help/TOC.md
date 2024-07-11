---
product: adobe analytics
audience: end-user
user-guide-title: Streaming Media Collection-Add-on
breadcrumb-title: Streaming Media Collection-Handbuch
user-guide-description: Implementieren von Streaming Media. Beinhaltet auch Informationen zum Media SDK und zur Media Collection API.
sub-product: media analytics
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 97%

---


# Streaming Media Collection-Add-on {#using}

+ [Streaming Media Collection-Handbuch](media-overview.md)
+ Versionshinweise {#release-notes}
   + [Versionshinweise zur Streaming-Mediensammlung](additional-resources/release-notes.md)
+ Erste Schritte {#getting-started}
   + [Voraussetzungen ](getting-started/prereqs.md)
   + [Unterstützte Geräte](getting-started/supported-devices.md)
   + [Dokumentation zur Implementierung der Streaming-Mediensammlung](getting-started/implementation-documentation.md)
   + [SDKs, Bibliotheken und Erweiterungen](getting-started/download-sdks.md)
   + Ende der Unterstützung {#end-of-support}
      + [Ende der Unterstützung für Media Analytics Mobile SDK](additional-resources/end-of-support-faqs.md)
      + Legacy − Migration vom eigenständigen Media SDK zu Launch {#sdk-to-launch}
         + [Überblick](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android − Media SDK zu Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS − Media SDK zu Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript − Media SDK zu Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementierung {#implementation}
   + [Implementierungsübersicht](implementation/overview.md)
   + Edge-Implementierungen (empfohlen) {#edge-recommended}
      + [Voraussetzungen ](/help/implementation/edge/prerequisites-edge.md)
      + Media Edge-SDKs/Erweiterung {#media-edge-sdk}
         + [Setup für Media Edge-SDKs/Erweiterung](/help/implementation/edge/implementation-edge.md)
         + [Media Edge Web SDK](/help/implementation/edge/edge-web-sdk.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge-API](/help/implementation/edge/implementation-edge-api.md)
   + Nur Adobe Analytics-Implementierungen {#analytics-only}
      + [Voraussetzungen ](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media-SDKs/Erweiterung {#media-sdk}
         + [JavaScript Web-SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics-Erweiterung](implementation/media-sdk/setup/web-implementation-tags.md)
         + [Mobile-SDKs](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT-SDKs {#ott-setup}
            + [Installieren des Chromecast SDK](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Installieren des Roku SDK](implementation/media-sdk/setup/set-up-roku.md)
      + Mediensammlungs-APIs − Implementierung {#streaming-media-apis}
         + [Mediensammlung](implementation/media-collection-api/mc-api-overview.md)
         + [API-Schnellstart](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Sitzungsanfrage](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Ereignisanfrage](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Anfrageparameter](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Ereignistypen und -beschreibungen](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + Implementieren der API {#mc-api-impl}
            + [Einstellen des HTTP-Anfragetyps in Ihrem Player](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Beziehen einer Sitzungs-ID](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Implementieren einer Ereignisanfrage](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON-Validierungsschemas](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Validieren von Ereignisanfragen](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Senden von Ping-Ereignissen](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [Senden von QoE-Daten](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Unterstützung benutzerspezifischer Metadaten](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Timeout-Bedingungen](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [Steuern der Ereignisreihenfolge](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variablen {#variables}
      + [Streaming Media-Parameter](implementation/variables/audio-video-parameters.md)
      + [Anzeigenparameter](implementation/variables/ad-parameters.md)
      + [Kapitelparameter](implementation/variables/chapter-parameters.md)
      + [Player-Statusparameter](implementation/variables/player-state-parameters.md)
      + [Qualitätsparameter](implementation/variables/quality-parameters.md)
      + [Berechnete Metriken ](implementation/variables/calculated-metrics.md)
+ Reporting {#media-reports}
   + [Aktivierung von Medienberichten ](reporting/media-reports-enable.md)
   + Medienbedienfelder in Workspace {#media-workspace-panels}
      + [Bedienfeld „Zielgruppendurchschnitt pro Minute“](reporting/workspace/average-minute-audience.md)
      + [Bedienfeld „Gleichzeitige Medienbetrachter“](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Panel „Verbrachte Zeit bei der Medienwiedergabe“](reporting/workspace/media-playback-time-spent.md)
   + [Medienberichte in Workspace](reporting/workspace/media-workspace-templates.md)
   + [Mediensegmente](reporting/segments.md)
   + Standardmedienberichte {#media-default-reports}
      + [Überblick über die Standardberichte](reporting/reports-and-analytics/default-reports-overview.md)
      + [Medienüberblick](reporting/reports-and-analytics/media-reports-overview.md)
      + [Mediendetails](reporting/reports-and-analytics/media-reports-detail.md)
      + [Medientagesbericht](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Bericht über gleichzeitige Medienbetrachtende](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Medien-API {#media-api}
      + [Abrufen von Daten über gleichzeitige Betrachtende](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [Abrufen der Daten zur mit der Medienwiedergabe verbrachten Zeit](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Nutzungsszenarios {#media-use-cases}
   + [Anwendungsfälle für Media SDK](use-cases/cookbook/sdk-cookbook-overview.md)
   + Player-Status-Tracking {#player-state-tracking}
      + [Überblick](use-cases/player-state-tracking/player-state-overview.md)
      + [Standardmäßige und benutzerdefinierte Status](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementierung und Reporting](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Statusverfolgung für mehrere Player](use-cases/player-state-tracking/multiple-player-states.md)
      + [Beispiele für Player-Status-Verfolgung](use-cases/player-state-tracking/player-state-examples.md)
   + [Tracking heruntergeladener Inhalte ](use-cases/track-downloaded-content.md)
   + [Federated Analytics ](use-cases/federated-analytics.md)
   + [Behandlung von Anwendungsunterbrechungen während der Wiedergabe](use-cases/cookbook/app-interrupts.md)
   + [Media Stream-Zuordnung](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Wiederaufnehmen von inaktiven Sitzungen](use-cases/cookbook/resuming-inactive.md)
   + [Roku-Tracking in SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Umgang mit Lücken zwischen Anzeigen](use-cases/cookbook/fix-ad-play-ad.md)
   + Timelines {#timelines}
      + [Kapitelstart und -ende](use-cases/timelines/chapter-start-end.md)
      + [Anzeigen zum Inhaltsende](use-cases/timelines/view-to-end-of-content.md)
      + [Sitzung beenden](use-cases/timelines/user-abandons-session.md)
   + Verwenden von Analytics in OTT-Apps {#analytics-with-ott}
      + [App-Zustände verfolgen](use-cases/analytics-with-ott/track-app-states.md)
      + [App-Aktionen verfolgen](use-cases/analytics-with-ott/track-app-actions.md)
      + [Festlegen von Benutzer-IDs](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT und Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT und Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Tracking {#tracking}
   + [Überblick](use-cases/track-av-playback/track-core-overview.md)
   + Tracking der Core-Wiedergabe von Streaming-Medien {#track-core}
      + [Tracking von Core-Wiedergaben in JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Tracking von Core-Wiedergaben in Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Tracking von Core-Wiedergaben in Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Puffer-Tracking {#track-buffering}
      + [Puffer-Tracking in JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Nachverfolgen der Pufferung auf Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Puffer-Tracking in Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Suchen-Tracking {#track-seeking}
      + [Suchen-Tracking in JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Nachverfolgen von Suchen auf Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Nachverfolgen von Suchen auf Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Standard-Metadaten implementieren {#impl-std-metadata}
      + [Standard-Metadaten in JavaScript 3.x implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Standard-Metadaten in Chromecast implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Standard-Metadatenparameter – Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Standard-Metadaten in Roku implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Standard-Metadatenparameter – Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Anzeigen verfolgen {#track-ads}
      + [Überblick](use-cases/track-ads/track-ads-overview.md)
      + [Tracking von Anzeigen in JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Nachverfolgen von Anzeigen auf Chromecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Nachverfolgen von Anzeigen auf Roku](use-cases/track-ads/track-ads-roku.md)
      + Standard-Anzeigenmetadaten implementieren {#impl-std-ad-metadata}
         + [Standard-Anzeigenmetadaten in JavaScript 3.x implementieren](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Standard-Anzeigenmetadaten in Roku implementieren](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Kapitel und Segmente verfolgen {#track-chapters}
      + [Überblick](use-cases/track-chapters/track-chapters-overview.md)
      + [Tracking von Kapiteln und Segmenten in JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Nachverfolgen von Kapiteln und Segmenten auf Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Nachverfolgen von Kapiteln und Segmenten auf Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Erlebnisqualität verfolgen {#track-qos}
      + [Überblick](use-cases/track-qos/track-qos-overview.md)
      + [Tracking der Erlebnisqualität in JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Tracking der Erlebnisqualität in Chromecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Nachverfolgen der Erlebnisqualität auf Roku](use-cases/track-qos/track-qos-roku.md)
   + Fehler-Tracking {#track-errors}
      + [Überblick](use-cases/track-errors/track-errors-overview.md)
      + [Tracking von Fehlern in JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Nachverfolgen von Fehlern auf Chromecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Tracking von Fehlern in Roku](use-cases/track-errors/track-errors-roku.md)
+ Datenschutz und Sicherheit {#streaming-media-privacy}
   + [Opt-out- und Datenschutz-Einstellungen](privacy/opt-out-privacy.md)
   + [Sicherheit](privacy/security.md)
+ Legacy-Implementierungen {#legacy-implementations}
   + [Legacy − Übersicht](legacy/setup/legacy-setup-overview.md)
   + [Legacy − SDKs herunterladen](legacy/legacy-download-sdks.md)
   + Legacy − Medien-SDKs {#legacy-media-sdks}
      + [Legacy − Media SDK – Übersicht](legacy/media-sdk/setup/setup-overview.md)
      + [Android einrichten](legacy/media-sdk/setup/set-up-android.md)
      + [Einrichten von iOS](legacy/media-sdk/setup/set-up-ios.md)
      + JavaScript einrichten {#setup-javascript}
         + [Einrichten von JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Über Heartbeat-Messungen](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Aktivierung von Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
   + [Implementierung benutzerdefinierter Links](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Veraltete Milestone-Verfolgung {#legacy-milestone-tracking}
      + [Veraltete Milestone-Verfolgung](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrieren von Milestone zu VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrieren von Milestone zu CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validierung {#validation}
      + [Validierungsübersicht](legacy/validation/validation-overview.md)
      + [Test 1: Standardwiedergabe](legacy/validation/test1-standard-playback.md)
      + [Test 2: Medienunterbrechung](legacy/validation/test2-media-interrupt.md)
      + [Details zum Testaufruf](legacy/validation/test-call-details.md)
      + [Beschreibungen der Heartbeat-Parameter](legacy/validation/heartbeat-params.md)
      + Debugging {#debugging}
         + [SDK-Debugging](legacy/validation/debugging/sdk-debugging.md)
   + [Legacy-Migration: VHL 1.x zu VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Code-Vergleich von v1.x mit v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [Tracking-APIs 1x bis 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Legacy − Einführung in AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Client-seitiger Pfad](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Legacy-Tracking {#track-av-playback}
      + [Nachverfolgen der grundlegenden Wiedergabe auf Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Nachverfolgen der grundlegenden Wiedergabe auf iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Tracking von Core-Wiedergaben in JavaScript {#track-core-javascript}
         + [Tracking von Core-Wiedergaben in JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Nachverfolgen der Pufferung auf Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Nachverfolgen der Pufferung auf iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Puffer-Tracking in JavaScript {#track-buffering-js}
            + [Puffer-Tracking in JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Nachverfolgen von Suchen auf Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Nachverfolgen von Suchen auf iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Suchen-Tracking in JavaScript {#track-seeking-js}
            + [Suchen-Tracking in JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Standard-Metadaten in Android implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standard-Metadaten in iOS implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-Metadatenschlüssel](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Standard-Metadaten in JavaScript implementieren {#impl-std-md-js}
            + [Standard-Metadaten in JavaScript 2.x implementieren](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Anzeigen nachverfolgen {#track-ads}
         + [Nachverfolgen von Anzeigen auf Android](use-cases/track-ads/track-ads-android.md)
         + [Nachverfolgen von Anzeigen auf iOS](use-cases/track-ads/track-ads-ios.md)
         + Tracking von Anzeigen in JavaScript {#track-ads-js}
            + [Tracking von Anzeigen in JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Standardmäßige Anzeigenmetadaten in Android implementieren](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Standard-Anzeigenmetadaten in iOS implementieren](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Standard-Anzeigenmetadaten in JavaScript implementieren {#impl-std-ad-md-js}
               + [Standard-Anzeigenmetadaten in JavaScript 2.x implementieren](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Kapitel und Segmente nachverfolgen {#track-chapters}
         + [Tracking von Kapiteln und Segmenten in Android](use-cases/track-chapters/track-chapters-android.md)
         + [Nachverfolgen von Kapiteln und Segmenten auf iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Tracking von Kapiteln und Segmenten in JavaScript {#track-chapters-js}
            + [Tracking von Kapiteln und Segmenten in JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Tracking der Erlebnisqualität in Android](use-cases/track-qos/track-qos-android.md)
         + [Nachverfolgen der Erlebnisqualität auf iOS](use-cases/track-qos/track-qos-ios.md)
         + Tracking der Erlebnisqualität in JavaScript {#track-qos-js}
            + [Tracking der Erlebnisqualität in JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Fehler nachverfolgen {#track-errors}
         + [Tracking von Fehlern in Android](use-cases/track-errors/track-errors-android.md)
         + [Tracking von Fehlern in iOS](use-cases/track-errors/track-errors-ios.md)
         + Tracking von Fehlern in JavaScript {#track-errors-js}
            + [Tracking von Fehlern in JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Tracking-Szenarien {#tracking-scenarios}
         + [VOD-Wiedergabe ohne Anzeigen](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [VOD-Wiedergabe mit Pre-roll-Anzeigen](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [VOD-Wiedergabe mit übersprungenen Anzeigen](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [VOD-Wiedergabe mit einem Kapitel](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [VOD-Wiedergabe mit einem übersprungenen Kapitel](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [VOD-Wiedergabe mit Suche im Hauptinhalt](use-cases/tracking-scenarios/vod-seeking.md)
         + [VOD-Wiedergabe mit Pufferung](use-cases/tracking-scenarios/vod-buffering.md)
         + [Mehrere parallele VOD-Tracker](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [Ein VOD-Tracker für mehrere Sitzungen](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Live-Hauptinhalt ](use-cases/tracking-scenarios/live-main-content.md)
         + [Live-Hauptinhalt mit sequentieller Verfolgung](use-cases/tracking-scenarios/live-sequential.md)

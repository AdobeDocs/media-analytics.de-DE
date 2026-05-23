---
title: Berechnete Metriken
description: Benutzerdefinierte berechnete Metriken für Berichte zu Streaming-Medien in Adobe Analytics und Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: 1251b66173158b8fea92516197b3b9f444bfaaf7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# Berechnete Metriken

Berechnete Metriken für Adobe-Streaming-Mediendienste sind benutzerdefinierte Metriken, die auf der Grundlage der standardmäßigen Streaming-Medienmetriken erstellt werden. So können Sie Verhältnisse wie durchschnittliche Anzeigenbesuchszeit oder Medienabschlussrate ableiten, ohne die Implementierung zu ändern.

Informationen zum Erstellen dieser berechneten Metriken in Analysis Workspace finden Sie in der entsprechenden Übersicht über berechnete Metriken in [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) oder [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Berechnete Metrik | Beschreibung | Formel |
| --- | --- | --- |
| Durchschnittl. Anzeigen pro Medien-Stream | Anzeigenstarts pro Medienstart | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Durchschnittl. Kapitel pro Medien-Stream | Kapitelstarts pro Medienstart | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Durchschnittl. Besuchszeit für Medien | Gesamtbesuchszeit pro Medienstart (`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Durchschnittl. Besuchszeit für Inhalt | Besuchszeit für den Inhalt nach gestarteten Inhalten (`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Durchschnittl. Besuchszeit für die Anzeige | Besuchszeit für die Anzeige pro gestarteter Anzeige (`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Durchschnittl. Besuchszeit für das Kapitel | Besuchszeit für das Kapitel pro gestartetem Kapitel (`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Abschlussrate der Medien | Anteil abgeschlossener Inhalte und initiierter Medien im Vergleich | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Abschlussrate des Inhalts | Anteil abgeschlossener Inhalte und gestarteter Inhalte im Vergleich | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Abschlussrate der Anzeige | Anteil abgeschlossener Anzeigen und gestarteter Anzeigen im Vergleich | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Abschlussrate des Kapitels | Anteil abgeschlossener Kapitel und gestarteter Kapitel im Vergleich | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Vor Start ablegen | Drop-Rate vor Start und Medienstart im Vergleich | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Rate der Inhaltspausen | Rate der Pausengesamtdauer im Vergleich zur Besuchszeit für den Inhalt | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Dauer des Inhaltspuffers | Rate der Puffergesamtdauer im Vergleich zur Besuchszeit für den Inhalt | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Rate der Zeit bis zum Start des Inhalts | Rate der zu startenden Zeit im Vergleich zur Besuchszeit für den Inhalt | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Besuchsrate für Anzeige | Rate der Besuchszeit für Anzeigen und der Besuchszeit für Inhalte im Vergleich | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |


---
title: Berechnete Metriken
description: Benutzerdefinierte berechnete Metriken für Berichte zu Streaming-Medien in Adobe Analytics und Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# Berechnete Metriken

Berechnete Metriken für Adobe-Streaming-Mediendienste sind benutzerdefinierte Metriken, die auf der Grundlage der standardmäßigen Streaming-Medienmetriken erstellt werden. So können Sie Verhältnisse wie durchschnittliche Anzeigenbesuchszeit oder Medienabschlussrate ableiten, ohne die Implementierung zu ändern.

Informationen zum Erstellen dieser berechneten Metriken in Analysis Workspace finden Sie in der entsprechenden Übersicht über berechnete Metriken in [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) oder [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Berechnete Metrik | Beschreibung | Formel |
| --- | --- | --- |
| Durchschnittl. Anzeigen pro Medien-Stream | [[!UICONTROL Anzeigenstarts]](/help/reporting/metrics/ad-starts.md) pro [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| Durchschnittl. Kapitel pro Medien-Stream | [[!UICONTROL Kapitelstarts]](/help/reporting/metrics/chapter-starts.md) pro [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| Durchschnittl. Besuchszeit für Medien | [[!UICONTROL Besuchszeit für Medien]](/help/reporting/metrics/media-time-spent.md) pro [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| Durchschnittl. Besuchszeit für Inhalt | [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md) pro [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| Durchschnittl. Besuchszeit für die Anzeige | [[!UICONTROL Besuchszeit für die Anzeige]](/help/reporting/metrics/ad-time-spent.md) pro [[!UICONTROL Anzeigenstart]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| Durchschnittl. Besuchszeit für das Kapitel | [[!UICONTROL Besuchszeit für Kapitel]](/help/reporting/metrics/chapter-time-spent.md) pro [[!UICONTROL Kapitelstart]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| Abschlussrate der Medien | Rate [[!UICONTROL Abgeschlossene Inhalte]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| Abschlussrate des Inhalts | Rate [[!UICONTROL Abgeschlossene Inhalte]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| Abschlussrate der Anzeige | Rate von [[!UICONTROL Abgeschlossene Anzeige]](/help/reporting/metrics/ad-completes.md) im Vergleich zu [[!UICONTROL gestarteten Anzeige]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| Abschlussrate des Kapitels | Rate von [[!UICONTROL Kapitelabschlüsse]](/help/reporting/metrics/chapter-completes.md) vs. [[!UICONTROL Kapitelstarts]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| Vor Start ablegen | Rate der [[!UICONTROL Drops vor dem Start]](/help/reporting/metrics/drops-before-start.md) im Vergleich zu [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| Rate der Inhaltspausen | Rate der [[!UICONTROL Pausierung insgesamt]](/help/reporting/metrics/total-pause-duration.md) im Vergleich zu [[!UICONTROL Besuchszeit für Inhalte]](/help/reporting/metrics/content-time-spent.md) | `[Total pause duration] / [Content time spent]` |
| Dauer des Inhaltspuffers | Rate [[!UICONTROL Puffergesamtdauer]](/help/reporting/metrics/total-buffer-duration.md) vs. [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md) | `[Total buffer duration] / [Content time spent]` |
| Rate der Zeit bis zum Start des Inhalts | Rate [[!UICONTROL Zeit bis zum Start]](/help/reporting/metrics/time-to-start.md) vs. [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md) | `[Time to start] / [Content time spent]` |
| Besuchsrate für Anzeige | Rate der [[!UICONTROL Besuchszeit für Anzeigen]](/help/reporting/metrics/ad-time-spent.md) im Vergleich zu [[!UICONTROL Besuchszeit für Inhalte]](/help/reporting/metrics/content-time-spent.md) | `[Ad time spent] / [Content time spent]` |


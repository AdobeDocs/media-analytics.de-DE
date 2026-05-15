---
title: Zielgruppendurchschnitt pro Minute
description: Gibt die durchschnittliche Anzahl der Betrachter an, die eine Minute lang über die Laufzeit des Inhalts hinweg zuschauen.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# Zielgruppendurchschnitt pro Minute

Die Metrik **Zielgruppendurchschnitt pro Minute** gibt die durchschnittliche Anzahl der Betrachter an, die während der Laufzeit des Inhalts eine bestimmte Minute lang zuschauen. Dies ist die standardmäßige „AMA“-Messung, mit der die Reichweite von Medien über verschiedene Längen hinweg verglichen wird.

## Berechnung dieser Metrik

Das Medien-Backend berechnet den Zielgruppendurchschnitt pro Minute pro Sitzung nach `Content time spent / Content length`. In der Summe aller Sitzungen wird die durchschnittliche Zielgruppengröße pro Minute des Inhalts dargestellt. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.averageMinuteAudience`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>Der Zielgruppendurchschnitt pro Minute erfordert eine [&#x200B; (Inhaltslänge](/help/reporting/dimensions/content-length.md). Wenn die Inhaltslänge auf null oder nicht festgelegt ist, wird diese Metrik für die Sitzung nicht erzeugt.

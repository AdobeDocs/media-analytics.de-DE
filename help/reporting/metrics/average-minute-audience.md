---
title: Zielgruppendurchschnitt pro Minute
description: Gibt die durchschnittliche Anzahl der Betrachter an, die eine Minute lang über die Laufzeit des Inhalts hinweg zuschauen.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.averageMinuteAudience`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>Der Zielgruppendurchschnitt pro Minute erfordert eine [&#x200B; (Inhaltslänge](/help/reporting/dimensions/content-length.md). Wenn die Inhaltslänge auf null oder nicht festgelegt ist, wird diese Metrik für die Sitzung nicht erzeugt.

---
title: Federated Data
description: Zählt Sitzungen, die über eine Federated Data Share statt über die eigene Implementierung eines Kunden empfangen wurden.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Federated Data

>[!AVAILABILITY]
>
>Der Federated Analytics-Service ist nur verfügbar, wenn Streaming-Medienfunktionen mit Adobe Analytics verwendet werden. Federated Analytics ist in Customer Journey Analytics nicht verfügbar.

Die **Federated Data**-Metrik zählt Sitzungen, die über eine Federated Data Share und nicht von Ihrer eigenen Implementierung empfangen wurden. Verwenden Sie diese Option, um das Volumen der von Partnern freigegebenen Sitzungen zu messen und Interaktion, Abschluss oder Qualität mit Erstanbieter-Sitzungen zu vergleichen.

Weitere Informationen finden Sie [&#x200B; Anwendungsfall &#x200B;](/help/use-cases/federated-media.md)Federated Media) .

>[!TIP]
>
>Wenn Sie Federated Data als Dimension verwenden möchten, erstellen Sie eine [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die die `a.media.federated` Kontextdatenvariable einer eVar zuordnet.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn die Sitzung über einen Federated Channel eingeht. Die Metrik wird einmal pro qualifizierter Sitzung inkrementiert und beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.federated`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.federated` |

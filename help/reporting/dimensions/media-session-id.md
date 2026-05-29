---
title: Mediensitzungs-ID
description: Identifiziert jede Wiedergabesitzung eindeutig.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# Mediensitzungs-ID

Die Dimension **Mediensitzungs-ID** identifiziert jede Wiedergabesitzung eindeutig. Er wird vom Backend generiert und bei jedem Ereignis für die Sitzung gestempelt. Verwenden Sie diese Option, um die Ereignisse einer einzelnen Sitzung zum Debugging zu isolieren oder Sitzungen in benutzerdefinierten Analysen zu deduplizieren.

## So wird diese Dimension ausgefüllt

Die Sitzungs-ID wird automatisch generiert, wenn das Backend ein &quot;[&quot;-](/help/implementation/events/session/session-start.md) erhält. Implementierungen von Web SDK und Mobile SDK erfassen und speichern die ID für Sie. Bei direkten API-Implementierungen muss die Sitzungs-ID aus der `sessionStart`-Antwort gelesen (der `Location`-Header für die Mediensammlungs-API oder das `media-analytics:new-session`-Handle für die Media Edge-API) und bei nachfolgenden Ereignissen eingeschlossen werden.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.vsid` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Dimensionselemente

Jedes Element ist eine eindeutige Sitzungs-ID, die vom Backend generiert wird (normalerweise eine 22-stellige alphanumerische Zeichenfolge). Verwenden Sie das Filter- oder Suchfeld, um eine bestimmte Sitzung nachzuschlagen.

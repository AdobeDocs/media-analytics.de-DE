---
title: Mediensitzungs-ID
description: Identifiziert jede Wiedergabesitzung eindeutig.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 6%
---

# Mediensitzungs-ID

Die Dimension **Mediensitzungs-ID** identifiziert jede Wiedergabesitzung eindeutig. Er wird vom Backend generiert und bei jedem Ereignis für die Sitzung gestempelt. Verwenden Sie diese Option, um die Ereignisse einer einzelnen Sitzung zum Debugging zu isolieren oder Sitzungen in benutzerdefinierten Analysen zu deduplizieren.

## So wird diese Dimension ausgefüllt

Die Sitzungs-ID wird automatisch generiert, wenn das Backend ein &quot;[&quot;-](/help/implementation/events/session/session-start.md) erhält. Implementierungen von Web SDK und Mobile SDK erfassen und speichern die ID für Sie. Bei direkten API-Implementierungen muss die Sitzungs-ID aus der `sessionStart`-Antwort gelesen (der `Location`-Header für die Mediensammlungs-API oder das `media-analytics:new-session`-Handle für die Media Edge-API) und bei nachfolgenden Ereignissen eingeschlossen werden.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.vsid` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Dimensionselemente

Jedes Element ist eine eindeutige Sitzungs-ID, die vom Backend generiert wird (normalerweise eine 22-stellige alphanumerische Zeichenfolge). Verwenden Sie das Filter- oder Suchfeld, um eine bestimmte Sitzung nachzuschlagen.

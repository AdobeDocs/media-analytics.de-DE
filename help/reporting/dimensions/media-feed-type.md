---
title: Medien-Feed-Typ
description: Meldet den Broadcast-Feed (z. B. East-HD oder West-SD), wenn derselbe Inhalt über mehrere Feeds bereitgestellt wird.
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
source-wordcount: '159'
ht-degree: 8%
---

# Medien-Feed-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Medien-Feed-Typ**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/standard-metadata/media-feed-type.md)Medien-Feed-Typ)*

>[!ENDSHADEBOX]

Die Dimension **Medien-Feed** Typ) zeigt den Broadcast-Feed für jede Sitzung an (z. B. `"East-HD"`, `"West-SD"` oder `"4K"`). Verwenden Sie sie, wenn derselbe Inhalt über mehrere regionale oder hochwertige Feeds bereitgestellt wird und Interaktion pro Feed gemeldet werden muss.

## So wird diese Dimension ausgefüllt

Der Medien-Feed-Typ wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.feed`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Dimensionselemente

Jedes Element ist der literale Feed-Wert, der beim Sitzungsstart gemeldet wird. Verwenden Sie einen stabilen Satz von Feed-Kennungen pro regionaler oder Qualitätsteilung.

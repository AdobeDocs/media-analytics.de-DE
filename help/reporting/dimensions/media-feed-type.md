---
title: Medien-Feed-Typ
description: Meldet den Broadcast-Feed (z. B. East-HD oder West-SD), wenn derselbe Inhalt über mehrere Feeds bereitgestellt wird.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.feed`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Dimensionselemente

Jedes Element ist der literale Feed-Wert, der beim Sitzungsstart gemeldet wird. Verwenden Sie einen stabilen Satz von Feed-Kennungen pro regionaler oder Qualitätsteilung.

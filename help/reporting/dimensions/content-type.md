---
title: Content-Typ
description: Gibt das Format des Streams an (VOD, Live, Linear, Podcast, Song usw.).
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# Content-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltstyp**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/content-type.md) unter „Content-Typ“*

>[!ENDSHADEBOX]

Die Dimension **Content** gibt das Format des Streams an (z. B. VOD, Live oder Linear für Video und Song, Podcast oder Hörbuch für Audio).

## So wird diese Dimension ausgefüllt

Der Inhaltstyp wird vom Player beim Sitzungsstart festgelegt und bei jedem Ereignis angewendet. Es wird nicht abgeleitet. Der gemeldete Wert entspricht dem, was während der Erfassung gesendet wurde.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.contentType`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>Wenn der Inhaltstyp nicht festgelegt oder leer ist, meldet die Dimension `missing_content_type` für die Sitzung. Verwenden Sie diesen Wert, um Implementierungen zu finden, die korrigiert werden müssen.

## Dimensionselemente

Von Adobe definierte Werte füllen die integrierten Segmente und Berichte aus. Benutzerdefinierte Zeichenfolgen werden akzeptiert, stimmen jedoch nicht mit den integrierten Segmenten überein.

| Stream-Typ | Empfohlene Werte |
| --- | --- |
| Video | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Audio | `song`, `podcast`, `audiobook`, `radio` |

## Empfohlene Segmente

| Segment | Regel |
| --- | --- |
| [!UICONTROL VOD-Inhalte] | Content-Typ = `vod` |
| [!UICONTROL Live-Inhalt] | Content-Typ = `live` |
| [!UICONTROL Linearer Inhalt] | Content-Typ = `linear` |

---
title: Inhaltstyp
description: Gibt das Format des Streams an (VOD, Live, Linear, Podcast, Song usw.).
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
source-wordcount: '210'
ht-degree: 15%
---

# Inhaltstyp

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltstyp**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/content-type.md) unter „Content-Typ“*

>[!ENDSHADEBOX]

Die Dimension **Content** gibt das Format des Streams an (z. B. VOD, Live oder Linear für Video und Song, Podcast oder Hörbuch für Audio).

## So wird diese Dimension ausgefüllt

Der Inhaltstyp wird vom Player beim Sitzungsstart festgelegt und bei jedem Ereignis angewendet. Es wird nicht abgeleitet. Der gemeldete Wert entspricht dem, was während der Erfassung gesendet wurde.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.contentType`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
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

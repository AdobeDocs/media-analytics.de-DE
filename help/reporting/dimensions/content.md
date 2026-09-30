---
title: Inhalt
description: Meldet jedes einzelne abgespielte Medium, verschlüsselt nach der Inhalts-ID.
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
source-wordcount: '251'
ht-degree: 7%
---

# Inhalt

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting **Dimension „Inhalt**&#x200B;behandelt. Unter [Inhalts-ID](/help/implementation/variables/core/content-id.md) finden Sie Informationen zum Erfassen dieser Variablen.*

>[!ENDSHADEBOX]

Die Dimension **Inhalt** zeigt jedes einzelne abgespielte Medium an, das durch die bei Sitzungsbeginn festgelegte Inhalts-ID verschlüsselt wird. Dies ist die primäre Aufschlüsselung für das Reporting über Streaming-Medien und der Join-Schlüssel für Klassifizierungsdimensionen wie Videoname, Videolänge, Asset-ID, Erstausstrahlungsdatum und Inhaltsbewertung.

## So wird diese Dimension ausgefüllt

Inhalte werden vom Player beim Sitzungsstart als stabile Kennung für das Asset festgelegt. Dieselbe Inhalts-ID wird bei jedem nachfolgenden Ereignis für die Sitzung gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.name`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. bleibt für die Dauer des Besuchs erhalten. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>Inhalts-ID ist erforderlich. Wenn sie nicht festgelegt oder leer ist, wird die Sitzung aus der Streaming-Medienberichterstattung entfernt und wird in keinem Medienbericht und auch nicht im Segment [!UICONTROL Alle Streaming] angezeigt.

## Dimensionselemente

Jedes Element ist eine eindeutige Inhalts-ID, die beim Sitzungsstart gemeldet wird. Verwenden Sie eine stabile Kennung (z. B. eine interne CMS-ID, eine Branchen-ID wie EIDR oder TMS/Gracenote oder einen beständigen Slug), damit Sitzungen für dasselbe Asset im Laufe der Zeit zu einem einzigen Zeileneintrag zusammengeführt werden.

## Empfohlene Segmente

| Segment | Regel |
| --- | --- |
| [!UICONTROL Alle Streaming-Medien] | Content (ID) exists |

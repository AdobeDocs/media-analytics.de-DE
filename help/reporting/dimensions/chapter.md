---
title: Kapitel
description: Meldet jedes einzelne abgespielte Kapitel basierend auf einer automatisch generierten Kapitel-ID.
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
source-wordcount: '196'
ht-degree: 9%
---

# Kapitel

Die Dimension **Chapter** zeigt jedes einzelne gespielte Kapitel an, das durch eine automatisch generierte Kapitel-ID verschlüsselt wird. Die ID wird vom SDK oder Backend aus der Inhalts-ID, dem Kapitelindex und der Kapitelstartzeit erstellt, sodass zwei Sitzungen desselben Kapitels mit demselben Inhalt zu einem einzigen Zeileneintrag zusammengeführt werden. Verwenden Sie die Dimension als Zusammenführungsschlüssel für Klassifizierungen auf Kapitelebene wie Kapitelname, Kapitellänge, Kapitelversatz und Kapitelposition.

## So wird diese Dimension ausgefüllt

Die Kapitel-ID wird automatisch generiert, wenn ein [Kapitelstart](/help/implementation/events/chapters/chapter-start.md)-Ereignis ausgelöst wird. Der Wert wird nicht direkt festgelegt, sondern von der Kapitelposition, dem Versatz und der Inhalts-ID abgeleitet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.name`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `videochapter`, `post_videochapter` |
| Audience Manager | nicht angegeben |

## Dimensionselemente

Jedes Element ist eine eindeutige Kapitel-ID. Die ID ist undurchsichtig (normalerweise ein Hash der Inhalts-ID + Index + Offset) und eignet sich am besten als Gruppierungsschlüssel. Paar mit [Kapitelname](chapter-name.md) für eine benutzerfreundliche Beschriftung.

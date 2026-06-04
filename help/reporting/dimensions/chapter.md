---
title: Kapitel
description: Meldet jedes einzelne abgespielte Kapitel basierend auf einer automatisch generierten Kapitel-ID.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 8%

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

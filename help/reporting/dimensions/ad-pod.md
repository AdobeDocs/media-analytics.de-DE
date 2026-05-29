---
title: Anzeigen-Pod
description: Meldet jede einzelne Werbeunterbrechung, verschlüsselt durch eine automatisch generierte Pod-ID.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# Anzeigen-Pod

Die Dimension **Anzeigen-Pod** zeigt jede einzelne Werbeunterbrechung an, die durch eine automatisch generierte Pod-ID verschlüsselt ist. Jede Anzeige in einer Sitzung gehört zu einem übergeordneten Anzeigen-Pod, und der Pod gruppiert mehrere Anzeigen, die hintereinander abgespielt werden. Verwenden Sie die Dimension, um die Interaktion durch Anzeigenunterbrechung und als Join-Schlüssel für die Klassifizierungen [Pod-Name](pod-name.md) und [Pod-Position](pod-position.md) zu unterbrechen.

## So wird diese Dimension ausgefüllt

Die ID des Anzeigen-Pods wird automatisch von SDK generiert, wenn ein [Start der Werbeunterbrechung](/help/implementation/events/ads/ad-break-start.md) ausgelöst wird. Bei direkten API-Implementierungen wird der Index aus dem Unterbrechungsindex und der Startzeit erstellt oder eine benutzerdefinierte Pod-ID bereitgestellt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.pod`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Daten-Feeds | `videoadpod`, `post_videoadpod` |
| Audience Manager | nicht angegeben |

## Dimensionselemente

Jedes Element ist eine eindeutige Werbe-Pod-ID. Die ID ist undurchsichtig (normalerweise ein Hash aus Sitzungs-ID, Inhalts-ID und Breakindex) und ist am nützlichsten als Gruppierungsschlüssel, wenn er mit [Pod-Name](pod-name.md) für die benutzerfreundliche Beschriftung kombiniert wird.

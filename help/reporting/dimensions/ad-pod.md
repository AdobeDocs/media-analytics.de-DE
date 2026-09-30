---
title: Anzeigen-Pod
description: Meldet jede einzelne Werbeunterbrechung, verschlüsselt durch eine automatisch generierte Pod-ID.
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
source-wordcount: '197'
ht-degree: 8%
---

# Anzeigen-Pod

Die Dimension **Anzeigen-Pod** zeigt jede einzelne Werbeunterbrechung an, die durch eine automatisch generierte Pod-ID verschlüsselt ist. Jede Anzeige in einer Sitzung gehört zu einem übergeordneten Anzeigen-Pod, und der Pod gruppiert mehrere Anzeigen, die hintereinander abgespielt werden. Verwenden Sie die Dimension, um die Interaktion durch Anzeigenunterbrechung und als Join-Schlüssel für die Klassifizierungen [Pod-Name](pod-name.md) und [Pod-Position](pod-position.md) zu unterbrechen.

## So wird diese Dimension ausgefüllt

Die ID des Anzeigen-Pods wird automatisch von SDK generiert, wenn ein [Start der Werbeunterbrechung](/help/implementation/events/ads/ad-break-start.md) ausgelöst wird. Bei direkten API-Implementierungen wird der Index aus dem Unterbrechungsindex und der Startzeit erstellt oder eine benutzerdefinierte Pod-ID bereitgestellt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.pod`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Daten-Feeds | `videoadpod`, `post_videoadpod` |
| Audience Manager | nicht angegeben |

## Dimensionselemente

Jedes Element ist eine eindeutige Werbe-Pod-ID. Die ID ist undurchsichtig (normalerweise ein Hash aus Sitzungs-ID, Inhalts-ID und Breakindex) und ist am nützlichsten als Gruppierungsschlüssel, wenn er mit [Pod-Name](pod-name.md) für die benutzerfreundliche Beschriftung kombiniert wird.

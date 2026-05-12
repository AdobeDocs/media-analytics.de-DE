---
title: Pod-Name
description: Gibt den Anzeigenamen jeder Werbeunterbrechung an. Sie können sie in Adobe Analytics mithilfe einer Klassifizierung oder einer benutzerdefinierten Verarbeitungsregel erfassen.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Pod-Name

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Pod-Name**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-break-name.md) unter „Anzeigenumbruch-Name“*

>[!ENDSHADEBOX]

Die Dimension **Pod-Name** zeigt den Anzeigenamen jeder Werbeunterbrechung an (z. B. `"pre-roll"`, `"mid-roll-1"`). In Customer Journey Analytics handelt es sich um eine diskrete Dimension, die direkt aus der Implementierungsvariablen ausgefüllt wird. In Adobe Analytics ist sie über zwei Ansätze verfügbar: eine Klassifizierung der Dimension [Ad Pod](ad-pod.md) oder eine eVar, die mithilfe einer Verarbeitungsregel ausgefüllt wird.

## So wird diese Dimension ausgefüllt

Der Pod-Name stammt aus dem Wert [Name der Werbeunterbrechung](/help/implementation/variables/ads/ad-break-name.md), den der Player für `media.adBreakStart` festlegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.podFriendlyName` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Ad-Pod-Dimension - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.podFriendlyName` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |

## Klassifizierungsansatz

Adobe erstellt die Pod-Namensklassifizierungsstruktur automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Pod-ID und ihrem Anzeigenamen. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Pod-Namen für die Klassifizierung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.podFriendlyName` einer eVar zuordnet. Dieser Ansatz erfasst den Anzeigenamen als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen dem Pod-Namen und der übergeordneten Dimension [Ad Pod](ad-pod.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Pod-ID über Ereignisse hinweg sendet, können mehrere Namen unter demselben Anzeigen-Pod angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der literale Anzeigenunterbrechungsname, der für `media.adBreakStart` gemeldet wird.

---
title: Zeit bis zum Start (Dimension)
description: Gibt die Zeit an, die vor dem ersten gerenderten Frame verstrichen ist.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---


# Zeit bis zum Start (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Zeit bis zum Start**&#x200B;behandelt. Adobe Analytics füllt automatisch eine paarweise [Time to Start (Metrik](/help/reporting/metrics/time-to-start.md) aus derselben `a.media.qoe.timeToStart` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.timeToStart` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/quality/time-to-start.md) „Zeit bis zum Start“*

>[!ENDSHADEBOX]

Die Dimension **Zeit bis**&quot; zeigt die Zeit zwischen dem Sitzungsstart und dem ersten Frame-Rendering an. Verwenden Sie die Dimension, um die Interaktion nach Startzeit-Bucket aufzuheben. Adobe speichert den Wert in Sekunden und konvertiert bei der Aufnahme die Millisekunden, die der Player meldet.

## So wird diese Dimension ausgefüllt

Der Player legt `timeToStart` auf das QoE-Objekt fest, bevor der Sitzungsstart ausgelöst wird. Das Backend meldet den Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.timeToStart`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Wert der Startzeit.

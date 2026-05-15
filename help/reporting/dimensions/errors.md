---
title: Fehler
description: Gibt die Anzahl der Fehlerereignisse pro Sitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# Fehler

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Fehler**behandelt. Adobe Analytics füllt automatisch eine gepaarte [Fehlerereignismetrik](/help/reporting/metrics/error-events.md) aus derselben `a.media.qoe.errorCount` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.errorCount` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Dimension **Fehler** zeigt die Anzahl der Fehlerereignisse an, die während einer Sitzung empfangen wurden. Verwenden Sie die Dimension, um die Interaktion anhand der genauen Fehleranzahl aufzuheben.

## So wird diese Dimension ausgefüllt

Das Medien-Backend erhöht die Anzahl bei jedem vom Player gemeldeten Fehler. Der Wert wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.errorCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## Dimensionselemente

Jedes Element ist der literale Wert für die Fehleranzahl, der beim Schließen-Aufruf gemeldet wird. Verwenden Sie für das boolesche Reporting auf Sitzungsebene (ob überhaupt ein Fehler aufgetreten ist) [Streams mit Auswirkung auf Fehler](/help/reporting/metrics/error-impacted-streams.md). Verwenden Sie für eindeutige Fehler-IDs [externe Fehler-IDs](external-error-ids.md) und [Player-SDK-Fehler-IDs](player-sdk-error-ids.md).

>[!NOTE]
>
>Wenn Sie die veraltete Heartbeat-SDK (Media SDK 1.5.x-2.x) verwenden, werden intern von der SDK generierte Fehler-IDs automatisch unter dem Kontextdatenschlüssel `a.media.qoe.mediaSdkErrors` erfasst und können in Adobe Analytics über eine benutzerdefinierte Verarbeitungsregel aufgerufen werden. Die Audience Manager-Eigenschaft ist `c_contextdata.a.media.qoe.mediaSdkErrors`. Dieses Feld gilt nicht für Implementierungen der Mediensammlungs-API oder der Media Edge-API.

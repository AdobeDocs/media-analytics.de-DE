---
title: Erfahren Sie, wie Sie Fehler in Roku verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Fehler-Trackings mit dem Media SDK in Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 81%

---

# Tracking von Fehlern in Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

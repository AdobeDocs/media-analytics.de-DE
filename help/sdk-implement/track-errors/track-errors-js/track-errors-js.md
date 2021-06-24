---
title: Erfahren Sie, wie Sie Fehler mit JavaScript 2.x verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Fehler-Trackings mit dem Media SDK in Browser-Apps (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
exl-id: b3012bce-4b92-408e-8b7a-57ae9d52e93d
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 79%

---

# Tracking von Fehlern mit JavaScript 2.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer:

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

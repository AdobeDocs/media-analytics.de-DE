---
seo-title: Tracking von Fehlern in JavaScript
title: Tracking von Fehlern in JavaScript
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking von Fehlern in JavaScript{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Fehlerverfolgung implementieren

1. Medienplayer-Fehler verfolgen:

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>Die Verfolgung von Medienplayer-Fehlern beendet die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.


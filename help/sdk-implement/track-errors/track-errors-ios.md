---
seo-title: Tracking von Fehlern in iOS
title: Tracking von Fehlern in iOS
uuid: 18 ea 93 d 3-5948-4375-bcdb -72309268 e 38 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Tracking von Fehlern in iOS{#track-errors-on-ios}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](../../sdk-implement/download-sdks.md)

## Fehlerverfolgung implementieren

1. Verfolgen Sie Medienplayer-Fehler:

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>Die Verfolgung von Fehlern im Medienplayer stoppt die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.


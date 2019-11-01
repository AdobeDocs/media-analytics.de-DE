---
title: Tracking von Fehlern in Chromecast
description: In diesem Thema wird die Implementierung der Fehlerverfolgung mit dem Media SDK on Chromecast beschrieben.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracking von Fehlern in Chromecast{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Fehlerverfolgung implementieren

1. Track media player errors: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Die Verfolgung von Medienplayer-Fehlern beendet die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.


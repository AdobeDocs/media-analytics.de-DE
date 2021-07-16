---
title: Erfahren Sie, wie Sie Fehler in Chromecast verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Fehler-Trackings mit dem Media SDK in Chromecast.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
exl-id: 513772c2-582d-4b4b-92ed-0c32b99d7fdc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 82%

---

# Tracking von Fehlern in Chromecast{#track-errors-on-chromecast}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

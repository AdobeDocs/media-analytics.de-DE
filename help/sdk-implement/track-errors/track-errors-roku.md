---
title: Erfahren Sie, wie Sie Fehler in Roku verfolgen können.
description: Erfahren Sie mehr über die Implementierung der Fehlerverfolgung mit dem Media SDK in Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 100%

---

# Tracking von Fehlern in Roku {#track-errors-on-roku}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
> Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

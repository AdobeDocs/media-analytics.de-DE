---
title: Tracking von Fehlern mit JavaScript 3.x
description: Hier wird die Implementierung des Fehler-Trackings mit dem Media SDK in Browser-Apps (JS) beschrieben.
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '95'
ht-degree: 100%

---

# Tracking von Fehlern mit JavaScript 3.x {#track-errors-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 3.x-SDKs vornehmen. Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

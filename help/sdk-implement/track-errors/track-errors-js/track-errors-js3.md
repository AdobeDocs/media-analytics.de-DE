---
title: Erfahren Sie, wie Sie Fehler mit JavaScript 3.x verfolgen können.
description: Erfahren Sie, wie Sie das Fehler-Tracking mit dem Media SDK in Browser-Apps (JS) implementieren.
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 100%

---

# Tracking von Fehlern mit JavaScript 3.x{#track-errors-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

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

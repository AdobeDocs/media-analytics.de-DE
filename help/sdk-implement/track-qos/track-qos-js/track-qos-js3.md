---
title: Erfahren Sie, wie Sie die Erlebnisqualität mit JavaScript 3.x verfolgen können.
description: „Erfahren Sie, wie Sie das Tracking der Erlebnisqualität (QoE, QoS) mit dem Medien-SDK in Browser-Programmen mit JavaScript 3x implementieren.“
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Tracking der Erlebnisqualität mit JavaScript 3.x{#track-quality-of-experience-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren von QOE

1. Ermitteln Sie, wann sich die Bit-Rate während der Medienwiedergabe ändert, und erstellen Sie die `qoeObject`-Instanz mithilfe der QoE-Informationen.

   QoEObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Servicequalität (QoS) verfolgen möchten.

   | Variable | Typ | Beschreibung |
   | --- | --- | --- |
   | `bitrate` | Anzahl | Aktuelle Bitrate |
   | `startupTime` | Anzahl | Startzeit |
   | `fps` | Anzahl | FPS-Wert |
   | `droppedFrames` | Anzahl | Anzahl der Dropped Frames |

   QoE-Objekterstellung:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoE-Objekt und rufen Sie bei jeder Bit-Ratenänderung das Ereignis zur Bit-Ratenänderung auf. So erhalten Sie die genauesten QoE-Daten.

1. Rufen Sie unbedingt die Methode `updateQoEObject()` auf, um die aktuellsten QoE-Informationen für das SDK bereitzustellen.
1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

---
title: Verfolgen Sie die Qualität der Erfahrung mit JavaScript 3.x.
description: In diesem Thema wird beschrieben, wie Sie die QoE- und QoS-Verfolgung mithilfe des Media SDK in Browser-Apps mit JavaScript 3x implementieren.
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# Verfolgen Sie die Qualität der Erfahrung mit JavaScript 3.x.{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 3.x-SDKs vornehmen. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementieren von QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   Objektvariablen:

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
   >Aktualisieren Sie das QoE-Objekt und rufen Sie bei jeder Bitratenänderung das Bitratenänderungs-Ereignis auf. Dadurch werden die genauesten QoE-Daten bereitgestellt.

1. Achten Sie darauf, die `updateQoEObject()` Methode aufzurufen, um die aktuellsten Servicequalitätsinformationen für das SDK bereitzustellen.
1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

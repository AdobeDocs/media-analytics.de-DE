---
title: Tracking der Erlebnisqualität mit JavaScript 2.x
description: Hier wird die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit dem Medien-SDK in Browser-Programmen mit JavaScript 2.x erläutert.
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '219'
ht-degree: 100%

---

# Tracking der Erlebnisqualität mit JavaScript 2.x {#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementierung von QoS

1. Ermitteln Sie, wann sich die Bitrate während der Medienwiedergabe ändert, und erstellen Sie die `MediaObject`-Instanz mithilfe der QoS-Informationen.

   QoSObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Servicequalität (QoS) verfolgen möchten.

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   Erstellung von QoS-Objekten:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>);
   ```

1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoS-Objekt und rufen Sie das Ereignis zur Bitratenänderung bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

1. Stellen Sie sicher, dass die `getQoSObject()`-Methode die neuesten QoS-Informationen zurückgibt.
1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

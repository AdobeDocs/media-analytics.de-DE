---
title: Überblick
description: Eine Übersicht über die Qualität der Verfolgung von Erlebnissen (QoE, QoS) mit dem Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Sie können die Medienplayer-API verwenden, um die Variablen im Zusammenhang mit Servicequalitätsprüfung und Fehlerverfolgung zu identifizieren. Das Tracking der Erlebnisqualität umfasst folgende wichtige Elemente:

## Player-Ereignisse {#player-events}

### Bei allen QoS-Metrikänderungen:

Erstellen oder aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe. [QoS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Bei allen Ereignissen zu Bitratenänderungen

Aufruf    `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementierung von QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   QoSObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, QoS zu verfolgen.

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

1. Stellen Sie sicher, dass die `getQoSObject()`-Methode die neuesten QoS-Informationen zurückgibt.
1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf.

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoS-Objekt und rufen Sie bei jeder Bitratenänderung das Bitratenänderungsereignis auf. So erhalten Sie möglichst präzise Daten.

Im folgenden Beispielcode wird das JavaScript 2.x SDK für einen HTML5-Medienplayer verwendet. Sie sollten diesen Code mit dem Core-Media-Wiedergabecode verwenden.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```


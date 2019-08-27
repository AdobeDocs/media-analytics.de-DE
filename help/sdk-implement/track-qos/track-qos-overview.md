---
seo-title: Überblick
title: Überblick
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Sie können die Media Player-API verwenden, um die Variablen zu identifizieren, die mit Servicequalitäts- und Fehlerverfolgung zusammenhängen. Das Tracking der Erlebnisqualität umfasst folgende wichtige Elemente:

## Player-Ereignisse {#player-events}

### Bei allen QoS-Metrikänderungen:

Erstellen oder aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe. [Qos-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Bei allen Ereignissen zu Bitratenänderungen

Aufruf    `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementierungs-QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   QoSObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, qos zu verfolgen.

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
   >Aktualisieren Sie das qos-Objekt und rufen Sie das Bitratenänderungsereignis bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

Der folgende Beispielcode verwendet das javascript 2. x SDK für einen HTML 5-Medienplayer. Sie sollten diesen Code mit dem Core-Media-Wiedergabecode verwenden.

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


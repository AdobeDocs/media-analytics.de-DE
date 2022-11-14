---
title: Nachverfolgen der Quality of Experience
description: Eine Übersicht über das Tracking der Erlebnisqualität (QoE, QoS) mit dem Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 100%

---

# Überblick {#overview}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

Das Tracking der Erlebnisqualität (QoE) beinhaltet Servicequalität (QoS) und Fehler-Tracking. Diese beiden Elemente sind optional und **nicht** für die Implementierung des Core-Medien-Tracking erforderlich. Sie können die Medienplayer-API verwenden, um die Variablen für QoS- und Fehler-Tracking zu ermitteln. Das Tracking der Erlebnisqualität umfasst folgende wichtige Elemente:

## Player-Ereignisse {#player-events}

### Bei allen QoS-Metrikänderungen:

Erstellen oder aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe. [QoS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Bei allen Ereignissen zu Bitratenänderungen

Aufruf `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementierung von QoS

1. Erkennen Sie, wann sich eine der QoS-Metriken während der Medienwiedergabe ändert, erstellen Sie `MediaObject` anhand der QoS-Informationen und aktualisieren Sie die neuen QoS-Informationen.

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

1. Stellen Sie sicher, dass die `getQoSObject()`-Methode die neuesten QoS-Informationen zurückgibt.
1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf.

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoS-Objekt und rufen Sie das Ereignis zur Bitratenänderung bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

Der folgende Beispielcode nutzt das JavaScript 2.x-SDK für einen HTML5-Medienplayer. Sie sollten diesen Code mit dem Code zur Core-Medienwiedergabe verwenden.

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

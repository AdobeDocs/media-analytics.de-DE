---
title: Nachverfolgen der Quality of Experience
description: Eine Übersicht über das Tracking der Erlebnisqualität (QoE, QoS) mit dem Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 99%

---

# Überblick{#overview}

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

## Implementieren von QoS

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

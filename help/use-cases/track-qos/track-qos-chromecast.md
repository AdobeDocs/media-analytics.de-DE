---
title: Erfahren Sie, wie Sie die Erlebnisqualität in Chromecast verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit Media SDK in Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VR-udMMg3tOMsbxnt-f0zjkGVZNgnCON0diYrhhMuoE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 95%

---

# Tracking der Erlebnisqualität in Chromecast{#track-quality-of-experience-on-chromecast}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Überblick {#overview}

Das Tracking der Erlebnisqualität (QoE) beinhaltet Servicequalität (QoS) und Fehler-Tracking. Diese beiden Elemente sind optional und **nicht** für die Implementierung des Core-Medien-Tracking erforderlich. Sie können die Medienplayer-API verwenden, um die Variablen für QoS- und Fehler-Tracking zu ermitteln.

## Player-Ereignisse {#player-events}

### Bei allen Ereignissen zu Bitratenänderungen

* Erstellen/aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe, `qosObject`.
* Aufruf `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Bei Player-Fehlern

Aufruf `trackError("media error id");`

## Implementierung {#implement}

1. Ermitteln Sie, wann sich die Bitrate während der Medienwiedergabe ändert, und erstellen Sie die `MediaObject`-Instanz mithilfe der QoS-Informationen.

   **QoSObject-Variablen:**

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Servicequalität (QoS) verfolgen möchten.

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   **Erstellung von QoS-Objekten:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoS-Objekt und rufen Sie das Ereignis zur Bitratenänderung bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

1. Stellen Sie sicher, dass die `getQoSObject()`-Methode die neuesten QoS-Informationen zurückgibt.
1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer stoppt die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

---
title: Erfahren Sie, wie Sie die Erlebnisqualität in Chromecast verfolgen können.
description: '"Erfahren Sie mehr über die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit dem Media SDK in Chromecast."'
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 91%

---

# Tracking der Erlebnisqualität auf Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Überblick {#overview}

Das Tracking der Erlebnisqualität (QoE) beinhaltet Servicequalität (QoS) und Fehler-Tracking. Diese beiden Elemente sind optional und **nicht** für die Implementierung des Core-Medien-Tracking erforderlich. Sie können die Medienplayer-API verwenden, um die Variablen für QoS- und Fehler-Tracking zu ermitteln.

## Player-Ereignisse {#player-events}

### Bei allen Ereignissen zu Bitratenänderungen

* Erstellen/aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe, `qosObject`.
* Aufruf `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Bei Player-Fehlern

Aufruf `trackError(“media error id”);`

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
1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

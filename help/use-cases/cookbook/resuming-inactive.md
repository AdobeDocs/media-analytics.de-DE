---
title: Wiederaufnehmen von inaktiven Sitzungen
description: Erfahren Sie, wie Sie eine inaktive Sitzung wieder aufnehmen können.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 38%

---

# Wiederaufnehmen von inaktiven Sitzungen{#resuming-inactive-sessions}

## Lange Pausen

Die Media SDK verfolgt automatisch, wie lange die Medienwiedergabe einen der folgenden inaktiven Status aufweist:

* Angehalten
* Wird gesucht
* Angehalten
* Pufferung

Wenn eine Medien-Tracking-Sitzung länger als 30 Minuten inaktiv ist, wird die Sitzung automatisch geschlossen. Wenn der Anwender eine zuvor inaktive Tracking-Sitzung wiederaufnimmt (`trackPlay`), erstellt Media Heartbeat automatisch eine neue Videositzung mit den zuvor verwendeten Videoinformationen und Metadaten und sendet ein Heartbeat-Ereignis zur Wiederaufnahme.

## Geräteübergreifende Weiterleitung mithilfe der Fortsetzungs-Markierung

Derselbe Fortsetzungsmechanismus, der die Fortsetzung von Single-App-Sitzungen handhabt, gilt auch, wenn ein Viewer die Wiedergabe zwischen Geräten überträgt - z. B. das Senden eines Videos von einem Mobiltelefon zu einem Fernseher oder Chromecast-Empfänger. Da jedes Gerät seine eigene Media SDK-Instanz ausführt, werden bei der Übergabe standardmäßig mehrere Sitzungen erstellt. Verwenden Sie das Fortsetzungs-Flag, um sie zu einer logischen Fortsetzung zusammenzufügen, sodass Analytics die kombinierte Anzeige als ein einzelnes Interaktionsstück und nicht als separate Medien startet.

**Implementierung:**

1. Rufen Sie auf dem **Quellgerät** (z. B. dem Telefon) `trackSessionEnd` auf, wenn der Viewer die Besetzung initiiert. Rufen Sie `trackComplete` nicht auf - der Inhalt ist noch nicht fertig, er wird auf ein anderes Gerät verschoben.
2. Rufen Sie auf dem **Zielgerät** (z. B. dem Chromecast) `trackSessionStart` auf, wobei das Fortsetzungs-Flag auf `true` gesetzt ist und die gleichen Inhaltsmetadaten (Name, ID, Länge) auf dem Quellgerät verwendet werden. Übergeben Sie die Abspielposition, an der der Viewer auf dem Quellgerät aufgehört hat.
3. Wenn der Viewer die Wiedergabe später an das Quellgerät zurückgibt, wiederholen Sie das gleiche Muster: `trackSessionEnd` am Ziel und `trackSessionStart` mit dem Fortsetzungs-Flag auf der Quelle.

Durch Festlegen des Fortsetzungs-Flags erhöht [ Adobe Analytics für den zweiten und die folgenden ](/help/reporting/metrics/media-starts.md) der Übergabe ](/help/reporting/metrics/content-resumes.md)Inhaltswiederaufnahmen[ anstelle von „Medienstarts. Da es keinen integrierten Mechanismus zum Freigeben der Sitzungs-ID zwischen SDK-Instanzen gibt, ist das Fortsetzungs-Flag eine Client-seitige Deklaration - Sie übergeben es basierend auf Ihrer Anwendungslogik, wenn Sie wissen, dass der Viewer eine vorherige Sitzung fortsetzt.

## Manuelles Wiederaufnehmen einer zuvor geschlossenen Sitzung

Die Media SDK nimmt Sitzungen nur dann automatisch wieder auf, wenn die Anwendung nicht geschlossen wurde. Wenn die Anwendung Benutzerdaten speichert und in der Lage ist, ein zuvor geschlossenes Medium wiederaufzunehmen, kann ein Wiederaufnahmeereignis manuell ausgelöst werden. Wenn Sie die Video-Tracking-Sitzung starten, legen Sie die optionale Eigenschaft zur Videowiederaufnahme fest.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```

---
title: Handbuch zur Implementierung von Custom Link
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
source-git-commit: e56ce73316d9cf00193220df8959a489fc3f2124
workflow-type: ht
source-wordcount: '189'
ht-degree: 100%

---

# Implementierungshandbuch für benutzerdefinierte Links {#custom-link-implementation-guide}

Das benutzerdefinierte Video-Tracking verwendet das manuelle Link-Tracking mit benutzerdefiniertem Link-Code im `appMeasurement` in Analytics.
Meistens wird das anwenderdefinierte Video-Tracking auf Plattformen und Geräten verwendet, bei denen eine minimale Videomessung erforderlich ist.

* In JavaScript: die Funktion `s.tl()`
* In mobilen Apps: [trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=de), [trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=de), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* In der Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Voraussetzungen

* Zugriff auf API-Ereignisse und -Daten für Videoplayer
* Möglichkeit zum Hinzufügen von Skripts bei Verwendung des Analytics SDK
* Möglichkeit zum Hinzufügen von Tracking-Beacons (benutzerdefiniertes Skript oder fester Code) bei Verwendung der Data Insertion API

## Metadaten

* Metadaten können zu jedem Tracking-Aufruf als Teil der Verknüpfungsdaten hinzugefügt werden.
* Denken Sie daran, `linkTrackVars` und `linkTrackEvents` zu aktualisieren

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## Warum sollte man benutzerdefinierte Links verwenden?

* Minimale Voraussetzungen sind erforderlich.
* Funktioniert auf jeder Plattform, auch solchen ohne Skript.
* Alle Berechnungen wie Zeitdauer oder Quartil müssen in einem benutzerdefinierten Skript berechnet werden.
* Einfache Nutzung ohne verborgene Bibliotheken oder Skripts
* Gesamtkontrolle über jeden Aspekt der Videodaten

## Beispiel für JavaScript für HTML5 Player

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```

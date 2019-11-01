---
title: Handbuch zur Implementierung von Custom Link
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Custom Link Implementation Guide{#custom-link-implementation-guide}

Custom Video Tracking uses [manual link tracking using custom link code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) within Analytics `appMeasurement`.
Meistens wird das anwenderdefinierte Video-Tracking auf Plattformen und Geräten verwendet, bei denen eine minimale Videomessung erforderlich ist.

* In JavaScript: die `s.tl()` Funktion
* In mobilen Apps: [trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html), [trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* In the Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Voraussetzungen

* Zugriff auf Ereignisse und Daten der Video-Player-APIs
* Möglichkeit, Skripte hinzuzufügen, wenn das Analytics-SDK verwendet wird
* Möglichkeit, Tracking Beacons (anwenderdefiniertes Skripting oder Hardcode) hinzuzufügen, wenn Sie die Data Insertion API verwenden

## Metadaten

* Metadaten können zu jedem Tracking-Aufruf als Teil der Verknüpfungsdaten hinzugefügt werden.
* Remember to update the `linkTrackVars` and `linkTrackEvents`

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

## Warum benutzerspezifischen Link verwenden

* Es sind nur minimale Voraussetzungen erforderlich
* Es funktioniert auf jeder Plattform, einschließlich NoScript
* Alle Berechnungen, wie z. B. Verweildauern oder Quartile, müssen in einem anwenderdefinierten Skript berechnet werden
* Es ist äußerst unkompliziert ohne versteckte Bibliotheken oder Skripte
* Sie haben volle Kontrolle über jeden Aspekt der Videodaten

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

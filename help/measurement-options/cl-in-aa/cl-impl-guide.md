---
seo-title: Handbuch zur Implementierung von Custom Link
title: Handbuch zur Implementierung von Custom Link
uuid: 83315 e 73-20 ca -4 db 5-9 d 43-33 daade 45 a 13
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Handbuch zur Implementierung von Custom Link{#custom-link-implementation-guide}

Das anwenderdefinierte Video-Tracking verwendet das [manuelle Link-Tracking mit Custom Link-Code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) im Analytics `appMeasurement`. Meistens wird das anwenderdefinierte Video-Tracking auf Plattformen und Geräten verwendet, bei denen eine minimale Videomessung erforderlich ist.

* In JavaScript: `s.tl()` function
* In mobilen Apps: [trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html), [trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)

* In Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

**Anforderungen:**

* Zugriff auf Ereignisse und Daten der Video-Player-APIs
* Möglichkeit, Skripte hinzuzufügen, wenn das Analytics-SDK verwendet wird
* Möglichkeit, Tracking Beacons (anwenderdefiniertes Skripting oder Hardcode) hinzuzufügen, wenn Sie die Data Insertion API verwenden

**Metadaten:**

* Metadaten können zu jedem Tracking-Aufruf als Teil der Verknüpfungsdaten hinzugefügt werden.
* Remember to update the `linkTrackVars` and `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15’; 
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

**Warum sollte man Custom Link verwenden?**

* Es sind nur minimale Voraussetzungen erforderlich
* Es funktioniert auf jeder Plattform, einschließlich NoScript
* Alle Berechnungen, wie z. B. Verweildauern oder Quartile, müssen in einem anwenderdefinierten Skript berechnet werden
* Es ist äußerst unkompliziert ohne versteckte Bibliotheken oder Skripte
* Sie haben volle Kontrolle über jeden Aspekt der Videodaten
* Link zum Beispiel-Player entfernen

**Beispiel für JavaScript für HTML5 Player**

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


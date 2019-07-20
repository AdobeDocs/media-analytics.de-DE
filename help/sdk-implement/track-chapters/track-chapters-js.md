---
seo-title: Tracking von Kapiteln und Segmenten in JavaScript
title: Tracking von Kapiteln und Segmenten in JavaScript
uuid: ef 99 eef 7-7 a 77-46 c 4-8429-bc 9 a 856 b 98 d 6
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Tracking von Kapiteln und Segmenten in JavaScript{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit 2. x sdks. Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](../../sdk-implement/download-sdks.md)

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   `ChapterObject` Kapitelverfolgungsreferenz:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Kapitel verfolgen möchten.

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Kapitelname | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellänge | Ja |
   | `startTime` | Startzeit des Kapitels | Ja |

   Kapitelobjekt:

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten:

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf:

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.


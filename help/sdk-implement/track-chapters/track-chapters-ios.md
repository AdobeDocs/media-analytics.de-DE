---
seo-title: Tracking von Kapiteln und Segmenten in iOS
title: Tracking von Kapiteln und Segmenten in iOS
uuid: ffc 5 ce 9 f -04 ba -4059-92 d 4-4 cb 4180 ac 9
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking von Kapiteln und Segmenten in iOS{#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit 2. x sdks. Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

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

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf:

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.


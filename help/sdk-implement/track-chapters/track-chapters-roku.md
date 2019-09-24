---
seo-title: Tracking von Kapiteln und Segmenten in Roku
title: Tracking von Kapiteln und Segmenten in Roku
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking von Kapiteln und Segmenten in Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit 2.x SDKs. Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementieren von Standard-Anzeigenmetadaten

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   `ChapterObject` Kapitelverfolgungsreferenz:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, Kapitel zu verfolgen.

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Kapitelname | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellänge | Ja |
   | `startTime` | Startzeit des Kapitels | Ja |

   Kapitelobjekt:

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten:

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.


---
title: Erfahren Sie, wie Sie Kapitel und Segmente in Android verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Kapitel- und Segment-Trackings mit dem Media SDK in Android.
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
exl-id: ada2e2a7-1383-471c-9ce6-c82ea93fa79d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---

# Tracking von Kapiteln und Segmenten in Android{#track-chapters-and-segments-on-android}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Implementieren von Kapitel-Tracking

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   Kapitel-Tracking-Referenz `ChapterObject`:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie Kapitel verfolgen möchten.

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Kapitelname | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellänge | Ja |
   | `startTime` | Startzeit des Kapitels | Ja |

   Kapitelobjekt:

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten:

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>();
   chapterMetadata.put("segmentType", "Sample Segment Type");
   chapterMetadata.put("segmentName", "Sample Segment Name");
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata);
   }
   ```

1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null);
   }
   ```

1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf:

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null);
   }
   ```

1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.

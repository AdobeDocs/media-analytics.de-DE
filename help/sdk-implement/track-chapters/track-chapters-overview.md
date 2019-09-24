---
seo-title: Überblick
title: Überblick
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit 2.x SDKs. Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Die Kapitel- und Segmentverfolgung ist für benutzerdefinierte Medienkapitel oder Segmente verfügbar. Einige gängige Verwendungszwecke für die Kapitelverfolgung sind die Definition benutzerspezifischer Segmente auf der Grundlage von Medieninhalten (wie z. B. Baseballeinführungen) oder die Definition von Inhaltssegmenten zwischen Werbeunterbrechungen. Chapter tracking is **not** required for core media tracking implementations.

Das Kapitel-Tracking beinhaltet Kapitelstarts, -beendigungen und übersprungene Kapitel. Sie können die Medienplayer-API mit angepasster Segmentierungslogik verwenden, um Kapitelereignisse zu identifizieren und die erforderlichen und optionalen Kapitelvariablen zu füllen.

## Player-Ereignisse

### Beim Kapitelstart

* Erstellen Sie die Kapitelobjektinstanz für das Kapitel, `chapterObject`.
* Populate the chapter metadata, `chapterCustomMetadata`
* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Beim Abschluss eines Kapitels

* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Beim Überspringen eines Kapitels

* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Kapitelverfolgung implementieren {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   Im Folgenden finden Sie die `ChapterObject`-Referenz zum Kapitel-Tracking:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, Kapitel zu verfolgen.

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Kapitelname | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellänge | Ja |
   | `startTime` | Startzeit des Kapitels | Ja |

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten.
1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf.
1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf.
1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf.
1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.

Im folgenden Beispielcode wird das JavaScript 2.x SDK für einen HTML5-Medienplayer verwendet. Sie sollten diesen Code mit dem Core-Media-Wiedergabecode verwenden.

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```


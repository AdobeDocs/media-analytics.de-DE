---
seo-title: Überblick
title: Überblick
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit 2. x sdks. Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Kapitel- und Segmentverfolgung ist für benutzerdefinierte Medienkapitel oder Segmente verfügbar. Einige gängige Einsatzmöglichkeiten für die Kapitelverfolgung sind die Definition benutzerdefinierter Segmente basierend auf Medieninhalten (wie z. B. Baseball-Schriften) oder die Definition von Inhaltssegmenten zwischen Werbeunterbrechungen. Chapter tracking is **not** required for core media tracking implementations.

Das Kapitel-Tracking beinhaltet Kapitelstarts, -beendigungen und übersprungene Kapitel. Sie können die Media Player-API mit angepasster Segmentierungslogik verwenden, um Kapitelereignisse zu identifizieren und die erforderlichen und optionalen Kapitelvariablen auszufüllen.

## Player-Ereignisse

### Beim Kapitelstart

* Erstellen Sie die Kapitelobjektinstanz für das Kapitel, `chapterObject`.
* Populate the chapter metadata, `chapterCustomMetadata`
* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Beim Abschluss eines Kapitels

* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Beim Überspringen eines Kapitels

* Aufruf    `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   Im Folgenden finden Sie die `ChapterObject`-Referenz zum Kapitel-Tracking:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Kapitel verfolgen möchten.

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

Der folgende Beispielcode verwendet das javascript 2. x SDK für einen HTML 5-Medienplayer. Sie sollten diesen Code mit dem Core-Media-Wiedergabecode verwenden.

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

## Überprüfen {#section_07EC2811BE3249249494596BFE9BF869}

### Chapter Start

Beim Start einer einzelnen Kapitelwiedergabe wird ein Schlüsselaufruf gesendet:

* Heartbeat Chapter Start (Dieser Aufruf enthält zusätzliche Kapitelmetadatenvariablen.)

### Kapitelbeendigung

Nach Abschluss der Kapitelwiedergabe wird ein Heartbeat-Chapter-Complete-Aufruf gesendet.

### Übersprungenes Kapitel

Wenn ein Kapitel übersprungen wird, wird ein Heartbeat-Chapter-Skip-Aufruf gesendet.

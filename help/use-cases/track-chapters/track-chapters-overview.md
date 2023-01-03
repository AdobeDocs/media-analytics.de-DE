---
title: Verfolgen von Kapiteln und Segmenten – Erklärung
description: Implementieren des Kapitel- und Segment-Trackings mit dem Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---

# Überblick {#overview}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
> 
> Wenn Sie Version 1.x des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

Das Tracking von Kapiteln und Segmenten ist für benutzerdefinierte Medienkapitel oder -segmente verfügbar. Zu den Anwendungsfällen für Kapitel-Tracking zählt die Definition von Kundensegmenten basierend auf Medieninhalten, z. B. Baseball-Innings, oder die Definition von Inhaltssegmenten zwischen Werbeunterbrechungen. Das Kapitel-Tracking ist **nicht** für die Implementierung des Core-Medien-Trackings erforderlich.

Das Kapitel-Tracking beinhaltet Kapitelstarts, -beendigungen und übersprungene Kapitel. Sie können die Medienplayer-API mit einer benutzerdefinierten Segmentierungslogik verwenden, um Kapitelereignisse zu erkennen und die erforderlichen und optionalen Kapitelvariablen hinzuzufügen.

## Player-Ereignisse

### Beim Kapitelstart

* Erstellen Sie die Kapitelobjektinstanz für das Kapitel, `chapterObject`.
* Fügen Sie die Kapitelmetadaten, `chapterCustomMetadata`, hinzu.
* Aufruf `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Beim Abschluss eines Kapitels

* Aufruf `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Beim Überspringen eines Kapitels

* Aufruf `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementieren von Kapitel-Tracking {#implement-chapter-tracking}

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   Im Folgenden finden Sie die `ChapterObject`-Referenz zum Kapitel-Tracking:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie Kapitel verfolgen möchten.

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

Der folgende Beispielcode nutzt das JavaScript 2.x-SDK für einen HTML5-Medienplayer. Sie sollten diesen Code mit dem Code zur Core-Medienwiedergabe verwenden.

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

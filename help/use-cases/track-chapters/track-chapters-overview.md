---
title: Verfolgen von Kapiteln und Segmenten – Erklärung
description: Implementieren des Kapitel- und Segment-Trackings mit dem Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 97%

---

# Überblick{#overview}

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
   | `name` | Name des Kapitels | Ja |
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

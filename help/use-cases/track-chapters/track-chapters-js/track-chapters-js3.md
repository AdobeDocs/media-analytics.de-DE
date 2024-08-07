---
title: Lernen Sie, wie Sie Kapitel und Segmente mit JavaScript 3.x verfolgen
description: Erfahren Sie mehr über die Implementierung des Kapitel- und Segment-Trackings mit dem Media SDK in Browser-Apps (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 100%

---

# Tracking von Kapiteln und Segmenten mit JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 3.x-SDKs vornehmen.

>[!IMPORTANT]
>
> Wenn Sie vorherige Versionen des SDKs implementieren möchten, können Sie hier das Entwicklerhandbuch herunterladen: [SDKs herunterladen](/help/getting-started/download-sdks.md).

1. Ermitteln Sie, wann das Kapitel beginnt, und erstellen Sie die `ChapterObject`-Instanz mithilfe dieser Kapitelinformationen.

   Kapitel-Tracking-Referenz `ChapterObject`:

   >[!NOTE]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie Kapitel verfolgen möchten.

   | Variablenname | Typ | Beschreibung |
   | --- | --- | --- |
   | `name` | string | Nicht leere Zeichenfolge, die den Kapitelnamen angibt. |
   | `position` | number | Die Positionsnummer des Kapitels innerhalb des Inhalts, beginnend bei 1. |
   | `length` | number | Positive Zahl, die die Länge des Kapitels angibt. |
   | `startTime` | number | Wert des Abspielkopfs am Beginn des Kapitels. |

   Kapitelobjekt:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Wenn Sie anwenderspezifische Metadaten für das Kapitel hinzufügen, erstellen Sie die Kontextdaten-Variablen für die Metadaten:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Um das Tracking der Kapitelwiedergabe zu starten, rufen Sie das `ChapterStart`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Wenn die Wiedergabe das Kapitelende nach Definition Ihres anwenderspezifischen Codes erreicht, rufen Sie das `ChapterComplete`-Ereignis in der `MediaHeartbeat`-Instanz auf:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Wenn die Kapitelwiedergabe nicht abgeschlossen wurde, weil der Anwender das Kapitel übersprungen hat (z. B. zu einer Position außerhalb des Kapitels springt), rufen Sie das `ChapterSkip`-Ereignis in der MediaHeartbeat-Instanz auf:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Wiederholen Sie die Schritte 1 bis 5, wenn es weitere Kapitel gibt.

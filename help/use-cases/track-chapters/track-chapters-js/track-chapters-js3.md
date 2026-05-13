---
title: Lernen Sie, wie Sie Kapitel und Segmente mit JavaScript 3.x verfolgen
description: Erfahren Sie mehr über die Implementierung des Kapitel- und Segment-Trackings mit dem Media SDK in Browser-Apps (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/YZAcZVcqS15hCae-LYwjpSYztXijauQNIzElCcWcPT0
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 224
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

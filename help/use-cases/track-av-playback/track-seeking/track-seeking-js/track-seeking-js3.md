---
title: Erfahren Sie, wie Sie Suchen mit JavaScript 3.x verfolgen.
description: Erfahren Sie, wie Sie Suchstart- und Suchabschlussereignisse mithilfe des Media SDK in Browser-Apps (JS 3.x) verfolgen.
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/orl8i3mc3iQm3t8cY9yCLOmFDoAHiryvMMANvfs5wpM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 138
ht-degree: 100%

---

# Nachverfolgen von Suchen mit JavaScript 3.x{#track-seeking-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung der 3.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Suchen-Tracking-Konstanten

| Konstantenname | Beschreibung     |
|---|---|
| `SeekStart` | Konstante für die Verfolgung des Suchstartereignisses. |
| `SeekComplete` | Konstante für die Verfolgung des Suchabschlussereignisses. |

## Suche implementieren

1. Suchen Sie nach den Wiedergabesuchereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Wenn Sie die Benachrichtigung zum Suchabschluss vom Medienplayer erhalten, zeichnen Sie das Suchende mit dem `SeekComplete`-Ereignis auf:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/use-cases/tracking-scenarios/vod-seeking.md).

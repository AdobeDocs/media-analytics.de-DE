---
title: Tracking des Suchens mit JavaScript 3.x
description: Hier wird die Implementierung des Suchen-Trackings mit dem Media SDK in Browser-Apps (JS) beschrieben.
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '126'
ht-degree: 100%

---

# Tracking des Suchens mit JavaScript 3.x {#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 3.x-SDKs vornehmen. Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

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

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/sdk-implement/tracking-scenarios/vod-seeking.md).

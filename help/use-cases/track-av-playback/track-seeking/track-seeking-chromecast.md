---
title: Erfahren Sie, wie Sie Suchen in Chromecast verfolgen können.
description: Erfahren Sie, wie Sie mit dem Media SDK in Chromecast Suchstart- und Suchabschlussereignisse verfolgen.
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
exl-id: 03be8ed3-ae3a-4e9a-b667-0d9280a844a1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N2OC8Ob2EoQndimEFbP8yKMXqiOTgGMEt7aO6krUpEE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 155
ht-degree: 100%

---

# Nachverfolgen von Suchen auf Chromecast{#track-seeking-on-chromecast}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Suchen-Tracking-Konstanten

| Konstantenname | Beschreibung     |
|---|---|
| `SeekStart` | Konstante für die Verfolgung des Suchstartereignisses. |
| `SeekComplete` | Konstante für die Verfolgung des Suchabschlussereignisses. |

## Suche implementieren

1. Suchen Sie nach den Wiedergabesuchereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart);
   ```

1. Wenn Sie die Suchabschlussbenachrichtigung vom Medienplayer erhalten, verfolgen Sie das Ende der Suche mit dem `SeekComplete`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete);
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/use-cases/tracking-scenarios/vod-seeking.md).

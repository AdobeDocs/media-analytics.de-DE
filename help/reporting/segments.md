---
title: Medien-Streaming-Segmente – Erklärung
description: Erfahren Sie mehr über die Berichterstellungssegmente, die mit dem Medien-Stream-Typ verknüpft sind, einschließlich Segment, Beschreibung und Regel für den Medien-Stream-Typ.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 76%

---

# Mediensegmente{#segments}

Mit Segmenten können Besucherteilmengen anhand von Merkmalen oder Website-Interaktionen identifiziert werden. Mit Streaming-Mediensegmenten können Sie den Besucher-Stream-Typ wie Audio-, Live- oder Podcast-Streams identifizieren. Weitere Informationen zu Adobe Analytics-Segmenten finden Sie [Informationen zu Segmenten](https://experienceleague.adobe.com/en/docs/analytics/components/segmentation/seg-overview) im Adobe Analytics-Komponentenhandbuch.

| Segment | Beschreibung | Regel |
|---|---|---|
| Medien-Streamingtyp: Alle | Segmentieren aller *Medien*-Stream-Daten | „Content (ID) exists“ |
| Medien-Streamingtyp: Audio | Segmentieren aller *Audio*-Stream-Daten | „Content (ID) exists“ UND „Media Stream Type = `audio`“ |
| Medien-Streamingtyp: Video | Segmentieren aller *Video*-Stream-Daten | „Content (ID) exists“ UND „Media Stream Type != `audio`“ |
| Medien-Content-Typ: VoD | Segmentieren aller VoD-Inhalte | „Content-Typ = `vod`“ |
| Medien-Content-Typ: Live | Segmentieren aller Live-Inhalte | „Content-Typ = `live`“ |
| Medien-Content-Typ: Linear | Segmentieren aller linearen Inhalte | „Content-Typ = `linear`“ |
| Medien-Content-Typ: Podcast | Segmentieren aller Podcast-Inhalte | „Content-Typ = `podcast`“ |
| Medien-Content-Typ: Audiobook | Segmentieren aller Audiobook-Inhalte | „Content-Typ = `audiobook`“ |
| Medien-Content-Typ: AoD | Segmentieren aller AoD-Inhalte | „Content-Typ = `aod`“ |

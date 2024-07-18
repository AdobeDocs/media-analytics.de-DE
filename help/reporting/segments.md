---
title: Medien-Streaming-Segmente – Erklärung
description: „Erfahren Sie mehr über die Berichterstellungssegmente, die mit dem Medien-Stream-Typ verknüpft sind, einschließlich Segment, Beschreibung und Regel für den Medien-Stream-Typ.“
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Media Analytics, Segmentation"
role: User, Admin, Data Engineer
source-git-commit: b15a81dc8f08e94c9b80d66019f3d0fe95ef5a74
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 100%

---

# Mediensegmente{#segments}

Mit Segmenten können Besucheruntergruppen anhand von Merkmalen oder Website-Interaktionen identifiziert werden. Mit Streaming-Mediensegmenten können Sie den Besucher-Stream-Typ wie Audio-, Live- oder Podcast-Streams identifizieren. Weitere Informationen zu Adobe Analytics-Segmenten finden Sie unter [Informationen zu Segmenten und Containern](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=de) im Adobe Analytics Komponenten-Handbuch.

>[!NOTE]
>
>Diese Segmente für die Berichterstellung, die dem Medien-Streamtyp zugeordnet sind, wurden am 13.9.18 zusammen mit dem `streamType`-Parameter eingeführt.

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

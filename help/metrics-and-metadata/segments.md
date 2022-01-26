---
title: Medien-Streaming-Segmente – Erklärung
description: „Erfahren Sie mehr über die Berichterstellungssegmente, die mit dem Medien-Stream-Typ verknüpft sind, einschließlich Segment, Beschreibung und Regel für den Medien-Stream-Typ.“
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Media Analytics, Segmentation
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---

# Segmente{#segments}

Mit Segmenten können Besucheruntergruppen anhand von Merkmalen oder Website-Interaktionen identifiziert werden. Mit Streaming-Mediensegmenten können Sie den Besucher-Stream-Typ wie Audio-, Live- oder Podcast-Streams identifizieren. Weitere Informationen zu Adobe Analytics-Segmenten finden Sie unter [Informationen zu Segmenten und Containern](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=de) im Adobe Analytics Komponenten-Handbuch.

>[!NOTE]
>
>Diese Segmente für die Berichterstellung, die dem Medien-Streamtyp zugeordnet sind, wurden am 13.9.18 zusammen mit dem `streamType`-Parameter eingeführt.

| Segment | Beschreibung | Regel |
|---|---|---|
| Medien-Streamingtyp: Alle | Segmentieren aller *Medien*-Stream-Daten | &quot;Content (ID) exists&quot; |
| Medien-Streamingtyp: Audio | Segmentieren aller *Audio*-Stream-Daten | &quot;Content (ID) exists&quot; UND &quot;Media Stream Type = `audio`&quot; |
| Medien-Streamingtyp: Video | Segmentieren aller *Video*-Stream-Daten | &quot;Content (ID) exists&quot; UND &quot;Media Stream Type != `audio`&quot; |
| Medien-Content-Typ: VoD | Segmentieren aller VoD-Inhalte | &quot;Content-Typ = `vod`&quot; |
| Medien-Content-Typ: Live | Segmentieren aller Live-Inhalte | &quot;Content-Typ = `live`&quot; |
| Medien-Content-Typ: Linear | Segmentieren aller linearen Inhalte | &quot;Content-Typ = `linear`&quot; |
| Medien-Content-Typ: Podcast | Segmentieren aller Podcast-Inhalte | &quot;Content-Typ = `podcast`&quot; |
| Medien-Content-Typ: Audiobook | Segmentieren aller Audiobook-Inhalte | &quot;Content-Typ = `audiobook`&quot; |
| Medien-Content-Typ: AoD | Segmentieren aller AoD-Inhalte | &quot;Content-Typ = `aod`&quot; |

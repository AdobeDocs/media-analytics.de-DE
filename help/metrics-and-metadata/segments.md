---
title: Segmente
description: '"Erfahren Sie mehr über die Berichterstellungssegmente, die mit dem Medien-Streamtyp verknüpft sind, einschließlich Segment, Beschreibung und Regel für den Medien-Streamtyp."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentierung"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 84%

---

# Segmente{#segments}

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

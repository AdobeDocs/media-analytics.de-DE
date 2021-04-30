---
title: Segmente
description: Segmente
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '125'
ht-degree: 100%

---

# Segmente {#segments}

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

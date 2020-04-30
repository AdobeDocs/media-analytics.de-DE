---
title: Segmente
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

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


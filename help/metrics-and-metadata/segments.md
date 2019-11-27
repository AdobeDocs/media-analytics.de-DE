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
| Medien-Streamtyp: Alle | Segmentieren aller Daten des *Medienstreams* | „Content (ID) exists“ |
| Medien-Streamtyp: Audio | Segmentieren aller Daten des *Audiostreams* | „Content (ID) exists“ UND „Media Stream Type = `audio`“ |
| Medien-Streamtyp: Video | Segmentieren aller Daten des *Videostreams* | „Content (ID) exists“ UND „Media Stream Type != `audio`“ |
| Medien-Content-Typ: VoD | Segmentieren aller VoD-Inhalte | "Content-Typ = `vod`" |
| Medien-Content-Typ: Live | Segmentieren aller Live-Inhalte | "Content-Typ = `live`" |
| Medien-Content-Typ: Linear | Segmentieren aller linearen Inhalte | "Content-Typ = `linear`" |
| Medien-Content-Typ: Podcast | Segmentieren aller Podcast-Inhalte | "Content-Typ = `podcast`" |
| Medien-Content-Typ: Hörbuch | Segmentieren aller Hörbuch-Inhalte | "Content-Typ = `audiobook`" |
| Medien-Content-Typ: AoD | Segmentieren aller AoD-Inhalte | "Content-Typ = `aod`" |


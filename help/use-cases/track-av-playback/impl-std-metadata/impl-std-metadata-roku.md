---
title: Erfahren Sie, wie Sie Standard-Metadaten in Roku implementieren.
description: Erfahren Sie, wie Sie Standard-Video- und Anzeigenmetadaten festlegen, die mit Tracking-Aufrufen in Roku gesendet werden.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# Standard-Metadaten in Roku implementieren{#implement-standard-metadata-on-roku}

Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und legen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt fest.

**Video:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

**Audio:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

Sehen Sie hier die umfassende Liste der verfügbaren Video-Metadaten: [Audio- und Videoparameter](/help/implementation/variables/audio-video-parameters.md)

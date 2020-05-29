---
title: Implementieren von Standard-Metadaten mit JavaScript 3.x
description: Beschreibt das Festlegen von Standard-Video- und Anzeigenmetadaten, die mit Tracking-Aufrufen in Browser-Anwendungen (JS) gesendet werden.
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# Implementieren von Standard-Metadaten mit JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementierung

Instanziieren Sie ein Kontextdatenobjekt und füllen Sie die gewünschten Standard-Metadatenvariablen aus. Beispiel:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```

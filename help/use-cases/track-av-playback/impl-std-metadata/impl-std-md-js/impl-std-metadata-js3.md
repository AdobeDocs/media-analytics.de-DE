---
title: Erfahren Sie, wie Sie Standard-Metadaten mit JavaScript 3.x implementieren.
description: Erfahren Sie, wie Sie Standard-Video- und Anzeigenmetadaten festlegen, die mit Tracking-Aufrufen in Browser-Apps (JS 3.x) gesendet werden.
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '48'
ht-degree: 100%

---

# Implementieren von Standard-Metadaten mit JavaScript 3.x {#implement-standard-metadata-on-javascript}

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

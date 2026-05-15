---
title: Im Fokus
description: Verfolgen Sie, wann der Player im Fokus auf dem Bildschirm des Viewers ist, damit das Backend Fokusinteraktionen melden kann.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 8%

---


# Im Fokus

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für den Player **Status „Im Fokus**behandelt. Siehe [Von im Fokus betroffene Streams](/help/reporting/metrics/in-focus-streams-impacted.md), [Anzahl der Fokussierungen](/help/reporting/metrics/in-focus-count.md) und [Gesamtdauer des Fokus](/help/reporting/metrics/in-focus-total-duration.md) für die entsprechenden Berichtsmetriken.*

>[!ENDSHADEBOX]

Der Player-Status im Fokus verfolgt, wann der Player die Aufmerksamkeit des Viewers hat. Lösen Sie ein Statusstart-Ereignis aus, wenn der Player den Fokus erhält (normalerweise, wenn die Player-Registerkarte oder das Player-Fenster aktiv wird), und ein Statusend-Ereignis, wenn der Player den Fokus verliert. Das Backend berechnet drei Metriken aus diesen Ereignissen: betroffene Streams, Anzahl der Statuseinträge und Gesamtzeit im Status.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariablen** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **XDM-Sammlungsfeld** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) und [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (Einträge mit `name: "inFocus"`) |
| **Audience Manager-Eigenschaften** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [State start](/help/implementation/events/player-state/state-start.md), [state end](/help/implementation/events/player-state/state-end.md) |

## Web SDK

Verwenden Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) , um ein `media.statesUpdate`-Ereignis mit dem Status zu senden, der `statesStart` hinzugefügt wurde:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Wenn der Player den Fokus verliert, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.IN_FOCUS`.

**iOS (SWIFT)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Verwenden Sie `sendMediaEvent` , um ein `media.statesUpdate`-Ereignis mit dem Status zu senden, der `statesStart` hinzugefügt wurde:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

Wenn der Player den Fokus verliert, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## Media Edge-API

Rufen Sie den [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)-Endpunkt mit `inFocus` in `statesStart` auf (oder `statesEnd`, wenn der Player den Fokus verliert):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Medien-SDK

Verwenden Sie `ADB.Media.createStateObject` und die `ADB.Media.PlayerState.InFocus` Konstante:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Mediensammlungs-API

Senden Sie eine `stateStart` POST-Anfrage, wenn der Player den Fokus erhält, und einen `stateEnd` POST, wenn er den Fokus verliert:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .

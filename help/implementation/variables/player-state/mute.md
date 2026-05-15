---
title: Stummschaltung
description: Verfolgen Sie, wann der Viewer Audio stumm schaltet und die Stummschaltung aufhebt, damit das Backend Interaktionen melden kann.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 10%

---


# Stummschaltung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für den Player **Status „Stumm**&#x200B;behandelt. Siehe [Von Stummschaltung betroffene Streams](/help/reporting/metrics/mute-streams-impacted.md), [Stummschaltungsanzahl](/help/reporting/metrics/mute-count.md) und [Stummschaltungsgesamtdauer](/help/reporting/metrics/mute-total-duration.md) für die entsprechenden Berichtsmetriken.*

>[!ENDSHADEBOX]

Der Status des Stummschaltungs-Players verfolgt, wann der Viewer Audio stummschaltet und die Stummschaltung aufhebt. Lösen Sie ein Statusstartereignis aus, wenn der Viewer stumm geschaltet wird, und ein Statusendereignis, wenn die Stummschaltung des Viewers aufgehoben wird. Das Backend berechnet drei Metriken aus diesen Ereignissen: betroffene Streams, Anzahl der Statuseinträge und Gesamtzeit im Status.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariablen** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **XDM-Sammlungsfeld** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-collection-details) und [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-collection-details) (Einträge mit `name: "mute"`) |
| **Audience Manager-Eigenschaften** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [State start](/help/implementation/events/player-state/state-start.md), [state end](/help/implementation/events/player-state/state-end.md) |

## Web SDK

Verwenden Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) , um ein `media.statesUpdate`-Ereignis mit dem Status zu senden, der `statesStart` hinzugefügt wurde:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Wenn die Stummschaltung des Viewers aufgehoben wird, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.MUTE`.

**iOS (SWIFT)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

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
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

Wenn die Stummschaltung des Viewers aufgehoben wird, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) mit `mute` in `statesStart` auf (oder `statesEnd`, wenn die Stummschaltung des Viewers aufgehoben wird):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Medien-SDK

Verwenden Sie `ADB.Media.createStateObject` und die `ADB.Media.PlayerState.Mute` Konstante:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Mediensammlungs-API

Senden Sie eine `stateStart` POST-Anfrage, wenn der Viewer stummgeschaltet wird, und eine `stateEnd` POST, wenn die Stummschaltung aufgehoben wird:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .

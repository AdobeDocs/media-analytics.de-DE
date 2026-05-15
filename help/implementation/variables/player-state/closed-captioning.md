---
title: Untertitel
description: Verfolgen Sie, wann der Viewer geschlossene Untertitel aktiviert und deaktiviert, damit das Backend Untertitelinteraktionen melden kann.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 9%

---


# Untertitel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für den Player-Status **Untertitel**&#x200B;behandelt. Siehe [Von geschlossenen Untertiteln betroffene Streams](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Geschlossene Untertitelanzahl](/help/reporting/metrics/closed-captioning-count.md) und [Geschlossene Untertitelgesamtdauer](/help/reporting/metrics/closed-captioning-total-duration.md) für die entsprechenden Berichtsmetriken.*

>[!ENDSHADEBOX]

Der Player-Status für Untertitel verfolgt, wann der Viewer Untertitel aktiviert und deaktiviert. Löst ein Statusstartereignis aus, wenn Beschriftungen aktiviert sind, und ein Statusendeereignis, wenn Beschriftungen deaktiviert sind. Das Backend berechnet drei Metriken aus diesen Ereignissen: betroffene Streams, Anzahl der Statuseinträge und Gesamtzeit im Status.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariablen** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **XDM-Sammlungsfeld** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) und [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (Einträge mit `name: "closedCaptioning"`) |
| **Audience Manager-Eigenschaften** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [State start](/help/implementation/events/player-state/state-start.md), [state end](/help/implementation/events/player-state/state-end.md) |

## Web SDK

Verwenden Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) , um ein `media.statesUpdate`-Ereignis mit dem Status zu senden, der `statesStart` hinzugefügt wurde:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Wenn der Viewer Untertitel deaktiviert, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.CLOSED_CAPTION`.

**iOS (SWIFT)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

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
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

Wenn der Viewer Untertitel deaktiviert, senden Sie ein weiteres Ereignis mit dem Status in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

## Media Edge-API

Rufen Sie den [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)-Endpunkt mit `closedCaptioning` in `statesStart` auf (oder `statesEnd`, wenn der Viewer Untertitel deaktiviert):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Medien-SDK

Verwenden Sie `ADB.Media.createStateObject` und die `ADB.Media.PlayerState.ClosedCaptioning` Konstante:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Mediensammlungs-API

Senden Sie eine `stateStart` POST-Anfrage, wenn Beschriftungen aktiviert sind, und einen `stateEnd` POST, wenn sie deaktiviert sind:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .

---
title: Untertitel
description: Verfolgen Sie, wann der Viewer geschlossene Untertitel aktiviert und deaktiviert, damit das Backend Untertitelinteraktionen melden kann.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%
---

# Untertitel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für den Player-Status **Untertitel**&#x200B;behandelt. Siehe [Von geschlossenen Untertiteln betroffene Streams](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Geschlossene Untertitelanzahl](/help/reporting/metrics/closed-captioning-count.md) und [Geschlossene Untertitelgesamtdauer](/help/reporting/metrics/closed-captioning-total-duration.md) für die entsprechenden Berichtsmetriken.*

>[!ENDSHADEBOX]

Der Player-Status für Untertitel verfolgt, wann der Viewer Untertitel aktiviert und deaktiviert. Löst ein Statusstartereignis aus, wenn Beschriftungen aktiviert sind, und ein Statusendeereignis, wenn Beschriftungen deaktiviert sind. Das Backend berechnet drei Metriken aus diesen Ereignissen: betroffene Streams, Anzahl der Statuseinträge und Gesamtzeit im Status.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariablen** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) und [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (Einträge mit `name: "closedCaptioning"`) |
| **Audience Manager-Eigenschaften** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [State start](/help/implementation/events/player-state/state-start.md), [state end](/help/implementation/events/player-state/state-end.md) |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.CLOSED_CAPTION`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.CLOSED_CAPTION`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Verwenden Sie `ADB.Media.createStateObject` und die `ADB.Media.PlayerState.ClosedCaptioning` Konstante:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.createStateObject` direkt mit der `"closedCaptioning"` Zeichenfolge, da Chromecast keine benannten `PlayerState` enthält:

```javascript
var stateObject = ADBMobile.media.createStateObject("closedCaptioning");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer disables captions:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Player-Status-Tracking ist in der Roku 2.x-SDK nicht verfügbar. Verwenden Sie zum Nachverfolgen der Player-Status [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB Media Collection API]

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

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]

---
title: Im Fokus
description: Verfolgen Sie, wann der Player im Fokus auf dem Bildschirm des Viewers ist, damit das Backend Fokusinteraktionen melden kann.
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
source-wordcount: '354'
ht-degree: 6%
---

# Im Fokus

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für den Player **Status „Im Fokus**&#x200B;behandelt. Siehe [Von im Fokus betroffene Streams](/help/reporting/metrics/in-focus-streams-impacted.md), [Anzahl der Fokussierungen](/help/reporting/metrics/in-focus-count.md) und [Gesamtdauer des Fokus](/help/reporting/metrics/in-focus-total-duration.md) für die entsprechenden Berichtsmetriken.*

>[!ENDSHADEBOX]

Der Player-Status im Fokus verfolgt, wann der Player die Aufmerksamkeit des Viewers hat. Lösen Sie ein Statusstart-Ereignis aus, wenn der Player den Fokus erhält (normalerweise, wenn die Player-Registerkarte oder das Player-Fenster aktiv wird), und ein Statusend-Ereignis, wenn der Player den Fokus verliert. Das Backend berechnet drei Metriken aus diesen Ereignissen: betroffene Streams, Anzahl der Statuseinträge und Gesamtzeit im Status.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariablen** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) und [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (Einträge mit `name: "inFocus"`) |
| **Audience Manager-Eigenschaften** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
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

>[!TAB iOS]

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.IN_FOCUS`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Verwenden Sie `tracker.trackPlayerStateStart()` und `tracker.trackPlayerStateEnd()` mit der `MediaConstants.PlayerState.IN_FOCUS`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Verwenden Sie `ADB.Media.createStateObject` und die `ADB.Media.PlayerState.InFocus` Konstante:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.createStateObject` direkt mit der `"inFocus"` Zeichenfolge, da Chromecast keine benannten `PlayerState` enthält:

```javascript
var stateObject = ADBMobile.media.createStateObject("inFocus");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the player loses focus:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Player-Status-Tracking ist in der Roku 2.x-SDK nicht verfügbar. Verwenden Sie zum Nachverfolgen der Player-Status [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB Media Collection API]

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

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]

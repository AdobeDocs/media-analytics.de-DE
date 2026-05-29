---
title: XDM-Berichtsschema
description: Erfahren Sie, welche Media Edge-API-Ereignisse Erlebnisereignisse in Adobe Experience Platform generieren und wie Sie Ihre Implementierung mithilfe des MediaReporting-XDM-Schemas validieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 267532dfbe6dc3f7bcff0991536ae3baf6eff053
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 4%

---


# XDM-Berichtsschema

Wenn Sie Medien-Tracking-Ereignisse mit der Adobe Experience Platform Edge Network senden, verarbeitet das Media Analytics-Backend diese Ereignisse und schreibt berechnete Erlebnisereignisse in Platform-Datensätze. Wenn Sie verstehen, welche Ereignisse Platform erreichen und was das Backend für Sie berechnet, können Sie Ihre Implementierung validieren und präzise Berichte in Customer Journey Analytics oder Adobe Analytics erstellen.

In verschiedenen Teilen der Erfassungs- und Reporting-Pipeline werden zwei verschiedene XDM-Schemata verwendet:

| Schema | Namespace | Richtung | Zweck |
|---|---|---|---|
| Mediensammlung | `xdm.mediaCollection` | Client → Adobe | Was Ihr Player für jedes Tracking-Ereignis sendet. Verwendet von [Variablen](/help/implementation/variables/). |
| Medienberichte | `xdm.mediaReporting` | Adobe → Platform | Was das Backend nach der Verarbeitung in Datensätze schreibt. Wird von [Dimensionen](/help/reporting/dimensions/overview.md) und [Metriken](/help/reporting/metrics/overview.md) verwendet. |

Felder, die in `mediaReporting` vorhanden sind, aber in der `mediaCollection`-Payload nicht vorhanden sind, werden aus der vollständigen Ereignissequenz einer Sitzung abgeleitet. Diese Felder werden nie gesendet, sondern von Adobe generiert.

## Ereignisse, die in Platform-Datensätze schreiben

Von den 12 verfolgbaren Ereignistypen generieren nur fünf individuelle Erlebnisereignis-Schreibvorgänge in Datensätze:

| Ereignistyp | In Datensätzen enthalten | Hinweise |
|---|---|---|
| [Sitzungsstart](/help/implementation/events/session/session-start.md) | Ja | Wird bei Initialisierung der Sitzung geschrieben |
| [Anzeigenstart](/help/implementation/events/ads/ad-start.md) | Ja | Wird geschrieben, wenn eine einzelne Anzeige beginnt |
| [Anzeige abgeschlossen](/help/implementation/events/ads/ad-complete.md) | Ja | Wird geschrieben, wenn eine Anzeige bis zum Abschluss wiedergegeben wird |
| [Kapitel abgeschlossen](/help/implementation/events/chapters/chapter-complete.md) | Ja | Wird geschrieben, wenn ein Kapitel bis zum Ende abgespielt wird |
| [Sitzung abgeschlossen](/help/implementation/events/session/session-complete.md) | Ja | Geschrieben, wenn die Sitzung beendet wird; umfangreichster Satz berechneter Felder |
| [Play](/help/implementation/events/playback/play.md) | Nein | Zur Berechnung von `timePlayed` |
| [Start anhalten](/help/implementation/events/playback/pause-start.md) | Nein | Wird zur Berechnung von `pauseCount` und `pauseTime` verwendet |
| [Ping](/help/implementation/events/playback/ping.md) | Nein | Heartbeat; wird zur Erkennung von Sitzungsinaktivität verwendet |
| [Pufferstart](/help/implementation/events/playback/buffer-start.md) | Nein | Zur Berechnung von QoE-Puffermetriken |
| [Bitratenänderung](/help/implementation/events/playback/bitrate-change.md) | Nein | Zur Berechnung von QoE-Bitraten-Metriken |
| [Bundesland-Start](/help/implementation/events/player-state/state-start.md) | Nein | Wird zur Berechnung von Player-Statusmetriken verwendet |
| [Fehler](/help/implementation/events/error.md) | Nein | Wird zur Berechnung von `errorCount` in QoE verwendet |

## Backend-berechnete Felder

Die folgenden Felder werden in `mediaReporting` Payloads angezeigt, sind jedoch nie Teil der Sammlungs-Payload. Das Backend leitet sie aus der vollständigen Ereignissequenz ab.

**Sitzungsebene** (erscheint auf der `sessionComplete`):

| Feld | Beschreibung |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | Gesamtsekunden des abgespielten Hauptinhalts ohne Anzeigen |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | Verstrichene Sekunden insgesamt, einschließlich Anzeigen |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | Deduplizierte Sekunden - Intervalle, die mehrmals angezeigt werden, werden nur einmal gezählt |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed` geteilt durch Inhaltslänge |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | Geschätzte gleichzeitige Streams |
| `xdm.mediaReporting.sessionDetails.adCount` | Anzahl der gestarteten Anzeigen |
| `xdm.mediaReporting.sessionDetails.chapterCount` | Anzahl der gestarteten Kapitel |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | Pausenfrequenz und gesamte Pausendauer |
| `xdm.mediaReporting.sessionDetails.hasProgress10` … `xdm.mediaReporting.sessionDetails.hasProgress95` | Markierung für Fortschritt-Milestone (10 %, 25 %, 50 %, 75 %, 95 %) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | Ob mindestens ein Frame des Inhalts angezeigt wurde |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | Fertigstellungs- und Start-Flags |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | Zeit zwischen dem letzten Ping und dem Schließen der Sitzung |
| `xdm.mediaReporting.sessionDetails.segment` | Inhaltssegmentklammer (z. B. `[0-1]`) |

**Anzeigenebene** (auf `adComplete` angezeigt):

| Feld | Beschreibung |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | Sekunden des wiedergegebenen Anzeigeninhalts |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | Ob die Anzeige bis zum Ende abgespielt wurde |

**Kapitelebene** (wird auf `chapterComplete` angezeigt):

| Feld | Beschreibung |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | Sekunden des wiedergegebenen Kapitelinhalts |
| `xdm.mediaReporting.chapterDetails.isCompleted` | Gibt an, ob das Kapitel bis zum Ende abgespielt wurde |
| `xdm.mediaReporting.chapterDetails.isStarted` | Ob das Kapitel begonnen hat |

**QoE** (aggregiert auf `sessionComplete`):

| Feld | Beschreibung |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | Durchschnittliche Bitrate über die gesamte Sitzung |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | Bereich mit gepackter durchschnittlicher Bitrate |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | Anzahl der Bitratenänderungen |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | Fehleranzahl |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | Insgesamt verworfene Frames |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | Array von Player-Fehlercodes |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Ob ein Fehler aufgetreten ist |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Ob Frames gelöscht wurden |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Ob Bitratenänderungen aufgetreten sind |

## Heruntergeladene Inhalte

Bei Sitzungen, die mit dem [heruntergeladenen Endpunkt](/help/use-cases/track-downloaded-content.md) verfolgt werden, setzt das Backend `xdm.mediaReporting.sessionDetails.isDownloaded` automatisch auf `true` im `sessionStart`. Alle anderen Berichterstellungsereignisse für heruntergeladene Sitzungen folgen demselben Schema wie Live-Sitzungen. Verwenden Sie dieses Feld in CJA oder Adobe Analytics, um die heruntergeladene Wiedergabe zu filtern oder zu segmentieren.

Weitere Informationen zur [&#x200B; finden Sie &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/)Downloaded Endpoint) in der Media Edge-API-Referenz.

## Validieren der Implementierung

Nachdem Sie über die Media Edge-API Ereignisse gesendet haben, überprüfen Sie mit einer der folgenden Methoden, ob Ihre Daten korrekt gelandet sind:

**Vorschau des Adobe Experience Platform-Datensatzes**

1. Navigieren [CX Enterprise](https://experience.adobe.com) zu **[!UICONTROL Datensätze]** und wählen Sie Ihren Streaming-Medien-Datensatz aus.
2. Wählen Sie **[!UICONTROL Vorschau des Datensatzes]** aus, um die zuletzt aufgenommenen Erlebnisereignisse anzuzeigen.
3. Vergewissern Sie sich, dass `eventType` Werte wie `media.sessionStart` und `media.sessionComplete` mit ausgefüllten `mediaReporting` angezeigt werden.

**Überprüfung von Customer Journey Analytics-Datensätzen**

1. Öffnen Sie in CJA die Verbindung, die mit Ihrem Streaming-Medien-Datensatz verknüpft ist.
2. Wählen Sie **Datensätze hinzufügen** und überprüfen Sie das Schema, um zu bestätigen, dass die `mediaReporting` Felder den erwarteten Dimensionen und Metriken zugeordnet sind.

**Adobe Analytics-Verarbeitungsregeln (bei Verwendung des Analytics-Ziels)**

Für Adobe Analytics Report Suites, die Daten über den Analytics-Quell-Connector erhalten, können Sie Verarbeitungsregeln verwenden, um `mediaReporting` Kontextdatenvariablen benutzerdefinierten Props oder eVars zuzuordnen. Die `isDownloaded`-Markierung ist als `a.media.downloaded` verfügbar.

## Beispiele für XDM-Payloads

Die folgenden Beispiele zeigen die vollständige `mediaReporting` XDM-Struktur für jedes Berichterstellungsereignis, das in Platform-Datensätze geschrieben wurde. Die `_{tenantName}`-Eigenschaft stellt den Mandanten-Namespace Ihres Unternehmens für alle benutzerdefinierten Felder dar.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (heruntergeladener Inhalt)

Sitzungen, die mit dem [heruntergeladenen Endpunkt](/help/use-cases/track-downloaded-content.md) verfolgt werden, folgen demselben Berichtsschema mit einem Hauptunterschied: `xdm.mediaReporting.sessionDetails.isDownloaded` ist auf `true` für das `sessionStart` Berichterstellungsereignis festgelegt. Alle anderen Ereignistypen sind mit den obigen Live-Inhaltsbeispielen identisch.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++

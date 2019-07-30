---
seo-title: 'Zeitlicher Ablauf 1: Wiedergabe bis zum Ende des Inhalts'
title: 'Zeitlicher Ablauf 1: Wiedergabe bis zum Ende des Inhalts'
uuid: 0 ff 591 d 3-fa 99-4123-9 e 09-c 4 e 71 ea 1060 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Zeitlicher Ablauf 1: Wiedergabe bis zum Ende des Inhalts{#timeline-view-to-end-of-content}

## VOD, Pre-Roll-Anzeigen, Pausen, Puffern, Wiedergabe des Inhalts bis zum Ende

Die folgenden Diagramme illustrieren die Timeline der Abspielleiste und die Zeitschiene der Zeitleiste eines Benutzers. Die Details zu den einzelnen Aktionen und den zugehörigen Anforderungen werden unten angezeigt.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Aktionsdetails

### Action 1 - Start session {#Action-1}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Automatische Wiedergabe oder Betätigung der Play-Schaltfläche; Video wird geladen. | 0 | 0 | `/api/v1/sessions` |

**Implementierungsdetails**

Dieser Aufruf signalisiert _die Anwenderintention, ein Video abzuspielen_. <br/><br/>Er gibt eine Sitzungs-ID ( `{sid}`) an den Client zurück, mit dem alle nachfolgenden Verfolgungsaufrufe innerhalb der Sitzung identifiziert werden. Der Player-Status lautet noch nicht „Playing“ (Wiedergabe), sondern „Starting“ (Start). <br/><br/>[Erforderliche Sitzungsparameter](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) müssen in der `params`-Map des Anfrageinhalts angegeben werden. <br/><br/>Am Backend generiert dieser Aufruf einen Adobe Analytics-Initiationsaufruf.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0, ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Action 2 - Ping timer start {#Action-2}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung startet Ping-Ereignis-Timer. | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Implementierungsdetails**

Starten Sie den Ping-Timer Ihrer App. Das erste ping-Ereignis sollte dann 1 Sekunde in auslösen, wenn Pre-Roll-Anzeigen vorhanden sind, andernfalls 10 Sekunden.

### Action 3 - Ad break start {#Action-3}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Start der Pre-Roll-Werbeunterbrechung wird verfolgt. | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Anzeigen können nur innerhalb einer Werbeunterbrechung verfolgt werden.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Action 4 - Ad start {#Action-4}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Start der ersten Pre-Roll-Anzeige wird verfolgt. | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Beginnen Sie mit dem Tracking der ersten Pre-Roll-Anzeige, die 15 Sekunden dauert, einschließlich anwenderspezifischer Metadaten mit diesem `adStart` .

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: &lt;timestamp&gt;
    },
    eventType:adStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Action 5 - Ad pings {#Action-5}

#### Action 5.1 - Ad ping 1 {#Action-5-1}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ping des Backend alle 1 Sekunde innerhalb einer Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Action 5.2 - Ad ping 2 {#Action-5-2}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ping des Backend alle 1 Sekunde innerhalb einer Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Action 5.3 - Ad ping 3 {#Action-5-3}


| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ping des Backend alle 1 Sekunde innerhalb einer Anzeige.

>[!NOTE]
>
>Nachfolgende Anzeigen in der Zeitleiste überspringen die Anzeige der einzweiseligen Pings.
>im Interesse der Treue…

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 6 - Ad complete {#Action-6}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Abschluss der ersten Pre-Roll-Anzeige wird verfolgt. | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie das Ende der ersten Pre-Roll-Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 7 - Ad start {#Action-7}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Start der zweiten Pre-Roll-Anzeige wird verfolgt. | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie den Start der zweiten Pre-Roll-Anzeige, die 7 Sekunden lang ist.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 8 - Ad pings {#Action-8}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ping des Backend alle 1 Sekunde.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 9 - Ad complete {#Action-9}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Abschluss der zweiten Pre-Roll-Anzeige wird verfolgt. | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie das Ende der zweiten Pre-Roll-Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 10 - Ad break complete {#Action-10}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Abschluss der Pre-Roll-Werbeunterbrechung wird verfolgt. | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Die Werbeunterbrechung ist vorüber. Während der Werbeunterbrechung wurde der Status „Playing“ (Wiedergabe) beibehalten.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 11 - Play content {#Action-11}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Wiedergabeereignis wird verfolgt. | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Versetzen Sie den Player nach dem Ereignis `adBreakComplete` mit dem Ereignis `play`-Ereignis in den Status „Playing“ (Wiedergabe).

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 12 - Ping {#Action-12}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 13 - Buffer start {#Action-13}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Pufferstartereignis aufgetreten. | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie den Wechsel des Players zum Status „Buffering“ (Puffern).

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Action 14 - Buffer end {#Action-14}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Puffern abgeschlossen; die Anwendung setzt den Inhalt fort. | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Puffern endet nach 3 Sekunden, sodass der Player wieder zum Status „Playing“ (Wiedergabe) wechselt. Sie müssen am Ende des Puffervorgangs ein weiteres Ereignis zum Verfolgen der Wiedergabe senden.  **Der`play`Aufruf nach dem`bufferStart`Aufrufen eines "buffstext" -Aufrufs am Backend, sodass** kein `bufferEnd` Ereignis benötigt wird.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 15 - Ping {#Action-15}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 16 - Ad break start {#Action-16}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Start der Mid-Roll-Werbeunterbrechung wird verfolgt. | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Mid-Roll-Anzeige mit einer Dauer von 8 Sekunden: Senden Sie `adBreakStart` .

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Action 17 - Ad start {#Action-17}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Start der dritten Mid-Roll-Anzeige wird verfolgt. | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie die Mid-Roll-Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 18 - Ad ping {#Action-18}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 19 - Ad complete {#Action-19}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Abschluss der ersten Mid-Roll-Anzeige wird verfolgt. | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Die Mid-Roll-Anzeige ist abgeschlossen.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 20 - Ad break complete {#Action-20}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Abschluss der Mid-Roll-Werbeunterbrechung wird verfolgt. | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Die Werbeunterbrechung ist abgeschlossen.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 21 - Ping {#Action-21}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 22 - Pause {#Action-22}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwender betätigt Pause-Schaltfläche. | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Durch die Anwenderaktion wechselt der Wiedergabestatus zu „Paused“ (Pause).

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Action 23 - Ping {#Action-23}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend. Der Player befindet sich weiterhin im Status „buffering“ (Puffern); der Nutzer hängt bei 20 Sekunden des Inhalts fest und ist frustriert.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 24 - Play {#Action-24}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwender betätigt Play-Schaltfläche, um Hauptinhalt fortzusetzen. | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ändern Sie den Wiedergabestatus zu „playing“ (Wiedergabe).  **Der`play`Aufruf nach dem`pauseStart`Aufrufen eines "Fortsetzen" -Aufrufs an das Backend,** sodass kein `resume` Ereignis benötigt wird.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Action 25 - Ping {#Action-25}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 26 - Session complete {#Action-26}

| Aktion | Aktionsablauf (Sekunden) | Abspielposition (Sekunden) | Clientanfrage |
| --- | :---: | :---: | --- |
| Anwender sieht sich Inhalt bis zum Ende an. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie `sessionComplete` an das Backend, um anzugeben, dass der Anwender den gesamten Inhalt abgespielt hat.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    }, eventType:sessionComplete
}
```

>[!NOTE]
>
>**Keine Suchereignisse? -** Die Mediensammlungs-API unterstützt die Ereignisse `seekStart` und `seekComplete` nicht explizit. Das liegt daran, dass bestimmte Player eine große Anzahl solcher Ereignisse generieren, wenn der Anwender durch das Video springt. So können einige Hunderte von Anwendern schnell die Netzwerkbandbreite des Backend-Service überlasten. Adobe umgeht die explizite Unterstützung von Suchereignissen durch die Berechnung einer Heartbeat-Dauer basierend auf dem Gerätezeitstempel statt auf der Abspielposition.


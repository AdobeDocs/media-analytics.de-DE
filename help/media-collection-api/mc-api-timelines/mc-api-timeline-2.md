---
title: Erfahren Sie mehr über die Zeitpläne für die Medienverfolgung � Verlassen der Sitzung durch Anwender
description: Erfahren Sie mehr über die Zeitleiste der Abspielleiste und die Aktion der entsprechenden Benutzer �, wenn eine Videositzung abgebrochen wird. Erfahren Sie mehr über die Details für jede Aktion und jede Anfrage.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 95%

---

# Zeitlicher Ablauf 2: Verlassen der Sitzung durch Anwender {#timeline--2-user-abandons-session}

## VOD, Pre-Roll-Anzeige, Mid-Roll-Anzeigen, Anwender verlässt Inhalt schnell

Die folgenden Diagramme illustrieren die Zeitleiste der Abspielleiste und die zugehörige Zeitleiste der Aktionen eines Benutzers. Die Details für jede Aktion und die zugehörigen Anforderungen sind unten aufgeführt.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Aktionsdetails

### Aktion 1: Sitzung starten {#Action-1}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Button zur automatischen Wiedergabe oder zur Wiedergabe gedrückt | 0 | 0 | `/api/v1/sessions` |

**Implementierungsdetails**

Dieser Aufruf signalisiert _die Anwenderintention, ein Video abzuspielen_. Er gibt eine Sitzungs-ID (`{sid}`) an den Client zurück, die zur Identifikation aller nachfolgenden Tracking-Aufrufe innerhalb der Sitzung verwendet wird. Der Player-Status lautet noch nicht „Playing“ (Wiedergabe), sondern „Starting“ (Start).  [Erforderliche Sitzungsparameter](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) müssen in der `params`-Map des Anfrageinhalts angegeben werden.  Am Backend generiert dieser Aufruf einen Adobe Analytics-Initiationsaufruf.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Aktion 2: Start des Ping-Timers {#Action-2}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| App startet Ping-Ereignis-Timer | 0 | 0 |  |

**Implementierungsdetails**

Starten Sie den Ping-Timer Ihrer App. Das erste Ping-Ereignis sollte dann nach 1 Sekunde ausgelöst werden, wenn Pre-Roll-Anzeigen vorhanden sind, andernfalls nach 10 Sekunden.

### Aktion 3: Start der Werbeunterbrechung {#Action-3}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Starts der Pre-Roll-Anzeigenunterbrechung | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Pre-Roll-Anzeigen müssen verfolgt werden. Anzeigen können nur innerhalb einer Werbeunterbrechung verfolgt werden.

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

### Aktion 4: Anzeigenstart {#Action-4}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Starts der Pre-Roll-Anzeige Nr. 1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Es startet eine 12-sekündige Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Aktion 5: Anzeigen-Pings {#Action-5}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie jede Sekunde ein Ping-Ereignis an das Backend. (Nachfolgende Anzeigen-Pings werden im Interesse der Kürze nicht angezeigt.)

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

### Aktion 6: Abschluss der Anzeige {#Action-6}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Abschlusses der Pre-Roll-Anzeige Nr. 1 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Die erste Pre-Roll-Anzeige ist vorüber.

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

### Aktion 7: Abschluss der Werbeunterbrechung {#Action-7}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Abschlusses der Pre-Roll-Anzeigenunterbrechung | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Die Werbeunterbrechung ist vorüber. Während der Anzeigenunterbrechung blieb der Player im Status „Abspielen“.

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

### Aktion 8: Inhalt abspielen {#Action-8}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Wiedergabe-Ereignisses | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Ändern Sie den Status des Players zu „Playing“ (Wiedergabe); beginnen Sie mit dem Tracking des Starts der Inhaltswiedergabe.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### Aktion 9: Ping {#Action-9}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Aktion 10: Ping {#Action-10}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Aktion 11: Fehler {#Action-11}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Fehler tritt auf, App sendet Fehlerinformationen | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**


**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### Aktion 12: Inhalt abspielen {#Action-12}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| App funktioniert nach Fehler wieder, Benutzer wählt „Abspielen“ | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**



**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### Aktion 13: Ping {#Action-13}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Anwendung sendet Ping-Ereignis. | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie alle 10 Sekunden Ping-Ereignisse an das Backend.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Aktion 14: Start der Werbeunterbrechung {#Action-14}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Starts der Mid-Roll-Anzeigenunterbrechung | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Mid-Roll-Anzeige mit einer Dauer von 8 Sekunden: Senden Sie `adBreakStart` .

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Aktion 15: Anzeigenstart {#Action-15}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Verfolgen des Starts der Mid-Roll-Anzeige Nr. 1 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Verfolgen Sie die Mid-Roll-Anzeige.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### Aktion 16: App schließen {#Action-16}

| Aktion | Aktions-Timeline (Sekunden) | Abspielleistenposition (Sekunden) | Client-Anfrage |
| --- | :---: | :---: | --- |
| Anwender schließt Anwendung; Die App stellt fest, dass der Benutzer die Anzeige abgebrochen hat und nicht zu dieser Sitzung zurückkehrt. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementierungsdetails**

Senden Sie `sessionEnd` an das VA-Backend, um anzugeben, dass die Sitzung umgehend und ohne weitere Verarbeitung geschlossen werden soll.

**Beispiel-Anfrageinhalt**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```

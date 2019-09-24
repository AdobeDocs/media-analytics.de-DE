---
seo-title: Ereignisanfrage
title: Ereignisanfrage
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Ereignisanfrage{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI-Parameter

`sid`: Die Sitzungs-ID, die von einer [Sitzungsanfrage zurückgegeben wird.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Anfrageinhalt

Die Anforderungsstelle muss JSON sein und die gleiche Struktur wie die folgende MusteranforderungsTextstelle haben:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obligatorisch)
   * `playhead`: Muss in Sekunden angegeben werden, es kann sich jedoch um einen Float-Wert handeln.
   * `ts`: Zeitstempel, der in Millisekunden angegeben werden muss.
* `eventType` (Obligatorisch)
* `params` (Optional)
* `customMetadata` (Optional) Nur senden mit `adStart` und `chapterStart` Ereignistypen)
* `qoeData` (Optional)

Eine Liste gültiger Ereignistypen für diese Version finden Sie unter [Ereignistypen und -beschreibungen.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Anzeigenverfolgung -**Sie können Anzeigen nur innerhalb eines`adBreak`*.
>
>Wenn Anzeigen nicht durch `adBreakStart` und `adBreakComplete` eingeschlossen sind, werden die Ereignisse `adStart` und `adComplete` einfach ignoriert und die Werbedauer wird der Dauer des Hauptinhalts angerechnet. Das kann deutliche Auswirkungen auf die aggregierten Daten haben, die in Adobe Analytics zur Verfügung stehen.

## Antwort

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP-Antwortcodes

| HTTP-Antwortcode | Beschreibung | Clientaktionselemente |
|---|---|---|
| **204** | **Kein Inhalt.** <br/><br/>Der Heartbeat-Aufruf war erfolgreich. | nicht angegeben |
| **400** | **Unzulässige Anfrage.**<br/><br/>Die Anfrage hatte ein unzulässiges Format. | Überprüfen Sie die [JSON-Validierungsschemata](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) für den Anfragetyp. |
| **404** | **nicht gefunden.** <br/><br/>Die Sitzungs-ID für die Mediensitzung wurde im Backend-Dienst nicht gefunden. | Die Client-Anwendung sollte die [Sitzungsanfrage-API](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) verwenden, um eine weitere Mediensitzung und einen Tracking-Bericht zu erstellen. |
| **410** | **Vorbei.** <br/><br/>Die Mediensitzung wurde im Back-End-Dienst gefunden, der Client kann jedoch keine Aktivität mehr darauf melden. | Die Client-Anwendung sollte die [Sitzungsanfrage-API](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) verwenden, um eine weitere Mediensitzung und einen Tracking-Bericht zu erstellen. |
| **500** | **Serverfehler** | nicht angegeben |


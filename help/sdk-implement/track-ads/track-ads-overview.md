---
seo-title: Überblick
title: Überblick
uuid: 1607798 b-c 6 ef -4 d 60-8 e 40-e 958 c 345 b 09 c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit den 2. x sdks. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Die Wiedergabe von Anzeigen beinhaltet das Tracking von Werbeunterbrechungen, Anzeigenstarts, -beendigungen und übersprungenen Anzeigen. Verwenden Sie die API des Medienplayers, um wichtige Player-Ereignisse herauszufinden und die erforderlichen und optionalen Anzeigenvariablen auszufüllen. Eine umfassende Liste der Metadaten finden Sie hier: [Anzeigenparameter.](/help/metrics-and-metadata/ad-parameters.md)

## Player-Ereignisse {#player-events}


### Beim Werbeunterbrechungsstart

>[!NOTE]
>Einschließen von Pre-Roll

* Erstellen Sie eine `adBreak`-Objektinstanz für die Werbepause. Beispiel, `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### Bei jedem Start eines Anzeigen-Assets

* Erstellen Sie eine Anzeigenobjektinstanz für das Anzeigen-Asset. Beispiel, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Rufen Sie `trackEvent` für den Anzeigenstart auf.

### Bei jedem Ende einer Anzeige:

* Rufen Sie `trackEvent` auf, um die Anzeige zu beenden.

### Beim Überspringen einer Anzeige:

* Rufen Sie `trackEvent` für das Überspringen einer Anzeige auf.

### Beim Abschluss einer Werbeunterbrechung:

* Rufen Sie `trackEvent` für das Ende der Werbeunterbrechung auf.

## Implementierung der Anzeigenverfolgung {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Anzeigen-Tracking-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `AdBreakStart` | Konstante für die Verfolgung des AdBreak Start-Ereignisses |
| `AdBreakComplete` | Konstante für die Verfolgung des AdBreak Complete-Ereignisses |
| `AdStart` | Konstante für die Verfolgung des Ad Start-Ereignisses |
| `AdComplete` | Konstante für die Verfolgung des Ad Complete-Ereignisses |
| `AdSkip` | Konstante für die Verfolgung des Ad Skip-Ereignisses |

### Implementierungsschritte

1. Ermitteln Sie, wann die Werbeunterbrechung beginnt, einschließlich Pre-Roll, und erstellen Sie ein `AdBreakObject` mithilfe dieser Pauseninformationen.

   `AdBreakObject` Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Name der Werbeunterbrechung, z. B. Pre-Roll, Mid-Roll oder Post-Roll. | Ja |
   | `position` | Positionsnummer der Werbeunterbrechung innerhalb des Inhalts, beginnend bei 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject` Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Der Anzeigename der Werbeanzeige. | Ja |
   | `adId` | Eindeutige Kennung für die Anzeige. | Ja |
   | `position` | Positionsnummer der Anzeige in der Werbeunterbrechung, beginnend bei 1. | Ja |
   | `length` | Anzeigenlänge | Ja |

1. Optional können Standard- und/oder Werbemetadaten über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Metadaten für Standardanzeigen:** Erstellen Sie für Metadaten für Standardanzeigen ein Wörterbuch der Schlüsselwertepaare für Standardanzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform.
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen.

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein.

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis.
1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zu deren Tracking das `AdBreakComplete`-Ereignis.

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie die Playhead für den Inhalts-Player (`l:event:playhead`) bei der Wiedergabe der Anzeige NICHT erhöhen (`s:asset:type=ad`). Wenn Sie dies tun, werden die Metriken "Besuchszeit pro Inhalt" negativ beeinflusst.

Der folgende Beispielcode nutzt das javascript 2. x SDK für einen HTML 5-Medienplayer.

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```


---
title: Überblick
description: Überblickt über die Implementierung des Anzeigen-Trackings mit dem Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '504'
ht-degree: 100%

---

# Überblick {#overview}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

Die Wiedergabe von Anzeigen beinhaltet das Tracking von Werbeunterbrechungen, Anzeigenstarts, -beendigungen und übersprungenen Anzeigen. Verwenden Sie die API des Medienplayers, um wichtige Player-Ereignisse zu ermitteln und die erforderlichen und optionalen Anzeigenvariablen hinzuzufügen. Sehen Sie hier die umfassende Liste der verfügbaren-Metadaten: [Anzeigenparameter.](/help/metrics-and-metadata/ad-parameters.md)

## Player-Ereignisse {#player-events}


### Beim Start einer Werbeunterbrechung

>[!NOTE]
>Einschließlich Pre-Roll

* Erstellen Sie eine `adBreak`-Objektinstanz für die Werbepause. Beispiel, `adBreakObject`.

* Rufen Sie `trackEvent` für den Start einer Werbeunterbrechung mit Ihrem `adBreakObject` auf.

### Bei jedem Start eines Anzeigen-Assets

* Erstellen Sie eine Anzeigenobjektinstanz für das Anzeigen-Asset. Beispiel, `adObject`.
* Fügen Sie die Anzeigenmetadaten hinzu: `adCustomMetadata`.
* Rufen Sie `trackEvent` für den Anzeigenstart auf.

### Bei jedem Ende einer Anzeige:

* Rufen Sie `trackEvent` auf, um die Anzeige zu beenden.

### Beim Überspringen einer Anzeige:

* Rufen Sie `trackEvent` für das Überspringen einer Anzeige auf.

### Beim Abschluss einer Werbeunterbrechung:

* Rufen Sie `trackEvent` für das Ende der Werbeunterbrechung auf.

## Implementieren des Anzeigen-Trackings {#implement-ad-tracking}

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

   `AdBreakObject`-Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Name der Werbeunterbrechung, z. B. Pre-Roll, Mid-Roll oder Post-Roll. | Ja |
   | `position` | Positionsnummer der Werbeunterbrechung innerhalb des Inhalts, beginnend bei 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

1. Rufen Sie `trackEvent()` mit `AdBreakStart` in der `MediaHeartbeat`-Instanz auf, um das Tracking der Werbeunterbrechung zu starten.

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject`-Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Der Anzeigename der Werbeanzeige. | Ja |
   | `adId` | Eindeutige Kennung für die Anzeige. | Ja |
   | `position` | Positionsnummer der Anzeige in der Werbeunterbrechung, beginnend bei 1. | Ja |
   | `length` | Anzeigenlänge | Ja |

1. Optional können Standard- und/oder Werbemetadaten über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Metadaten für Standardanzeigen:** Erstellen Sie für Metadaten für Standardanzeigen ein Wörterbuch der Schlüsselwertepaare für Standardanzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform.
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen.

1. Rufen Sie `trackEvent()` mit dem `AdStart`-Ereignis in der `MediaHeartbeat`-Instanz auf, um das Tracking der Anzeigenwiedergabe zu starten.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein.

1. Wenn die Wiedergabe der Anzeige das Ende der Anzeige erreicht, rufen Sie `trackEvent()` mit dem `AdComplete`-Ereignis auf.

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis.
1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zu deren Tracking das `AdBreakComplete`-Ereignis.

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie die Abspielleiste (`l:event:playhead`) des Inhaltsplayers während der Wiedergabe der Anzeige NICHT erhöhen (`s:asset:type=ad`). In diesem Fall werden die Metriken zur Besuchszeit für Inhalte negativ beeinflusst.

Der folgende Beispielcode nutzt das JavaScript 2.x-SDK für einen HTML5-Medienplayer.

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

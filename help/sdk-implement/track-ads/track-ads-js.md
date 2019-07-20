---
seo-title: Tracking von Anzeigen in JavaScript
title: Tracking von Anzeigen in JavaScript
uuid: 4 d 81 d 29 c-c 55 d -4 d 48-b 505-3260922712 ff
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Tracking von Anzeigen in JavaScript{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Die folgenden Anweisungen enthalten Anleitungen zur Implementierung mit den 2. x sdks. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](../../sdk-implement/download-sdks.md)

## Anzeigen-Tracking-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `AdBreakStart` | Konstante für die Verfolgung des AdBreak Start-Ereignisses |
| `AdBreakComplete` | Konstante für die Verfolgung des AdBreak Complete-Ereignisses |
| `AdStart` | Konstante für die Verfolgung des Ad Start-Ereignisses |
| `AdComplete` | Konstante für die Verfolgung des Ad Complete-Ereignisses |
| `AdSkip` | Konstante für die Verfolgung des Ad Skip-Ereignisses |

## Implementierungsschritte

1. Ermitteln Sie, wann die Werbeunterbrechung beginnt, einschließlich Pre-Roll, und erstellen Sie ein `AdBreakObject` mithilfe dieser Pauseninformationen.

   `AdBreakObject` Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Name der Werbeunterbrechung, z. B. Pre-Roll, Mid-Roll oder Post-Roll. | Ja |
   | `position` | Positionsnummer der Werbeunterbrechung, beginnend bei 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

   Erstellung von Werbeunterbrechungsobjekten:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject` Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Der Anzeigename der Werbeanzeige. | Ja |
   | `adId` | Eindeutige Kennung für die Anzeige. | Ja |
   | `position` | Positionsnummer der Anzeige in der Werbeunterbrechung, beginnend bei 1. | Ja |
   | `length` | Anzeigenlänge | Ja |

   Erstellung von Anzeigenobjekten:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Fügen Sie standardmäßig Standard- und/oder Anzeigenmetadaten über Kontextdatenvariablen an die Medienverfolgungssitzung an.

   * [Standard-Anzeigenmetadaten in JavaScript implementieren](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen:

      ```js
      /* Set custom context data */ 
      var adCustomMetadata = { 
          affiliate: "Sample affiliate", 
          campaign: "Sample ad campaign", 
          creative: "Sample creative" 
      };
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein:

   ```js
   _onAdStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata); 
   };
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```js
   _onAdComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   };
   ```

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis:

   ```js
   _onAdSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
   };
   ```

1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zum Tracking das `AdBreakComplete`-Ereignis:

   ```js
   _onAdBreakComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   };
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Pre-roll-Anzeigen](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md).

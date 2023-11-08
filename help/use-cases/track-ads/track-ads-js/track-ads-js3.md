---
title: Erfahren Sie, wie Sie Anzeigen mit JavaScript 3.x verfolgen.
description: Implementieren des Anzeigen-Trackings in Browser-Anwendungen (JS) mit dem Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 88%

---

# Nachverfolgen von Anzeigen mit JavaScript 3.x{#track-ads-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 3.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

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

   `AdBreakObject`-Referenz:

   | Variablenname | Typ | Beschreibung |
   | --- | --- | --- |
   | `name` | string | Nicht leere Zeichenfolge, die den Namen der Werbeunterbrechung angibt (Pre-Roll, Mid-Roll und Post-Roll). |
   | `position` | number | Positionsnummer der Werbeunterbrechung, beginnend bei 1. |
   | `startTime` | number | Abspielpositionswert bei Start der Werbeunterbrechung. |

   Erstellung von Werbeunterbrechungsobjekten:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Rufen Sie `trackEvent()` mit `AdBreakStart` in der `MediaHeartbeat`-Instanz auf, um das Tracking der Werbeunterbrechung zu starten:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject`-Referenz:

   | Variablenname | Typ | Beschreibung |
   | --- | --- | --- |
   | `name` | string | Nicht leere Zeichenfolge, die den Anzeigennamen angibt. |
   | `adId` | string | Nicht leere Zeichenfolge mit Anzeigenkennung. |
   | `position` | number | Positionsnummer der Anzeige in der Werbeunterbrechung, beginnend bei 1. |
   | `length` | number | Positive Zahl, die die Länge der Anzeige angibt. |

   Erstellung von Anzeigenobjekten:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. (Optional) Fügen Sie Standard- und/oder Anzeigenmetadaten über Kontextdatenvariablen an die Medien-Tracking-Sitzung an.

   * [Standard-Anzeigenmetadaten in JavaScript implementieren](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen:

     ```js
     /* Set context data */
     // Standard metadata keys provided by adobe.
     adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
     adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
     
     // Custom metadata keys
     adMetadata["affiliate"] = "Sample affiliate";
     adMetadata["campaign"] = "Sample ad campaign";
     adMetadata["creative"] = "Sample creative";
     ```

1. Rufen Sie `trackEvent()` mit dem `AdStart`-Ereignis in der `MediaHeartbeat`-Instanz auf, um das Tracking der Anzeigenwiedergabe zu starten.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Wenn die Wiedergabe der Anzeige das Ende der Anzeige erreicht, rufen Sie `trackEvent()` mit dem `AdComplete`-Ereignis auf:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zum Tracking das `AdBreakComplete`-Ereignis:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Pre-roll-Anzeigen](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

## Granulares Anzeigen-Tracking

Das standardmäßige Anzeigen-Ping-Intervall beträgt `10 seconds`.

Sie können eine detaillierte Anzeigenverfolgung einrichten, um `1 second` Anzeigen-Tracking.

>[!IMPORTANT]
>
>Diese Informationen müssen beim Starten einer Tracking-Sitzung angegeben werden.



**Syntax**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Beispiel**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```

---
title: Erfahren Sie, wie Sie Anzeigen mit JavaScript 2.x verfolgen.
description: Implementieren des Anzeigen-Trackings in Browser-Anwendungen (JS) mit dem Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ItWdBdCHpR9E0OiZNKTNaPs-3cWWrdWouHn6TP9-RWA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 91%

---

# Nachverfolgen von Anzeigen mit JavaScript 2.x{#track-ads-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

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

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Name der Anzeigenunterbrechung, z. B. Pre-roll, Mid-roll und Post-roll. | Ja |
   | `position` | Positionsnummer der Werbeunterbrechung, beginnend bei 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

   Erstellung von Werbeunterbrechungsobjekten:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Rufen Sie `trackEvent()` mit `AdBreakStart` in der `MediaHeartbeat`-Instanz auf, um das Tracking der Werbeunterbrechung zu starten:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject`-Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Der Anzeigename der Werbeanzeige. | Ja |
   | `adId` | Eindeutige Kennung für die Anzeige. | Ja |
   | `position` | Die Positionsnummer der Anzeige innerhalb der Werbeunterbrechung, beginnend mit 1. | Ja |
   | `length` | Anzeigenlänge | Ja |

   Erstellung von Anzeigenobjekten:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Optional können Standard- und/oder Anzeigenmetadaten über Kontextdatenvariablen an die Medien-Tracking-Sitzung angehängt werden.

   * [Standard-Anzeigenmetadaten in JavaScript implementieren](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen:

     ```js
     /* Set custom context data */
     var adCustomMetadata = {
         affiliate: "Sample affiliate",
         campaign: "Sample ad campaign",
         creative: "Sample creative"
     };
     ```

1. Rufen Sie `trackEvent()` mit dem `AdStart`-Ereignis in der `MediaHeartbeat`-Instanz auf, um das Tracking der Anzeigenwiedergabe zu starten.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Wenn die Wiedergabe der Anzeige das Ende der Anzeige erreicht, rufen Sie `trackEvent()` mit dem `AdComplete`-Ereignis auf:

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

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Pre-roll-Anzeigen](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

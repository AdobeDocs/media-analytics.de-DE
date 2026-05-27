---
title: Erfahren Sie, wie Sie Anzeigen in iOS verfolgen.
description: Implementieren des Anzeigen-Trackings in iOS-Anwendungen mit dem Media SDK.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
exl-id: a352bca9-bcfc-4418-b2a2-c9b1ad226359
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/4z8fq-mojLd4zzlCJsZQ7R7AOc5W59x0u-yOTpylojc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 367
ht-degree: 87%

---

# Nachverfolgen von Anzeigen auf iOS{#track-ads-on-ios}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Anzeigen-Tracking-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Konstante für die Verfolgung des AdBreak Start-Ereignisses |
| `ADBMediaHeartbeatEventAdBreakComplete` | Konstante für die Verfolgung des AdBreak Complete-Ereignisses |
| `ADBMediaHeartbeatEventAdStart` | Konstante für die Verfolgung des Ad Start-Ereignisses |
| `ADBMediaHeartbeatEventAdComplete` | Konstante für die Verfolgung des Ad Complete-Ereignisses |
| `ADBMediaHeartbeatEventAdSkip` | Konstante für die Verfolgung des Ad Skip-Ereignisses |

## Implementierungsschritte

1. Ermitteln Sie, wann die Werbeunterbrechung beginnt, einschließlich Pre-Roll, und erstellen Sie ein `AdBreakObject` mithilfe dieser Pauseninformationen.

   `AdBreakObject`-Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Name der Anzeigenunterbrechung, z. B. Pre-roll, Mid-roll und Post-roll. | Ja |
   | `position` | Die Position der Anzeigenunterbrechung im Inhalt, beginnend mit 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

   Erstellung von Werbeunterbrechungsobjekten:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME]
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Rufen Sie `trackEvent()` mit `AdBreakStart` in der `MediaHeartbeat`-Instanz auf, um das Tracking der Werbeunterbrechung zu starten:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil];
   }
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

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME]
                                    adId:[AD_ID]
                                    position:[POSITION]
                                    length:[LENGTH]];
   ```

1. Optional können Standard- und/oder Anzeigenmetadaten über Kontextdatenvariablen an die Medien-Tracking-Sitzung angehängt werden.

   * [Standard-Anzeigenmetadaten in iOS implementieren](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen:

     ```
     NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
     [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
     [adDictionary setObject:@"Sample campaign" forKey:@"campaign"];
     [adDictionary setObject:@"Sample creative" forKey:@"creative"];
     ```

1. Rufen Sie `trackEvent()` mit dem `AdStart`-Ereignis in der `MediaHeartbeat`-Instanz auf, um das Tracking der Anzeigenwiedergabe zu starten.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein:

   ```
   - (void)onAdStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary];
   }
   ```

1. Wenn die Wiedergabe der Anzeige das Ende der Anzeige erreicht, rufen Sie `trackEvent()` mit dem `AdComplete`-Ereignis auf.

   ```
   - (void)onAdComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis.

   ```
   - (void)onAdSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zum Tracking das `AdBreakComplete`-Ereignis:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Pre-roll-Anzeigen](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

---
title: Anzeigen verfolgen – Erklärung
description: Überblickt über die Implementierung des Anzeigen-Trackings mit dem Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 641
ht-degree: 62%

---

# Überblick{#overview}

Mit den folgenden Anweisungen können Sie die Implementierung unter Verwendung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

Die Wiedergabe von Anzeigen beinhaltet das Tracking von Werbeunterbrechungen, Anzeigenstarts, -beendigungen und übersprungenen Anzeigen. Verwenden Sie die API des Medienplayers, um wichtige Player-Ereignisse zu ermitteln und die erforderlichen und optionalen Anzeigenvariablen hinzuzufügen.

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
   | `name` | Name der Anzeigenunterbrechung, z. B. Pre-roll, Mid-roll und Post-roll. | Ja |
   | `position` | Die Position der Anzeigenunterbrechung im Inhalt, beginnend mit 1. | Ja |
   | `startTime` | Abspielpositionswert bei Start der Werbeunterbrechung. | Ja |

1. Rufen Sie `trackEvent()` mit `AdBreakStart` in der `MediaHeartbeat`-Instanz auf, um das Tracking der Werbeunterbrechung zu starten.

1. Ermitteln Sie, wann die Anzeige startet und erstellen Sie die `AdObject`-Instanz mithilfe dieser Anzeigeninformationen.

   `AdObject`-Referenz:

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Der Anzeigename der Werbeanzeige. | Ja |
   | `adId` | Eindeutige Kennung für die Anzeige. | Ja |
   | `position` | Die Positionsnummer der Anzeige innerhalb der Werbeunterbrechung, beginnend mit 1. | Ja |
   | `length` | Anzeigenlänge | Ja |

1. Fügen Sie optional über Kontextdatenvariablen Standard- und/oder Anzeigenmetadaten an die Tracking-Sitzung an.

   * **Standard-Anzeigenmetadaten -** Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Wert-Paare für Standard-Anzeigenmetadaten mithilfe der Schlüssel für Ihre Plattform.
   * **Anwenderspezifische Anzeigenmetadaten:** Erstellen Sie für anwenderdefinierte Metadaten ein variables Objekt für die anwenderspezifischen Datenvariablen und füllen Sie es mit den Daten für aktuelle Anzeigen.

1. Rufen Sie `trackEvent()` mit dem `AdStart`-Ereignis in der `MediaHeartbeat`-Instanz auf, um das Tracking der Anzeigenwiedergabe zu starten.

   Fügen Sie als dritten Parameter im Ereignisaufruf eine Referenz auf Ihre anwenderdefinierte Metadatenvariable (oder ein leeres Objekt) ein. Halten Sie während der Wiedergabe der Anzeige den Abspielkopf für den Inhalt (`l:event:playhead`) an der Position, an der die Anzeigenunterbrechung begann, fest. Wird er während der Anzeigenwiedergabe vorgezogen, wird [Besuchszeit für den Inhalt](/help/reporting/metrics/content-time-spent.md) überbewertet.

1. Wenn die Wiedergabe der Anzeige das Ende der Anzeige erreicht, rufen Sie `trackEvent()` mit dem `AdComplete`-Ereignis auf.

1. Wenn die Anzeigenwiedergabe nicht abgeschlossen wurde, weil der Benutzer die Anzeige überspringt, verfolgen Sie das `AdSkip`-Ereignis.
1. Wiederholen Sie die Schritte 3 bis 7, wenn dieselbe `AdBreak` weitere Anzeigen enthält.
1. Wenn die Werbeunterbrechung abgeschlossen ist, verwenden Sie zu deren Tracking das `AdBreakComplete`-Ereignis.

>[!IMPORTANT]
>
>**Pre-Roll-Anzeigen: Rufen Sie `trackPlay` nicht vor dem `AdBreakStart` und `AdStart` auf.** Das erste `play`-Ping für Hauptinhaltsinkremente [Inhaltsstarts](/help/reporting/metrics/content-starts.md). Wenn `trackPlay` aufgerufen wird, bevor die Pre-Roll-Anzeigenereignisse ausgelöst werden, und der Viewer während der Anzeige ausfällt, wird der Inhalt gestartet erhöht, obwohl nie Hauptinhalt wiedergegeben wurde. Verzögern Sie bei Pre-Roll-Szenarien `trackPlay`, bis `AdBreakStart` und `AdStart` gesendet wurden.

>[!NOTE]
>
>Der während der Anzeigenwiedergabe angezeigte Abspielkopfwert stellt die Position des Viewers innerhalb des **Hauptinhalts** und nicht innerhalb der Anzeige dar. Bei einer Pre-Roll-Anzeige, die einem 10-minütigen Video vorausgeht, wird der Abspielkopf während der gesamten Anzeige `0`. Bei einer Mid-Roll-Anzeige, die mit der 5-Minuten-Markierung beginnt, bleibt der Abspielkopf für die Dauer der Anzeige bei `300` (Sekunden).

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

>[!MORELIKETHIS]
>
>* [Start der Werbeunterbrechung](/help/implementation/events/ads/ad-break-start.md)
>* [Anzeigenstart](/help/implementation/events/ads/ad-start.md)
>* [Anzeige abgeschlossen](/help/implementation/events/ads/ad-complete.md)
>* [Überspringen der Anzeige](/help/implementation/events/ads/ad-skip.md)
>* [Werbeunterbrechung abgeschlossen](/help/implementation/events/ads/ad-break-complete.md)

---
title: Sitzungsende
description: Sofortiges Schließen einer Mediensitzung, wenn der Viewer Inhalte abbricht.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---


# Sitzungsende

Das Sitzungsende-Ereignis schließt eine Medienverfolgungssitzung sofort und unwiderruflich. Sitzungsende ist ein harter Abschluss. Nach dem Versand wird die Sitzung beendet und es können keine weiteren Ereignisse darunter verfolgt werden. Verwenden Sie Sitzungsende nur, wenn Sie sicher sind, dass keine zusätzlichen Ereignisse folgen werden, z. B. wenn der Player zerstört oder die Seite entladen wird. In den meisten Fällen ist es sicherer, die Sitzung auf natürliche Weise ablaufen zu lassen, anstatt zu riskieren, Ereignisse abzuschneiden, die noch eintreffen könnten. Wenn der Viewer den Inhalt fertig gestellt hat, rufen Sie stattdessen [Sitzung abgeschlossen](session-complete.md) auf.

Ohne explizites Sitzungsende wird eine Sitzung automatisch nach 10 Minuten ohne Ereignisse oder 30 Minuten ohne Abspielkopfbewegung geschlossen.

>[!NOTE]
>
>Sie können Sitzungsende sicher mehrmals für dieselbe Sitzung aufrufen. Das Backend schließt die Sitzung beim ersten Ereignis und löscht alle nachfolgenden Ereignisse für diese Sitzungs-ID, einschließlich eines zweiten Sitzungsendes, im Hintergrund. Sie müssen sich nicht vor doppelten Aufrufen in Race-Bedingungen schützen, wie z. B. einem 30-Minuten-Timeout, das in dem Moment abläuft, in dem der Viewer den Player schließt.

* **Voraussetzungen**: [Sitzungsstart](session-start.md)
* **Zugeordnete Metrik**: Keine

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.sessionEnd"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert.

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert.

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Roku]

`sendMediaEvent` mit `eventType: "media.sessionEnd"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert:

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert:

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB Media Collection API]

Senden Sie einen `sessionEnd` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]

---
title: Einrichten der Web-SDK für Streaming-Medien
description: Konfigurieren Sie Adobe Experience Platform Web SDK (alloy.js), um Streaming-Mediendaten an die Edge Network zu senden.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Einrichten der Web-SDK für Streaming-Medien

Die `streamingMedia` der Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview) (`alloy.js`, Version 2.20.0 oder höher) erfasst Mediensessionsdaten auf Ihrer Website und sendet sie an die Edge Network. Auf dieser Seite wird die In-Code-Konfiguration (`alloy.js`) beschrieben. Informationen zum Konfigurieren von Web SDK über Tags finden Sie unter [Einrichten der Tag-Erweiterung für Web SDK für Streaming-Medien](web-sdk-tags.md).

* **Voraussetzungen**:
   * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
   * Installieren Sie Web SDK 2.20.0 oder höher. Siehe [Installieren der Web-SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview).

## Konfigurieren der Streaming-Medienkomponente

Fügen Sie die `streamingMedia` Komponente zu Ihrer `alloy` hinzu:

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Ausführliche Informationen zur Konfiguration finden Sie unter dem [`streamingMedia`-Befehl](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia).

### Migration von Media JS SDK

Wenn Sie von der Media JS (3.x)-SDK wechseln, gibt der Befehl Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) eine Tracker-Instanz zurück, die dieselben APIs wie [3.x Media SDK](/help/implementation/analytics-only/javascript.md) bereitstellt, sodass Ihre bestehenden Tracking-Aufrufe weiterhin funktionieren.

## Medien-Events tracken

Senden Sie bei konfiguriertem SDK jedes Medienereignis, indem Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufrufen. Die **Payloads finden Sie auf der Registerkarte** Web[&#x200B; auf jeder &#x200B;](/help/implementation/events/overview.md)- und [&#128279;](/help/implementation/variables/overview.md).

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Web SDK – Übersicht](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)

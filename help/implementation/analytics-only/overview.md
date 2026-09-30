---
title: Nur Analytics-Implementierung - Übersicht
description: Voraussetzungen und Implementierungsmethoden für das Add-on Adobe Analytics for Streaming Media, das für reine Analytics-Implementierungen verwendet wird.
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 5%
---
# Nur Analytics-Implementierung - Übersicht

Reine Analytics-Implementierungen verwenden das Add-on Adobe Analytics für Streaming-Medien , um Daten direkt an Adobe Analytics zu senden, ohne die Edge Network zu verwenden. Diese Methoden werden weiterhin vollständig unterstützt. Bei neuen Implementierungen empfiehlt Adobe stattdessen die Implementierung von [Edge](/help/implementation/edge/overview.md), da diese Daten zusätzlich zu Adobe Analytics für Customer Journey Analytics, Adobe Journey Optimizer und Real-Time CDP verfügbar macht.

## Voraussetzungen

1. **Vervollständigen Sie die allgemeinen Voraussetzungen.** Siehe [Allgemeine Voraussetzungen](/help/getting-started/prereqs.md).

1. **Bestätigen einer Adobe Analytics-Implementierung.** Für eine reine Analytics-Implementierung von Streaming-Medien ist eine einfache Adobe Analytics-Implementierung erforderlich. Siehe [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de).

1. **Abrufen der URL des Medien-Tracking-Servers.** Fragen Sie Ihren Adobe Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers (der `collection-api-server`-URL). Die Domain folgt normalerweise dem Muster `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie die SDK herunter oder installieren Sie die Erweiterung.** Laden Sie je nach Plattform [die aktuelle SDK herunter](/help/getting-started/download-sdks.md) oder installieren Sie die erforderliche Tag-Erweiterung.

## Wählen Sie Ihre Implementierungsmethode

Jede Seite behandelt die für Streaming-Medien spezifische Einrichtung. Der Code pro Ereignis und pro Variable lebt in [Ereignisse](/help/implementation/events/overview.md) und [Variablen](/help/implementation/variables/overview.md).

| Codebase | In-Code | Verwenden von Tags |
|---|---|---|
| Web (JavaScript) | [JavaScript](javascript.md) | [Media Analytics-Tag-Erweiterung](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| Roku | [Roku 2.x](roku-2x.md) | — |
| API | [Media Collection API](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation) | — |

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Implementierungsübersicht](/help/implementation/overview.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)

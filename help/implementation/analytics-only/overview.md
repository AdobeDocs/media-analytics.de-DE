---
title: Nur Analytics-Implementierung - Übersicht
description: Voraussetzungen und Implementierungsmethoden für das Add-on Adobe Analytics for Streaming Media, das für reine Analytics-Implementierungen verwendet wird.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '230'
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
| API | [Media Collection API](media-collection-api.md) | — |

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Implementierungsübersicht](/help/implementation/overview.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)

---
title: Einrichten von Chromecast für Streaming-Medien
description: Installieren und konfigurieren Sie die Media SDK für Chromecast für reine Analytics-Streaming-Medienimplementierungen.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%

---

# Einrichten von Chromecast für Streaming-Medien

Der Media SDK für Chromecast sendet Streaming-Mediendaten von Chromecast-Receiver-Apps direkt an Adobe Analytics. Die SDK und die zugehörige Dokumentation werden auf GitHub gehostet.

* **Voraussetzungen**:
   * Schließen Sie die [Nur Analytics-Implementierung - Übersicht](overview.md) ab.
   * [Laden Sie die Media SDK für Chromecast &#x200B;](/help/getting-started/download-sdks.md).

## Installieren und Konfigurieren von SDK

Fügen Sie die SDK zu Ihrer Chromecast-Receiver-App hinzu und konfigurieren Sie den Tracker wie in den kanonischen Referenzen beschrieben:

* [Einrichten der Chromecast-SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Referenz zur Chromecast SDK-API](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## Medien-Events tracken

Verfolgen Sie bei erstelltem Tracker jedes Medienereignis mit der entsprechenden Tracker-Methode. Auf der **Chromecast**-Registerkarte auf jeder [Ereignis](/help/implementation/events/overview.md)- und [Variablen](/help/implementation/variables/overview.md)-Seite finden Sie die genauen Aufrufe.

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Chromecast SDK API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)

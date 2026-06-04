---
title: Einrichten der Mediensammlungs-API für Streaming-Medien
description: Verwenden Sie die Mediensammlungs-API , um Streaming-Mediendaten mit RESTful-HTTP-Aufrufen direkt an Adobe Analytics zu senden.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Einrichten der Mediensammlungs-API für Streaming-Medien

Die Mediensammlungs-API sendet Streaming-Mediendaten mithilfe von RESTful-HTTP-Aufrufen direkt an Adobe Analytics. Da es vollständig anpassbar ist, unterstützt es benutzerdefiniertes Tracking und Geräte, die von den SDKs nicht abgedeckt werden. Verwenden Sie sie, wenn eine SDK für Ihre Plattform keine Option ist.

* **Voraussetzungen**: Vervollständigen Sie die [Nur-Analytics-Implementierung - Übersicht](overview.md).

## Implementieren der API

Öffnen Sie eine Sitzung mit einer `sessionStart` Anfrage und senden Sie anschließend Ereignisse an die Sitzung, die sie zurückgibt. Die vollständigen Anfrage-/Antwortformate, Parameter, Validierungsschemas und Implementierungshandbücher finden Sie in der [Media Collection API-Referenz](../media-collection-api/mc-api-overview.md).

## Medien-Events tracken

Die genauen Payloads finden Sie auf **Registerkarte** Mediensammlungs-API[ auf jeder ](/help/implementation/events/overview.md)- und [](/help/implementation/variables/overview.md)-Seite.

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Media Collection API-Referenz](../media-collection-api/mc-api-overview.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)

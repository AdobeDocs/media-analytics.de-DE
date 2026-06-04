---
title: Einrichten der Tag-Erweiterung „Media Analytics“
description: Verwenden Sie die Tag-Erweiterung „Adobe Media Analytics (3.x SDK) for Audio and Video“, um reine Analytics-Streaming-Medien zu implementieren.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 14%

---

# Einrichten der Tag-Erweiterung „Media Analytics“

Die Tag-Erweiterung „Adobe Media Analytics (3.x SDK) for Audio and Video“ stellt Media SDK for JavaScript (3.x) über Tags bereit, ohne dass JavaScript manuell installiert werden muss. Auf dieser Seite wird die Konfiguration von Tags behandelt. Informationen zum Installieren von SDK im Code finden Sie unter [Einrichten von JavaScript für Streaming-Medien](javascript.md). Beachten Sie für neue Implementierungen den empfohlenen [Web SDK-Tag-Erweiterung](/help/implementation/edge/web-sdk-tags.md)Edge-Pfad.

* **Voraussetzungen**: Vervollständigen Sie die [Nur-Analytics-Implementierung - Übersicht](overview.md).

## Installieren und Konfigurieren der Erweiterung

Fügen Sie die Media Tracker-Instanz einer für Tags aktivierten Site hinzu, indem Sie die Erweiterung in der Datenerfassungs-UI installieren und konfigurieren. Informationen zur Installation und Konfiguration finden Sie unter [Adobe Media Analytics (3.x SDK) for Audio and Video-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=de).

## Medien-Events tracken

Wenn die Erweiterung konfiguriert ist, verfolgen Sie jedes Medienereignis mit der zugehörigen Tracker-Methode. Die **Aufrufe finden Sie auf der Registerkarte** Media SDK JS 3.x[ auf jeder Seite mit ](/help/implementation/events/overview.md) Ereignissen und [Variablen](/help/implementation/variables/overview.md) .

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Media Analytics (3.x SDK) for Audio and Video-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=de)
>* [Einrichten von JavaScript für Streaming-Medien (im Code)](javascript.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

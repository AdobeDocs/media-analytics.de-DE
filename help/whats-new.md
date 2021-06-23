---
title: Neue Funktionen in Media Analytics
description: Dieser Artikel enthält Informationen zu neuen Funktionen und Benachrichtigungen.
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '625'
ht-degree: 100%

---


# Neue Funktionen in Media Analytics {#whats-new}

![Banner](assets/media_analytics_banner.png)


Auf dieser Seite werden neue Funktionen, Fehlerbehebungen und wichtige Hinweise zu Media Analytics beschrieben. Außerdem werden neue Dokumentationen, Schulungen und Video-Tutorials vorgestellt, die Ihnen helfen, Media Analytics optimal zu nutzen.


## Versionshinweise

Versionshinweise zu Adobe Experience Cloud

In den Adobe Experience Cloud-Versionshinweisen werden neue Funktionen, Fehlerbehebungen und wichtige Hinweise zu Adobe Experience Cloud beschrieben. Dazu gehören die neuesten Änderungen an Media Analytics. Außerdem werden neue Dokumentationen, Schulungen und Videoschulungen vorgestellt, die Ihnen helfen, Experience Cloud optimal zu nutzen.

## Neue Funktionen

| Funktion | [Allgemeine Verfügbarkeit](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=de) – geplantes Datum | Beschreibung |
| ----------- | ---------- | ---------- |
| [Bedienfeld „Gleichzeitige Medienbetrachter“](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17. Sept. 2020 | Mit dem Bedienfeld „Gleichzeitige Medienbetrachter“ in Workspace können Sie erkennen, wo es zu Spitzen bei gleichzeitigen Betrachtern oder zu Abbrüchen kam. Es bietet wertvolle Einblicke in die Qualität von Inhalten und die Interaktion mit Betrachtern und hilft bei der Fehlerbehebung oder der Planung in Bezug auf Volumen/Skalierung. |
| [Unterstützte Geräte und Plattformen](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=de) | 18. Juni 2020 | Die [!UICONTROL Media Launch-Erweiterung] mit dem Mobile SDK für Adobe Experience Platform unterstützt jetzt die folgenden OTT-Geräte:<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [Player-Status-Tracking](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html?lang=de) | 29. Mai 2020 | [!UICONTROL Media Analytics]-Kunden können die Interaktion mit dem Besucher während der Wiedergabe mit einem Standardsatz von Lösungsvariablen für Vollbild, verdeckte Untertitel, Stummschaltung, Bild-in-Bild und im Fokus erfassen. Sie haben auch die Möglichkeit, benutzerdefinierte Player-Status zu erstellen. [!UICONTROL Player-Status-Tracking]-Variablen sind jetzt für Berichte in [!UICONTROL Analysis Workspace verfügbar]. Diese Funktion erfordert eine der folgenden Voraussetzungen: <ul><li>Media [!DNL JavaScript] SDK 3.0 oder höher</li><li>Zur Verwendung mit dem [!DNL Adobe Experience Platform] (AEP)-SDK:</li><li>[!UICONTROL Media Analytics-Erweiterung] (für Web): [!UICONTROL Adobe Media Analytics] (3.x SDK) für Audio und Video v1.0 oder höher</li><li>[!UICONTROL Media Analytics-Erweiterung] (für Smartphone und Tablet): [!UICONTROL Adobe Media Analytics für Audio] und Video v2.0 oder höher</li><li>[!UICONTROL Mediensammlung]</li></ul> |


## Wichtige Benachrichtigungen

| Funktion | [Allgemeine Verfügbarkeit](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=de) – geplantes Datum | Beschreibung |
| ----------- | ---------- | ---------- |
| [Unterstützte Geräte und Plattformen](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=de) | 31. August 2021 | Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein. Weitere Informationen finden Sie unter den häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK. |
| [Häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK](sdk-implement/end-of-support-faqs.md) | Herbst 2019 | Die Entwicklung von Funktionen wurde für die Media Analytics-SDKs für iOS und Android beendet.  Neue Funktionen, die Anfang Herbst 2019 eingeführt wurden, werden mit den Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert. |
| [Medien-Übersicht](media-overview.md) | 20. Februar 2019 | Adobe unterstützt nur TLS 1.1 oder höher. Seit dieser Änderung erfasst Adobe keine Daten mehr von Endbenutzern mit älteren Geräten oder Webbrowsern, die TLS 1.0 bereitstellen. |
| [Unterstützte Geräte und Plattformen](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=de) | 19. Februar 2019 | Die Mindestanforderungen an die Plattformversionen, die für jedes SDK unterstützt werden, sind unten aufgeführt. <br>- iOS: iOS 6+ <br>- Android: Android 5.0+ - Lollipop <br>- Chrome: v22+<br>- Mozilla: v27+<br>- Safari: v7+<br>- IE: v1+ |
| [Audio- und Videoparameter](metrics-and-metadata/audio-video-parameters.md) | 7. Februar 2019 | Adobe Analytics für Video und Audio hat eine Metriken-Namensänderung vorgenommen. <i>Medienaufrufe</i> werden nun als <i>Medienstarts</i> bezeichnet. Diese Änderung wurde vorgenommen, um die Branchenstandards bezüglich Metriken und Berichten einzuhalten und um die Metrik in Berichten problemlos identifizieren zu können. |
| [Audio- und Videoparameter](metrics-and-metadata/audio-video-parameters.md) | 13. September 2018 | Die Bezeichnungen für einige Abmessungen, Metriken und Berichte wurden geändert, um ein inhaltsübergreifendes Tracking von Video- und Audioanalysen zu ermöglichen. Zu den geänderten Bezeichnungen gehören: *Videoaufrufe* in *Medienaufrufe*, *Videolänge* in *Inhaltsdauer* und *Videoname* in *Inhaltsname*. Die Videoberichte in Reports and Analytics wurden aktualisiert und verwenden nun die Bezeichnung „Medien“ anstelle von „Video“. Die Änderung der Bezeichnungen hat keinen Einfluss auf die Datenerfassung oder historische Daten. Beachten Sie diese Änderungen, wenn Sie sie in Report Builder oder in anderen externen automatisierten Datenabrufen verwenden, die von dieser Änderung betroffen sein könnten. |




<!-- | title | date | description | -->

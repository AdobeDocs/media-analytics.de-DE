---
title: Messoptionen
description: null
uuid: null
translation-type: ht
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: ht
source-wordcount: '293'
ht-degree: 100%

---


# Messoptionen {#measurement-options}

Sie können das Audio- und Video-Tracking unter Verwendung von Adobe Launch mit der Adobe Media Analytics-Erweiterung, dem Media SDK oder der Media Collection-API aktivieren.

## Adobe Launch mit der Adobe Media Analytics-Erweiterung

Adobe Launch ist die Adobe-Tag-Management-Lösung der nächsten Generation von Adobe. Launch bietet eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind. Um Ihre eigenen Integrationen mit Launch zu erstellen und zu pflegen, verwenden Sie Erweiterungen. Eine Erweiterung ist ein JavaScript-, HTML- und CSS-Package, das die Launch-Benutzeroberfläche und die Client-Funktionen ausbaut. Weitere Informationen finden Sie im [Benutzerhandbuch zu Experience Platform Launch](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)

Mit der Adobe Media Analytics-Erweiterung (MA) wird das JavaScript Media SDK (Media 2.x SDK) für Audio und Video hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Launch-Site oder einem Projekt.

Adobe Launch mit der Media Analytics-Erweiterung erfordert Folgendes:
* Sie müssen Adobe Experience Cloud-Kunde sein.
* Sie müssen den Launch- oder DTM-Einbettungscode auf Ihren Websites bereitstellen.
* [Analytics-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Medien-SDK

Das Media SDK lässt sich den am häufigsten verwendeten Medien-Playern integrieren.

## Mediensammlungs-API (RESTful)

Kann mit Playern ohne SDK-Unterstützung integriert werden oder wenn keine SDK-Integration erforderlich ist.<br>Ab Version 2.2.0 werden die Video Heartbeat Library-SDKs (VHL) in Media Analytics-SDKs umbenannt. Sie unterstützen das Audio- und Video-Tracking. Das Media 2.2.0 SDK ist mit der VHL 2.x SDK-Reihe vollständig abwärtskompatibel. Nur der Name wurde geändert, nicht aber die Funktionen.

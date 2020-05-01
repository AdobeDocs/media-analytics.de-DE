---
title: Messoptionen
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# Messoptionen

Sie können die Audio- und Videoverfolgung mit Adobe Launch mit der Adobe Media Analytics-Erweiterung, dem Media SDK oder der Media Collection-API aktivieren.

## Adobe Launch mit der Adobe Media Analytics-Erweiterung

Adobe Launch ist die nächste Generation der Tag-Management-Lösung von Adobe. &quot;Launch&quot;bietet eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbetags bereitzustellen und zu verwalten, die zur Nutzung relevanter Kundenerlebnisse erforderlich sind. Um Ihre eigenen Integrationen mit Launch zu erstellen und zu pflegen, verwenden Sie Erweiterungen. Bei einer Erweiterung handelt es sich um ein JavaScript-, HTML- und CSS-Paket, das die Benutzeroberfläche für den Start und die Clientfunktion erweitert. Weitere Informationen finden Sie im Benutzerhandbuch zur [Erlebnisplattform](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)

Mit der Adobe Media Analytics (MA)-Erweiterung wird das JavaScript Media SDK (Media 2.x SDK) für Audio und Video hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Launch-Site oder einem Projekt.

Adobe Launch mit der Media Analytics-Erweiterung erfordert Folgendes:
* Sie müssen Adobe Experience Cloud-Kunde sein.
* Sie müssen den Einbettungscode &quot;Start&quot;oder &quot;DTM&quot;auf Ihren Webseiten bereitstellen.
* [Analytics-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Das Media SDK ist in die am häufigsten verwendeten Medienplayer integriert.

## API zur Medienerfassung (RESTful-API)

Integration mit Playern ohne SDK-Unterstützung oder wenn keine SDK-Integration erforderlich ist.<br>Ab Version 2.2.0 werden die Video Heartbeat Library (VHL)-SDKs in Media Analytics-SDKs umbenannt, um die Audio- und Videoverfolgung zu unterstützen. Das Media 2.2.0 SDK ist vollständig rückwärtskompatibel mit der VHL 2.x SDK-Serie. Die Namensänderung ist lediglich eine Änderung der Namenskonvention und stellt keine funktionalen Änderungen dar.

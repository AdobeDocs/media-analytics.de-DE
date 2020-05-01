---
title: Unterstützte Geräte
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 3a237ee31412784f708e772cc3a58047630e2184

---


# Unterstützte Geräte {#devices-supported}

Adobe Analytics für Audio und Video stellt sicher, dass jeder Medienstream auf allen Geräten erfasst und in Berichten aufgeführt wird.

Adobe Analytics für Audio und Video unterstützt alle wichtigen Geräte, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für ROKU, AppleTV, FireTV und Android-TV
* JavaScript-Browser für Desktop und Laptop

Das Media SDK wird routinemäßig aktualisiert, wenn neue Versionen von Geräten veröffentlicht werden. Sie können das SDK verwenden, um sich mit den größten Medienplayern von heute, einschließlich Brightcove und Ooyala, zu integrieren.

Für Geräte oder Plattformen, die derzeit keine SDK-Unterstützung haben, oder in Situationen, in denen Sie kein SDK verwenden möchten, können Sie die Media Collection-API implementieren. Mit der Media Collection-API können Sie RESTful-API-Aufrufe direkt von einem Gerät oder einer Plattform zum Media Analytics-Backend durchführen.

Die folgende Tabelle zeigt die derzeit unterstützten Listen. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Wenn ein Gerät nicht aufgeführt ist, wenden Sie sich an Ihren Kundendienst oder Lösungsberater, um den Status des Geräts zu erfahren.


| Streaming-Plattform/-Gerät |  | Media Launch Extension mit AEP SDK | Medien-SDK | Mediensammlungs-API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | JavaScript-Browser | X | X | X |
| Mobile App |  |  |  |  |
|  | iOS-Geräte | X | X | X |
|  | Android-Geräte | X | X | X |
|  | Windows-Geräte |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV (veraltet, TVOS) |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>(nativ) |
|  | Fire TV (Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | Spielekonsolen (z. B. Xbox ONE, Sony PS3/PS4) |  |  | X |
|  | Top-Boxen festlegen (z. B. xfinity X1) |  |  | X |
|  | Smart-TVs (z. B. Samsung, LG, Sony, Vizio) |  | X<br>(webbasiert) | X |
| Sonstige |  |  |  |  |
|  | Neue verbundene Geräte |  |  | X |


Weitere Informationen zum Media SDK finden unter [Unterstützte Mindestversionen der Plattformen](/help/sdk-implement/setup/setup-overview.md#minimum-platform-version).

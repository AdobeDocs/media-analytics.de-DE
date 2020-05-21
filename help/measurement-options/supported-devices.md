---
title: Unterstützte Geräte und Plattformen
description: Adobe Analytics für Audio und Video stellt sicher, dass jeder Medienstream auf allen Geräten erfasst und in Berichten aufgeführt wird.
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# Unterstützte Geräte und Plattformen {#devices-supported}

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Version 4 Mobile-SDKs, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter Häufig gestellte Fragen zum Ende der Unterstützung für [Media Analytics SDK](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics für Audio und Video unterstützt alle wichtigen Geräte, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für ROKU, AppleTV, FireTV und Android-TV
* JavaScript-Browser für Desktop und Laptop

Die Media SDKs werden routinemäßig aktualisiert, wenn neue Versionen von Geräten veröffentlicht werden. Sie können das SDK verwenden, um sich mit den größten Medienplayern von heute, einschließlich Brightcove und Ooyala, zu integrieren.

Für Geräte oder Plattformen, die derzeit keine SDK-Unterstützung haben, oder in Situationen, in denen Sie kein SDK verwenden möchten, können Sie die Media Collection-API implementieren. Mit der Media Collection-API können Sie RESTful-API-Aufrufe direkt von einem Gerät oder einer Plattform zum Media Analytics-Backend durchführen.

Die folgende Tabelle zeigt Listen, die derzeit von Geräten und Plattformen unterstützt werden. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Wenn ein Gerät nicht aufgeführt ist, wenden Sie sich an Ihren Kundendienst oder Lösungsberater, um den Status des Geräts zu erfahren.

| Streaming-Plattformen und -Geräte |  | Media Launch Extension mit AEP SDK | Medien-SDK | Mediensammlungs-API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | JavaScript-Browser | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Mobile App |  |  |  |  |
|  | iOS-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows-Geräte |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | Für 2020 geplant | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(native) |
|  | Fire TV (Fire OS) | Für 2020 geplant | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | Für 2020 geplant | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Spielekonsolen (z. B. Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Top-Boxen festlegen (z. B. xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smart-TVs (z. B. Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(webbasiert)    | ![](/help/assets/icon-blue-check.png) |
| Sonstige |  |  |  |  |
|  | Neue verbundene Geräte |  |  | ![](/help/assets/icon-blue-check.png) |

1. Die Unterstützung für diese SDKs endet am 31. August 2021. Weitere Informationen finden Sie unter Häufig gestellte Fragen zum Ende der Unterstützung für [Media Analytics SDK](/help/sdk-implement/end-of-support-faqs.md).

Weitere Informationen zu den Mindestanforderungen an die Plattformversionen, die für jedes SDK unterstützt werden, finden Sie unter Unterstützung der [Mindestplattformversion](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)

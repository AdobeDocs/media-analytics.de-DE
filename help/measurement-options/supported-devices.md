---
title: Unterstützte Geräte und Plattformen
description: Adobe Analytics for Streaming Media stellt sicher, dass jeder Medienstream auf allen Geräten erfasst und gemeldet wird.
translation-type: tm+mt
source-git-commit: dfffcf1e1d815ca178e0bdba881d973d60fe1631
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 89%

---


# Unterstützte Geräte und Plattformen {#devices-supported}

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Streaming Media unterstützt alle wichtigen Geräte, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für ROKU, AppleTV, FireTV und Android-TV
* JavaScript-Browser für Desktop und Laptop

Die Medien-SDKs werden routinemäßig aktualisiert, wenn neue Versionen von Geräten veröffentlicht werden. Sie können dieses SDK verwenden, um eine Integration mit den wichtigsten der heutigen Medien-Player herzustellen, einschließlich Brightcove und Ooyala.

Für Geräte oder Plattformen, die derzeit keine SDK-Unterstützung haben, oder in Situationen, in denen Sie kein SDK verwenden möchten, können Sie die Mediensammlungs-API implementieren. Mit der Mediensammlungs-API können Sie RESTful-API-Aufrufe direkt von einem Gerät oder einer Plattform zum Media Analytics-Backend durchführen.

Die folgende Tabelle zeigt die derzeit unterstützten Geräte und Plattformen. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/download-sdks.html). Wenn ein Gerät nicht aufgeführt ist, wenden Sie sich an die Kundenunterstützung oder einen Berater, um den Status des Geräts zu erfahren.

| Streaming-Plattformen und -Geräte |  | Media Launch Extension mit AEP Mobile SDK | Medien-SDK | Mediensammlungs-API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | JavaScript-Browser | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Mobile App |  |  |  |  |
|  | iOS-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows-Geräte |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Roku |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(nativ) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Spielekonsolen (z. B. Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Set-Top-Boxen (z. B. xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smart-TVs (z. B. Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(Web-basiert)    | ![](/help/assets/icon-blue-check.png) |
| Sonstige |  |  |  |  |
|  | Neue verbundene Geräte |  |  | ![](/help/assets/icon-blue-check.png) |

1. Die Unterstützung für diese SDKs endet am 31. August 2021. Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/sdk-implement/end-of-support-faqs.md).

Weitere Informationen zu den Mindestanforderungen an die Plattformversionen, die für jedes SDK unterstützt werden, finden Sie unter [Unterstützte Mindestplattformversionen](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/setup/setup-overview.html).

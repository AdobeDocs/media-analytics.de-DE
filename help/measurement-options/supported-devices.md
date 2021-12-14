---
title: Erfahren Sie mehr über unterstützte Geräte und Plattformen.
description: „Erfahren Sie mehr über die wichtigsten Geräte wie iOS, Android, OTT-Geräte und JavaScript-Browser, die Adobe Analytics for Streaming Media unterstützt.“
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 98%

---

# Unterstützte Geräte und Plattformen {#devices-supported}

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics für Streaming-Medien unterstützt alle wichtigen Geräte, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für ROKU, AppleTV, FireTV und Android-TV
* JavaScript-Browser für Desktop und Laptop

Die Medien-SDKs werden routinemäßig aktualisiert, wenn neue Versionen von Geräten veröffentlicht werden. Sie können dieses SDK verwenden, um eine Integration mit den wichtigsten der heutigen Medien-Player herzustellen, einschließlich Brightcove und Ooyala.

Für Geräte oder Plattformen, die derzeit keine SDK-Unterstützung haben, oder in Situationen, in denen Sie kein SDK verwenden möchten, können Sie die Mediensammlungs-API implementieren. Mit der Mediensammlungs-API können Sie RESTful-API-Aufrufe direkt von einem Gerät oder einer Plattform zum Media Analytics-Backend durchführen.

Die folgende Tabelle zeigt die derzeit unterstützten Geräte und Plattformen. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html?lang=de). Wenn ein Gerät nicht aufgeführt ist, wenden Sie sich an die Kundenunterstützung oder einen Berater, um den Status des Geräts zu erfahren.

| Streaming-Plattformen und -Geräte |  | Datenerfassung mit AEP Mobile SDK | Medien-SDK | Mediensammlungs-API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | JavaScript-Browser | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Mobile App |  |  |  |  |
|  | iOS-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-Geräte | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows-Geräte |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Roku |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(nativ) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Spielekonsolen (z. B. Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Set-Top-Boxen (z. B. xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smart-TVs (z. B. Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(Web-basiert)    | ![](/help/assets/icon-blue-check.png) |
| Sonstige |  |  |  |  |
|  | Neue verbundene Geräte |  |  | ![](/help/assets/icon-blue-check.png) |

1. Die Unterstützung für diese SDKs endet am 31. August 2021. Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/sdk-implement/end-of-support-faqs.md).

Weitere Informationen zu den Mindestanforderungen an die Plattformversionen, die für jedes SDK unterstützt werden, finden Sie unter [Unterstützte Mindestplattformversionen](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html?lang=de).

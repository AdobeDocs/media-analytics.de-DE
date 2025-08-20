---
title: Erfahren Sie mehr über die häufig gestellten Fragen zum Media Analytics SDK End of Support
description: In diesem Kapitel finden Sie häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 68%

---

# Häufig gestellte Fragen zum Ende der Unterstützung für Media Analytics Mobile SDK

Seit dem 31. August 2021, dem Ende der Unterstützung für Mobile SDKs der Version 4, stellt Adobe auch die Unterstützung für die Media Analytics Mobile SDKs für iOS und Android ein. (Dies betrifft nicht die Media Analytics SDK for Web (JS)- und OTT-Plattformen wie Chromecast und Roku, die weiterhin unterstützt werden.)

Dies bedeutet, dass Adobe keine Fehlerbehebungen, betriebssystembezogene Updates oder Unterstützung für Media Analytics Mobile SDK mehr bereitstellt. Beachten Sie bei der Migration zu den neuen Experience Platform-SDKs, dass [Media Analytics-Erweiterungen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) implementiert werden müssen, um die Adobe-Streaming-Mediendienste zu aktivieren.


## Die fünf wichtigsten Dinge

1. Ab dem 31. August 2021 werden Mobile v4-SDKs nicht mehr unterstützt. Sie sollten zu den Adobe Experience Platform (AEP) Mobile SDKs für iOS und Android migrieren.

1. Für eine Implementierung von Adobe Streaming Media Services sind die Mobile SDK von AEP und die Verwendung der Erweiterungen Analytics und Media Analytics erforderlich. Ab dem 1. September 2021 sollten Sie die neuen AEP Mobile SDKs und Erweiterungen verwenden.  Media Analytics-Erweiterungen werden mit Adobe Tags (Datenerfassung) konfiguriert.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Die Funktionsentwicklung wurde für die Media Analytics-SDKs für iOS und Android beendet. Neue Funktionen, die seit Herbst 2019 eingeführt wurden, werden mithilfe der Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden mit dem Add-on „Adobe Analytics for Streaming Media“ und dem Add-on &quot;Customer Journey Analytics Streaming Media Collection“ verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs verbessert und unterstützt. Wenn Sie das JS-SDK für Media Analytics verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung mithilfe der Adobe-Datenerfassung (vormals Adobe Launch) aktivieren.

Wenden Sie sich bei Fragen an Ihr Adobe Account Team.

## Häufig gestellte Fragen (FAQ)

1. **Wird die Unterstützung für Roku- und Chromecast-SDKs beeinträchtigt? &#x200B;**

   Nein.  Roku- und Chromecast-SDKs werden vorläufig weiterhin als eigenständige SDKs unterstützt.
&#x200B;
1. **Wird diese Änderung Auswirkungen auf die JS-SDK-Implementierungen von Media Analytics haben? &#x200B;**

   Nein.  Kunden, die das JS-SDK für Media Analytics verwenden, können das SDK weiterhin verwenden oder es über Adobe Launch aktivieren.
&#x200B;
1. **Wie aufwändig ist die Migration zu den Media Analytics-Erweiterungen? &#x200B;**

   Das hängt von der jeweiligen Kundenimplementierung und variiert daher.  Wenden Sie sich nach der Lektüre der unten genannten Migrationsdokumentation an die Beratung und/oder Kundenunterstützung, um weitere Unterstützung zu erhalten.

[Media Analytics-Erweiterungen: Android-Migration](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics-Erweiterungen: iOS-Migration](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics-Erweiterungen: neue Implementierungen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Muss ich Launch als Tag-Management-System haben? Was ist, wenn ich Launch nicht verwenden möchte?**

   Bei der Verwendung für mobile Anwendungen wird Launch nicht wie für das Web als Tag-Management-System verwendet. Zum Konfigurieren der SDK-Erweiterungen muss die Launch-Benutzeroberfläche verwendet werden. Dies ähnelt der Verwendung der Benutzeroberfläche von Adobe Mobile Services zum Konfigurieren des mobilen SDK der Version 4. Bei der Installation liegt der Vorteil der Verwendung von Launch darin, dass Sie benutzerdefinierte Installationsanweisungen anhand der von Ihnen ausgewählten Erweiterung erhalten.

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für tvOS?**

   Ja, bei tvOS (ab Version 10) wird empfohlen, zu den Media Analytics-Erweiterungen zu migrieren. Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für Fire TV und Android TV?**

   Ja. Für Fire TV und Android TV wird zur Implementierung die Migration zu den Media Analytics-Erweiterungen empfohlen. Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).

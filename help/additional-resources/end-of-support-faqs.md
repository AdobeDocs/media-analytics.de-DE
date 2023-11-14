---
title: Erfahren Sie mehr über die häufig gestellten Fragen zum Media Analytics SDK End of Support
description: In diesem Kapitel finden Sie häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c00c9850d5ea924cef6b4842ecb770df1e78eb21
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 79%

---

# Media Analytics Häufig gestellte Fragen zum Ende der Unterstützung für Mobile-SDKs

Am 31. August 2021, dem Ende der Unterstützung für Mobile SDKs der Version 4, hat Adobe auch die Unterstützung für die Mobile SDKs für Media Analytics für iOS und Android beendet. (Dies umfasst nicht das Media Analytics-SDK für Web- (JS-) und OTT-Plattformen wie Chromecast und Roku, die weiterhin unterstützt werden.)

Das bedeutet, dass Adobe keine Fehlerbehebungen, betriebssystembezogenen Aktualisierungen oder Unterstützung für das Media Analytics Mobile SDK mehr bietet. Beachten Sie bei der Migration zu den neuen Experience Platform SDKs, dass die Variable [Media Analytics-Erweiterungen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) muss implementiert werden, um Adobe Analytics für Streaming-Medien zu aktivieren.


## Die fünf wichtigsten Dinge

1. Mobile SDKs der Version 4 werden ab dem 31. August 2021 nicht mehr unterstützt. Wir empfehlen, zu den mobilen SDKs von Adobe Experience Platform (AEP) für iOS und Android zu migrieren.

1. Für die Implementierung von Analytics für Streaming-Medien sind das mobile SDK von Adobe Experience Platform und die Verwendung der Analytics- und Media Analytics-Erweiterungen erforderlich. Ab dem 1. September 2021 sollten Sie die neuen AEP Mobile SDKs und Erweiterungen verwenden.  Media Analytics-Erweiterungen werden mit Adobe Tags (Datenerfassung) konfiguriert.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Die Funktionsentwicklung wurde für die Media Analytics-SDKs für iOS und Android beendet. Neue Funktionen, die seit Herbst 2019 eingeführt wurden, werden mithilfe der Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden von Analytics für Streaming-Medien verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs verbessert und unterstützt. Wenn Sie das JS-SDK für Media Analytics verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung mithilfe der Adobe-Datenerfassung (vormals Adobe Launch) aktivieren.

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

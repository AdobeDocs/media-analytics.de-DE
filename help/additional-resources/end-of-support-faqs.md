---
title: Erfahren Sie mehr über die häufig gestellten Fragen zum Media Analytics SDK End of Support
description: In diesem Kapitel finden Sie häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '690'
ht-degree: 100%

---

# Media Analytics Häufig gestellte Fragen zum Ende der Unterstützung für Mobile-SDKs

Seit dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics Mobile SDK für iOS und Android ein. Seit dem 31. August 2021 stellt Adobe keine Fehlerbehebungen, betriebssystembezogene Updates oder Unterstützung für das Media Analytics Mobile SDK mehr bereit.  Beachten Sie bei der Migration zu diesen neuen Experience Platform-SDKs, dass die [Media Analytics-Erweiterungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) implementiert werden müssen, um Adobe Analytics für Streaming-Medien zu aktivieren.

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).


## Die fünf wichtigsten Dinge

1. Mobile SDKs der Version 4 werden nach dem 31. August 2021 nicht mehr unterstützt. Wir empfehlen, zu den mobilen SDKs von Adobe Experience Platform (AEP) für iOS und Android zu migrieren. Weitere Informationen finden Sie in den [häufig gestellten Fragen zum Ende der Unterstützung für Mobile SDKs der Version 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. Für die Implementierung von Analytics für Streaming-Medien sind das mobile SDK von Adobe Experience Platform und die Verwendung der Analytics- und Media Analytics-Erweiterungen erforderlich. Ab dem 1. September 2021 sollten Sie die neuen mobilen SDKs und Erweiterungen von Adobe Experience Platform verwenden.  Media Analytics-Erweiterungen werden mit Adobe Tags (Datenerfassung) konfiguriert.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Die Funktionsentwicklung wurde für die Media Analytics-SDKs für iOS und Android beendet.  Neue Funktionen, die Anfang Herbst 2019 eingeführt wurden, werden mit den Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden von Analytics für Streaming-Medien verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs verbessert und unterstützt.  Wenn Sie das JS-SDK für Media Analytics verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung mithilfe der Adobe-Datenerfassung (vormals Adobe Launch) aktivieren.

1. Vor dem 1. September 2021 kann Adobe nach eigenem Ermessen neue Fehlerbehebungen für Probleme herausbringen, die starke technische oder geschäftliche Auswirkungen haben. Adobe wird auf der Basis der Kundenanfragen das Maß der Auswirkungen sowie die daraus resultierenden Aktivitäten bestimmen.

Wenden Sie sich an Ihren Adobe-Success-Manager, wenn Sie Fragen haben.

## Häufig gestellte Fragen (FAQ)

1. **Wird die Unterstützung für Roku- und Chromecast-SDKs beeinträchtigt? &#x200B;**

   Nein.  Roku- und Chromecast-SDKs werden vorläufig weiterhin als eigenständige SDKs unterstützt.
&#x200B;
1. **Wird diese Änderung Auswirkungen auf die JS-SDK-Implementierungen von Media Analytics haben? &#x200B;**

   Nein.  Kunden, die das JS-SDK für Media Analytics verwenden, können das SDK weiterhin verwenden oder es über Adobe Launch aktivieren.
&#x200B;
1. **Wie aufwändig ist die Migration zu den Media Analytics-Erweiterungen? &#x200B;**

   Das hängt von der Implementierung des jeweiligen Kunden ab und variiert.  Wenden Sie sich nach der Lektüre der unten genannten Migrationsdokumentation an die Beratung und/oder Kundenunterstützung, um weitere Unterstützung zu erhalten.

[Media Analytics-Erweiterungen: Android-Migration](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics-Erweiterungen: iOS-Migration](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics-Erweiterungen: neue Implementierungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Muss ich Launch als Tag-Management-System haben? Was ist, wenn ich Launch nicht verwenden möchte?**

   Bei der Verwendung für mobile Anwendungen wird Launch nicht wie für das Web als Tag-Management-System verwendet.  Zum Konfigurieren der SDK-Erweiterungen muss die Launch-Benutzeroberfläche verwendet werden. Dies ähnelt der Verwendung der Benutzeroberfläche von Adobe Mobile Services zum Konfigurieren des mobilen SDK der Version 4. Bei der Installation liegt der Vorteil der Verwendung von Launch darin, dass Sie benutzerdefinierte Installationsanweisungen anhand der von Ihnen ausgewählten Erweiterung erhalten.

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für tvOS?**

   Ja, bei tvOS (ab Version 10) wird empfohlen, zu den Media Analytics-Erweiterungen zu migrieren.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für Fire TV und Android TV?**

   Ja. Für Fire TV und Android TV wird zur Implementierung die Migration zu den Media Analytics-Erweiterungen empfohlen.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
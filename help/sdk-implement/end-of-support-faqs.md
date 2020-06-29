---
title: Häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK
description: In diesem Kapitel finden Sie häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK.
translation-type: ht
source-git-commit: 38adc54438f85ca8ece8c77d9ff0d0aa14eb6605
workflow-type: ht
source-wordcount: '703'
ht-degree: 100%

---


# Häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK

Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein. Ab dem 31. August 2021 stellt Adobe keine Fehlerbehebungen, betriebssystembezogene Updates oder Unterstützung für das Media Analytics-SDK bereit.  Beachten Sie bei der Migration zu diesen neuen Experience Platform-SDKs, dass die [Media Analytics-Erweiterungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) implementiert werden müssen, um Adobe Analytics für Audio und Video zu aktivieren.

## Die fünf wichtigsten Dinge

1. Mobile SDKs der Version 4 werden nach dem 31. August 2021 nicht mehr unterstützt. Wir empfehlen, zu den Adobe Experience Platform-SDKs (AEP) für iOS und Android zu migrieren. Weitere Informationen finden Sie in den [häufig gestellten Fragen zum Ende der Unterstützung für Mobile SDKs der Version 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. Für die Implementierung von Analytics für Audio und Video sind das AEP-SDK und die Verwendung der Analytics- und Media Analytics-Erweiterungen erforderlich. Ab dem 1. September 2021 sollten Sie die neuen AEP SDKs und Erweiterungen verwenden.  Media Analytics-Erweiterungen werden über Adobe Launch konfiguriert.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html).

1. Die Funktionsentwicklung wurde für die Media Analytics-SDKs für iOS und Android beendet.  Neue Funktionen, die Anfang Herbst 2019 eingeführt wurden, werden mit den Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden von Analytics für Audio und Video verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs verbessert und unterstützt.  Wenn Sie das JS-SDK für Media Analytics verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung über Adobe Launch aktivieren.

1. Vor dem 1. September 2021 kann Adobe nach eigenem Ermessen neue Fehlerbehebungen für Probleme herausbringen, die starke technische oder geschäftliche Auswirkungen haben. Adobe wird auf der Basis der Kundenanfragen das Maß der Auswirkungen sowie die daraus resultierenden Aktivitäten bestimmen.

Wenden Sie sich an Ihren Adobe-Success-Manager, wenn Sie Fragen haben.

## Häufig gestellte Fragen (FAQ)

1. **Wird die Unterstützung für Roku- und Chromecast-SDKs beeinträchtigt? &#x200B;**

   Nein.  Roku- und Chromecast-SDKs werden vorläufig weiterhin als eigenständige SDKs unterstützt. &#x200B; &#x200B;
1. **Wird diese Änderung Auswirkungen auf die JS-SDK-Implementierungen von Media Analytics haben? &#x200B;**

   Nein.  Kunden, die das JS-SDK für Media Analytics verwenden, können das SDK weiterhin verwenden oder es über Adobe Launch aktivieren.
&#x200B;
1. **Wie aufwändig ist die Migration zu den Media Analytics-Erweiterungen? &#x200B;**

   Das hängt von der Implementierung des jeweiligen Kunden ab und variiert.  Wenden Sie sich nach der Lektüre der unten genannten Migrationsdokumentation an die Beratung und/oder Kundenunterstützung, um weitere Unterstützung zu erhalten.

   [Media Analytics-Erweiterungen: Android-Migration](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics-Erweiterungen: iOS-Migration](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics-Erweiterungen: neue Implementierungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Muss ich Launch als Tag-Management-System haben? Was ist, wenn ich Launch nicht verwenden möchte?**

   Bei der Verwendung für mobile Anwendungen wird Launch nicht wie für das Web als Tag-Management-System verwendet.  Zum Konfigurieren der SDK-Erweiterungen muss die Launch-Benutzeroberfläche verwendet werden. Dies ähnelt der Verwendung der Benutzeroberfläche von Adobe Mobile Services zum Konfigurieren des mobilen SDK der Version 4. Bei der Installation liegt der Vorteil der Verwendung von Launch darin, dass Sie benutzerdefinierte Installationsanweisungen anhand der von Ihnen ausgewählten Erweiterung erhalten.

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für tvOS?**

   Ja, bei tvOS (ab Version 10) wird empfohlen, zu den Media Analytics-Erweiterungen zu migrieren.  Die Unterstützung vom AEP-SDK und von der Media Analytics-Erweiterung ist für Juni 2020 geplant.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – iOS](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für FireTV und AndroidTV? &#x200B;**

   Ja. Für FireTV und AndroidTV wird eine Migration zu den Media Analytics-Erweiterungen empfohlen.  Die Unterstützung vom AEP-SDK und von der Media Analytics-Erweiterung ist für Juni 2020 geplant.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch – Android](https://docs.adobe.com/content/help/de-DE/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).

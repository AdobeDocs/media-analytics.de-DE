---
title: Häufig gestellte Fragen zum Ende der Unterstützung für Medienanalysen-SDK
description: In diesem Thema finden Sie häufig gestellte Fragen zum Ende der Unterstützung für Media Analytics-SDKs.
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# Häufig gestellte Fragen zum Ende der Unterstützung für Medienanalysen-SDK

Ab dem 31. August 2021, dem Ende der Unterstützung für Version 4 Mobile-SDKs, stellt Adobe auch die Unterstützung für die Media Analytics-SDKs für iOS und Android ein. Ab dem 31. August 2021 stellt Adobe keine Fehlerbehebungen, betriebssystembezogene Updates oder Unterstützung für das Medienanalytics-SDK bereit.  Beachten Sie bei der Migration zu diesen neuen Experience Platform SDKs, dass die [Media Analytics-Erweiterungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) implementiert werden müssen, um Adobe Analytics für Audio und Video zu aktivieren.

## Die fünf wichtigsten Dinge

1. Mobile v4 SDKs werden nach dem 31. August 2021 nicht mehr unterstützt. Sie sollten zu den Adobe Experience Platform (AEP) SDKs für iOS und Android migrieren.

1. Für die Implementierung von Analytics für Audio und Video ist das AEP SDK und die Verwendung der Analytics- und Medienanalyseerweiterungen erforderlich. Ab dem 1. September 2021 sollten Sie die neuen AEP SDKs und Erweiterungen verwenden.  Media Analytics-Erweiterungen werden mit Adobe Launch konfiguriert.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zum Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Die Funktionsentwicklung für die Media Analytics-SDKs für iOS und Android ist beendet.  Neue Funktionen, die seit Herbst 2019 eingeführt wurden, werden mit den Media Analytics-Erweiterungen und der Media Collection-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden von Analytics für Audio und Video verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs erweitert und unterstützt.  Wenn Sie das JS SDK für Medienanalyse verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung mit Adobe Launch aktivieren.

1. Vor dem 1. September 2021 kann Adobe nach eigenem Ermessen neue Lösungen für Probleme mit hohen technischen Auswirkungen oder einer hohen geschäftlichen Präsenz entwickeln. Auf Basis der Kundeneingabe ermittelt Adobe den Grad der Auswirkung und Belichtung sowie die daraus resultierenden Aktivitäten.

Wenden Sie sich bei Fragen an Ihren Adobe-Kundenbetreuer.

## Häufig gestellte Fragen (FAQ)

1. **Wird die Unterstützung für Roku- und Chromecast-SDKs beeinträchtigt? &#x200B;**

   Nein.  Roku- und Chromecast-SDKs werden vorläufig weiterhin als eigenständige SDKs unterstützt. &#x200B; &#x200B;
1. **Wird diese Änderung Auswirkungen auf die JS SDK-Implementierungen von Media Analytics haben? &#x200B;**

   Nein.  Kunden, die das JS-SDK für Media Analytics verwenden, können das SDK weiterhin verwenden oder es über Adobe Launch aktivieren.
&#x200B;
1. **Wie viel Aufwand besteht für die Migration zu den Media Analytics-Erweiterungen? &#x200B;**

   LOE hängt von der Implementierung des jeweiligen Kunden ab, sodass es variiert.  Wenden Sie sich nach der Überprüfung der unten stehenden Migrationsdokumentation an die Beratung und/oder Kundenbetreuung, um weitere Unterstützung zu erhalten.

   [Media Analytics-Erweiterungen: Android-Migration](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics-Erweiterungen: iOS-Migration](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics-Erweiterungen: neue Implementierungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Muss ich Launch als Tag-Management-System haben? Was ist, wenn ich Launch nicht verwenden möchte?**

   Für Mobilgeräte ist &quot;Start&quot;erforderlich, um die Media-Erweiterungen wie die Mobile Services-Benutzeroberfläche zu konfigurieren. Im Anwendungsfall für mobile Apps wird sie nicht als Tag-Management-System verwendet.

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für tvOS?**

   Ja, bei tvOS (ab Version 10) wird empfohlen, zu den Media Analytics-Erweiterungen zu migrieren.  Die Unterstützung von AEP SDK und Media Analytics Extension ist für Juni 2020 geplant.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Media SDK zu Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Hat dieses Ende der Unterstützung Auswirkungen auf das SDK für FireTV und AndroidTV? &#x200B;**

   Ja. Für FireTV und AndroidTV wird eine Migration zu den Media Analytics-Erweiterungen empfohlen.  Die Unterstützung von AEP SDK und Media Analytics Extension ist für Juni 2020 geplant.  Weitere Informationen finden Sie unter [Migration vom eigenständigen Media SDK zu Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).

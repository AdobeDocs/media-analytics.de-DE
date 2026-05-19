---
title: Erfahren Sie mehr über die häufig gestellten Fragen zum Media Analytics SDK End of Support
description: In diesem Kapitel finden Sie häufig gestellte Fragen zum Ende der Unterstützung für das Media Analytics-SDK.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 61%

---

# Häufig gestellte Fragen zum Ende der Unterstützung für Media Analytics Mobile SDK

Seit dem 31. August 2021, dem Ende der Unterstützung für Mobile SDKs der Version 4, stellt Adobe auch die Unterstützung für die Media Analytics Mobile SDKs für iOS und Android ein. (Dies betrifft nicht die Media Analytics SDK for Web (JS)- und OTT-Plattformen wie Chromecast und Roku, die weiterhin unterstützt werden.)

Dies bedeutet, dass Adobe keine Fehlerbehebungen, betriebssystembezogene Updates oder Unterstützung für Media Analytics Mobile SDK mehr bereitstellt. Beachten Sie bei der Migration zu den neuen Experience Platform-SDKs, dass [Media Analytics-Erweiterungen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) implementiert werden müssen, um die Adobe-Streaming-Mediendienste zu aktivieren.


## Die fünf wichtigsten Dinge

1. Ab dem 31. August 2021 werden Mobile v4-SDKs nicht mehr unterstützt. Sie sollten zu den Adobe Experience Platform (AEP) Mobile SDKs für iOS und Android migrieren.

1. Für eine Implementierung von Adobe Streaming Media Services sind die Mobile SDK von AEP und die Verwendung der Erweiterungen Analytics und Media Analytics erforderlich. Ab dem 1. September 2021 sollten Sie die neuen AEP Mobile SDKs und Erweiterungen verwenden.  Media Analytics-Erweiterungen werden mit Adobe Tags (Datenerfassung) konfiguriert. Weitere Informationen finden Sie unter [Migration vom eigenständigen Medien-SDK zu Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Die Funktionsentwicklung wurde für die Media Analytics-SDKs für iOS und Android beendet. Neue Funktionen, die seit Herbst 2019 eingeführt wurden, werden mithilfe der Media Analytics-Erweiterungen und der Mediensammlungs-API aktiviert.

1. Die Roku- und Chromecast-SDKs bleiben für Kunden mit dem Add-on „Adobe Analytics for Streaming Media“ und dem Add-on &quot;Customer Journey Analytics Streaming Media Collection“ verfügbar. Die Roku- und Chromecast-SDKs werden weiterhin als eigenständige SDKs verbessert und unterstützt. Wenn Sie das JS-SDK für Media Analytics verwenden, können Sie weiterhin das eigenständige SDK verwenden oder die Media Analytics-Erweiterung mithilfe der Adobe-Datenerfassung (vormals Adobe Launch) aktivieren.

Wenden Sie sich bei Fragen an Ihr Adobe Account Team.

## Häufig gestellte Fragen (FAQ)

1. **Wird die Unterstützung für Roku- und Chromecast-SDKs beeinträchtigt? &#x200B;**

   Nein.  Roku- und Chromecast-SDKs werden vorerst weiterhin als eigenständige SDKs unterstützt&#x200B;
&#x200B;
1. **Wird diese Änderung Auswirkungen auf die JS-SDK-Implementierungen von Media Analytics haben? &#x200B;**

   Nein.  Kunden, die die JS-SDK für Media Analytics verwenden, können die SDK weiterhin verwenden oder über Adobe Launch aktivieren.
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

---
title: Erste Schritte
description: Erste Schritte mit Adobe Analytics für Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# Erste Schritte {#getting-started}

Adobe Analytics für Streaming Media bietet zwei Hauptimplementierungsmethoden: die Medien-SDKs und die Mediensammlungs-APIs.

![Methoden](assets/getting-started2.png)

Unter Verwendung der integrierten Logik der **Medien-SDKs** können Sie mehrere Medienplattformen genau messen, darunter Websites, Mobiltelefone, vernetzte TVs, Tablets, OTT-Geräte, Set-Top-Boxen und Spielekonsolen. Sie können sogar heruntergeladene Inhalte messen. Sie erhalten detaillierte Einblicke in die Interaktion der Benutzer, sodass Sie verstehen können, wie lange, wann und wo die Zuschauer interagieren. Die Medien-SDKs verwenden die **Mediensammlungs-APIs** für das Tracking. Die Mediensammlungs-APIs können angepasst werden, wenn Ihre Anwendung benutzerdefinierte Tracking-Funktionen erfordert. Für Geräte, die von den Medien-SDKs nicht unterstützt werden, können Sie die Mediensammlungs-APIs verwenden.

Die Adobe Analytics Streaming Media-Lösung ist für die folgenden Medienplattformen verfügbar:

* Web
* Mobile
* Over-the-top
* Jedes verbundene Gerät, das für Streaming-Medien oder eine Server-zu-Server-Integration verwendet werden kann

Weitere Informationen finden Sie unter [Unterstützte Geräte und Plattformen](#_Supported_devices_and).

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung von Adobe Analytics Streaming-Medien an Ihren Adobe-Kundenbetreuer oder -Account Manager, um sicherzustellen, dass Streaming-Medien Teil Ihres Produktportfolios ist.

## Medien-SDKs für Streaming-Medien {#media-sdks}

Medien-SDKs für Streaming-Medien sind für die Plattformen JavaScript, Android, iOS, tvOS, Chromecast und Roku verfügbar.

Informationen zum Herunterladen und Installieren von Medien-SDKs finden Sie unter [Abrufen von Medien-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs](/help/getting-started/download-sdks.md).


## Mediensammlungs-APIs {#media-collection-apis}

Mithilfe der **Mediensammlungs-APIs** können Sie Ihre Medienanalyseimplementierung anpassen. Verwenden Sie die Mediensammlungs-APIs, um die Server von Adobe direkt aufzurufen und fast alle Aktionen auszuführen, die Sie auch mit den SDKs durchführen können u. ä. Passen Sie Ihre Datenerfassung an, um Berichte zu erstellen, die Ihnen helfen, Fragestellungen zu untersuchen, Einblicke zu gewinnen oder wichtige Fragen zu Ihren Streaming-Mediendaten zu beantworten.

Informationen zur Verwendung der Mediensammlungs-APIs finden Sie unter [Dokumentation zu Streaming Medien-APIs](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe-Erweiterungen {#adobe-extensions}

* Die [**Adobe Media Analytics für Audio und Video-Erweiterung**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=de) (Media Analytics-Erweiterung) ist für iOS- und tvOS-Implementierungen erforderlich. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der Tracker-Instanz zu einer Tag-Site oder einem Projekt. Für die MA-Erweiterung sind auch die Analytics-Erweiterung und die Experience Cloud-ID-Erweiterung erforderlich.

* [Analytics-Erweiterung v1.6 oder höher](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=de): Mit dieser Erweiterung können Sie die JavaScript-Bibliothek des Adobe Experience Platform Web-SDKs laden, um Daten an Adobe-Lösungen zu senden.

* [Experience Cloud-ID-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=de): Diese Erweiterung implementiert den Experience Cloud-ID-Service, der Besucher über alle Experience Cloud-Lösungen hinweg identifiziert. Der Experience Cloud-ID-Service ist eine Personalisierungserweiterung in Adobe Experience Platform.

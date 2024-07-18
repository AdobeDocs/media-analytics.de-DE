---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Streaming Media Collection Add-ons mit reinen Adobe Analytics-Implementierungen
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# Voraussetzungen für reine Adobe Analytics-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen müssen erfüllt sein, um das Streaming-Mediensammlungs-Add-on mit reinen Adobe-Analytics-Implementierungen zu implementieren (wenn Edge nicht verwendet wird).

1. **Die allgemeinen Voraussetzungen erfüllen**<br>
Stellen Sie sicher, dass Sie die [allgemeinen Voraussetzungen](/help/getting-started/prereqs.md) erfüllen, unabhängig davon, ob Sie das Streaming-Mediensammlungs-Add-on für Implementierungen mit nur Adobe Analytics oder für Implementierungen mit Edge implementieren.

1. **Bestätigen, dass Sie über eine Adobe Analytics-Implementierung verfügen**<br>
Bei der Implementierung des Streaming-Media-Collection-Add-ons mit einer Nur-Analytics-Implementierung ist auch eine grundlegende Adobe Analytics-Implementierung erforderlich. Weitere Informationen finden Sie unter [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de).

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie Ihren Adobe Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. Dies ist die `collection-api-server`-URL für das Mobile SDK, das JavaScript SDK und den Tracking-Server ohne Sammlungs-API für Roku. Domain-Namen für die API-Implementierung sind: `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie das aktuelle Medien-SDK herunter oder implementieren Sie die erforderlichen Erweiterungen**<br>
Abhängig vom Implementierungspfad können Sie für Web-, Mobil- und Over-the-top-Plattformen [das aktuelle SDK herunterladen](/help/getting-started/download-sdks.md). Die erforderlichen Erweiterungen müssen implementiert werden, um die Erweiterungspfade des Streaming Media Collection Add-ons für Streaming-Medien zu aktivieren.

1. **Aktivieren von Adobe Analytics-Berichten**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten](/help/reporting/media-reports-enable.md).

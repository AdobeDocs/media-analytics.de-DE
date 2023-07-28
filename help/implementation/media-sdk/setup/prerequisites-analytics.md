---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung von Streaming-Medien mit reinen Adobe Analytics-Implementierungen
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Voraussetzungen für reine Adobe Analytics-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung von Streaming-Medien mit reinen Adobe-Analytics-Implementierungen (wenn Edge nicht verwendet wird).

1. **Allgemeine Voraussetzungen erfüllen**<br>
Stellen Sie sicher, dass Sie die [Allgemeine Voraussetzungen](/help/getting-started/prereqs.md).

1. **Bestätigen der Adobe Analytics-Implementierung**<br>
Bei der Implementierung von Streaming-Medien mit einer Nur-Analytics-Implementierung ist auch eine grundlegende Adobe Analytics-Implementierung erforderlich. Weitere Informationen finden Sie unter [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de).

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie Ihren Adobe Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. Dies ist die `collection-api-server`-URL für das Mobile SDK, das JavaScript-SDK und den Tracking-Server ohne Sammlungs-API für Roku. Domain-Namen für die API-Implementierung sind: `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie das aktuelle Medien-SDK herunter oder implementieren Sie die erforderlichen Erweiterungen**<br>
Abhängig vom Implementierungspfad können Sie für Web-, Mobil- und Over-the-top-Plattformen [das aktuelle SDK herunterladen](/help/getting-started/download-sdks.md). Die erforderlichen Erweiterungen müssen implementiert werden, um die Erweiterungspfade für Adobe Analytics für Streaming-Medien zu aktivieren.

1. **Aktivieren von Adobe Analytics-Berichten**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten](/help/reporting/media-reports-enable.md).

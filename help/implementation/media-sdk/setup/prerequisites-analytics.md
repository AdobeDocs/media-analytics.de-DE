---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Add-ons „Adobe Analytics for Streaming Media“ für Implementierungen, die nur auf Adobe Analytics basieren
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 43%

---

# Voraussetzungen für reine Adobe Analytics-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung des Add-ons „Adobe Analytics for Streaming Media“ für Implementierungen, die nur auf Adobe Analytics basieren (wenn Edge nicht verwendet wird).

1. **Vervollständigen Sie die allgemeinen Voraussetzungen**<br>
Unabhängig davon, ob Sie Streaming-Medien-Services für Implementierungen auf Adobe Analytics oder für Edge-Implementierungen implementieren, stellen Sie sicher, dass Sie die [allgemeinen Voraussetzungen](/help/getting-started/prereqs.md) erfüllen.

1. **Vergewissern Sie sich, dass Sie über eine Adobe Analytics-Implementierung verfügen**<br>
Bei der Implementierung des Add-ons „Adobe Analytics for Streaming Media“ für eine reine Analytics-Implementierung ist auch eine Standardimplementierung von Adobe Analytics erforderlich. Weitere Informationen finden Sie unter [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de).

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie Ihren Adobe Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. Dies ist die `collection-api-server`-URL für die Mobile SDK, die JavaScript SDK und den Tracking-Server ohne Sammlungs-API für Roku. Domain-Namen für die API-Implementierung sind: `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie das aktuelle Medien-SDK herunter oder implementieren Sie die erforderlichen Erweiterungen**<br>
Abhängig vom Implementierungspfad können Sie für Web-, Mobil- und Over-the-top-Plattformen [das aktuelle SDK herunterladen](/help/getting-started/download-sdks.md). Die erforderlichen Erweiterungen müssen implementiert werden, um das Add-on Adobe Analytics for Streaming Media zu aktivieren.

1. **Aktivieren von Adobe Analytics-Berichten**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten](/help/reporting/media-reports-enable.md).

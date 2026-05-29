---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Add-ons „Adobe Analytics for Streaming Media“ für Implementierungen, die nur auf Adobe Analytics basieren
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Voraussetzungen für reine Adobe Analytics-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung des Add-ons „Adobe Analytics for Streaming Media“ für Implementierungen, die nur auf Adobe Analytics basieren (wenn Edge nicht verwendet wird).

1. **Allgemeine Voraussetzungen erfüllen**<br>
Unabhängig davon, ob Sie Streaming-Medien-Services für Implementierungen auf Adobe Analytics oder für Edge-Implementierungen implementieren, stellen Sie sicher, dass Sie die [allgemeinen Voraussetzungen](/help/getting-started/prereqs.md) erfüllen.

1. **Vergewissern Sie sich, dass Sie über eine Adobe Analytics-Implementierung verfügen**<br>
Bei der Implementierung des Add-ons „Adobe Analytics for Streaming Media“ für eine reine Analytics-Implementierung ist auch eine Standardimplementierung von Adobe Analytics erforderlich. Weitere Informationen finden Sie unter [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de).

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie den Adobe Analytics-Support nach der URL des Medien-Tracking-Servers. Dies ist die `collection-api-server`-URL für die Mobile SDK, die JavaScript SDK und den Tracking-Server ohne Sammlungs-API für Roku. Domain-Namen für die API-Implementierung sind: `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie die aktuelle Media SDK herunter oder implementieren Sie die erforderlichen Erweiterungen**<br>
Abhängig vom Implementierungspfad [Laden Sie die aktuelle SDK herunter](/help/getting-started/download-sdks.md) für Web-, Mobil- oder Over-the-top-Plattformen. Die erforderlichen Erweiterungen müssen implementiert werden, um das Add-on Adobe Analytics for Streaming Media zu aktivieren.

1. **Adobe Analytics-Berichte aktivieren**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten](/help/implementation/media-sdk/setup/media-reports-enable.md).

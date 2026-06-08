---
title: Einrichten der Tag-Erweiterung „Web SDK" für Streaming-Medien
description: Konfigurieren Sie die Streaming-Mediensammlung in der Tag-Erweiterung "Adobe Experience Platform Web SDK".
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Einrichten der Tag-Erweiterung „Web SDK&quot; für Streaming-Medien

Mit der Tag-Erweiterung &quot;Adobe Experience Platform Web SDK&quot; können Sie die Streaming-Mediensammlung in der Datenerfassungs-Benutzeroberfläche ohne `alloy.js`-Konfigurations-Code konfigurieren. Auf dieser Seite wird die Konfiguration von Tags behandelt. Informationen zum Konfigurieren der Web-SDK im Code finden Sie unter [Einrichten der Web-SDK für Streaming-Medien](web-sdk.md).

* **Voraussetzungen**:
   * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
   * Installieren und konfigurieren Sie die Tag-Erweiterung „Web SDK&quot;. Siehe [Übersicht über die Tag-Erweiterung „Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview).

## Konfigurieren von Streaming-Medien in der Erweiterung

1. Öffnen Sie in der Datenerfassungs-UI Ihre Web-Eigenschaft und wählen Sie **[!UICONTROL Erweiterungen]** aus.
1. Wählen Sie in der installierten Erweiterung **Adobe Experience Platform Web SDK** die Option **[!UICONTROL Konfigurieren]**.
1. Erweitern Sie den **[!UICONTROL Streaming Media]** und legen Sie Folgendes fest:
   * **[!UICONTROL channel]**: Der bei jeder Sitzung gemeldete Kanalname.
   * **[!UICONTROL Player-Name]**: Der Name des verwendeten Medien-Players.
   * **[!UICONTROL Anwendungsversion]**: Die Version Ihrer Player-Anwendung.
   * **[!UICONTROL Haupt-Ping]** Intervall und **[!UICONTROL Anzeigen-Ping-Intervall]**: Die Ping-Kadenz (in Sekunden) für Hauptinhalte und Anzeigen.
1. Speichern Sie die Erweiterungskonfiguration und veröffentlichen Sie Ihre Änderungen.

## Medien-Events tracken

Senden Sie bei konfigurierter Erweiterung jedes Medienereignis mit der Aktion **[!UICONTROL Ereignis senden]** (oder dem `sendEvent`). Die **Payloads finden Sie auf der Registerkarte** Web[&#x200B; auf jeder &#x200B;](/help/implementation/events/overview.md)- und [&#128279;](/help/implementation/variables/overview.md).

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Übersicht über die Tag-Erweiterung „Web SDK&quot;](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [Einrichten der Web-SDK für Streaming-Medien (im Code)](web-sdk.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

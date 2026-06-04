---
title: Einrichten von iOS für Streaming-Medien mit Tags
description: Konfigurieren Sie die Streaming-Mediensammlung für iOS mit der Tag-Erweiterung "Adobe Streaming Media for Edge Network".
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Einrichten von iOS für Streaming-Medien mit Tags

Sie können die Streaming-Mediensammlung für Ihre iOS- oder tvOS-App über eine mobile Tags-Eigenschaft konfigurieren, wobei die Medieneinstellungen in der Datenerfassungs-Benutzeroberfläche verwaltet werden. Auf dieser Seite wird die Konfiguration von Tags behandelt. Informationen zum Konfigurieren der SDK im Code finden Sie unter [Einrichten von iOS für Streaming-Medien](ios.md).

* **Voraussetzungen**:
   * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
   * Erstellen Sie in der Datenerfassungs-UI eine Eigenschaft für Mobilgeräte. Siehe [Adobe Streaming Media für Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Konfigurieren Sie die Erweiterung

1. Öffnen Sie in der Datenerfassungs-UI Ihre Mobile-Eigenschaft und wählen Sie **[!UICONTROL Erweiterungen]** aus.
1. Suchen Sie auf der **[!UICONTROL Katalog]** die Erweiterung **Adobe Streaming Media for Edge Network** und wählen Sie **[!UICONTROL Installieren]** aus.
1. Legen Sie Folgendes fest und speichern Sie dann:
   * **[!UICONTROL channel]** - der bei jeder Sitzung gemeldete Kanalname.
   * **[!UICONTROL Player-Name]** - Der Name des verwendeten Medien-Players.
   * **[!UICONTROL Anwendungsversion]** - die Version Ihrer Player-Anwendung.
1. Veröffentlichen Sie Ihre Änderungen, fügen Sie dann die `AEPCore`-, `AEPEdge`-, `AEPEdgeIdentity`- und `AEPEdgeMedia` zu Ihrer App hinzu und registrieren Sie sie bei Mobile Core.

## Medien-Events tracken

Nachdem die Eigenschaft veröffentlicht und der Tracker erstellt wurde, verfolgen Sie jedes Medienereignis mit der Tracker-Methode. Die genauen Aufrufe finden Sie auf der Registerkarte **0[ auf jeder Seite ](/help/implementation/events/overview.md)Ereignis[ und ](/help/implementation/variables/overview.md)Variable .**

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media für Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Einrichten von iOS für Streaming-Medien (im Code)](ios.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

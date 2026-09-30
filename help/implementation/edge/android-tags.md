---
title: Einrichten von Android für Streaming-Medien mit Tags
description: Konfigurieren Sie die Streaming-Mediensammlung für Android mit der Tag-Erweiterung "Adobe Streaming Media for Edge Network".
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%
---
# Einrichten von Android für Streaming-Medien mit Tags

Sie können die Streaming-Mediensammlung für Ihre Android-App über eine mobile Tags-Eigenschaft konfigurieren, wobei die Medieneinstellungen in der Datenerfassungs-Benutzeroberfläche verwaltet werden. Auf dieser Seite wird die Konfiguration von Tags behandelt. Informationen zum Konfigurieren der SDK im Code finden Sie unter [Einrichten von Android für Streaming-Medien](android.md).

* **Voraussetzungen**:
  * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
  * Erstellen Sie in der Datenerfassungs-UI eine Eigenschaft für Mobilgeräte. Siehe [Adobe Streaming Media für Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Konfigurieren Sie die Erweiterung

1. Öffnen Sie in der Datenerfassungs-UI Ihre Mobile-Eigenschaft und wählen Sie **[!UICONTROL Erweiterungen]** aus.
1. Suchen Sie auf der **[!UICONTROL Katalog]** die Erweiterung **Adobe Streaming Media for Edge Network** und wählen Sie **[!UICONTROL Installieren]** aus.
1. Legen Sie Folgendes fest und speichern Sie dann:
   * **[!UICONTROL channel]**: der bei jeder Sitzung gemeldete Kanalname.
   * **[!UICONTROL Player-Name]**: Der Name des verwendeten Medien-Players.
   * **[!UICONTROL Anwendungsversion]**: die Version Ihrer Player-Anwendung.
1. Veröffentlichen Sie Ihre Änderungen, fügen Sie dann die `Core`-, `Edge`-, `EdgeIdentity`- und `EdgeMedia` zu Ihrer App hinzu und registrieren Sie sie bei Mobile Core.

## Medien-Events tracken

Nachdem die Eigenschaft veröffentlicht und der Tracker erstellt wurde, verfolgen Sie jedes Medienereignis mit der Tracker-Methode. Die genauen Aufrufe finden Sie auf der Registerkarte **0[&#x200B; auf jeder Seite &#x200B;](/help/implementation/events/overview.md)Ereignis[&#x200B; und &#x200B;](/help/implementation/variables/overview.md)Variable .**

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media für Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Einrichten von Android für Streaming-Medien (im Code)](android.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

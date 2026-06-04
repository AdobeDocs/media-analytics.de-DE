---
title: Einrichten von Android für Streaming-Medien
description: Konfigurieren Sie die Adobe Experience Platform Mobile SDK auf Android, um Streaming-Mediendaten an die Edge Network zu senden.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Einrichten von Android für Streaming-Medien

Die Erweiterung Adobe Streaming Media for Edge Network (`EdgeMedia`) erfasst Mediensessionsdaten in Ihrer Android-App und sendet sie an die Edge Network. Auf dieser Seite wird die In-Code-Konfiguration beschrieben. Informationen zum Konfigurieren des SDK über eine mobile Tags-Eigenschaft finden Sie unter [Einrichten von Android für Streaming-Medien mit Tags](android-tags.md).

* **Voraussetzungen**:
   * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
   * Fügen Sie die `Core`-, `Edge`-, `EdgeIdentity`- und `EdgeMedia`-Erweiterungen zu Ihrer App hinzu. Installation und Registrierung finden Sie unter [Adobe Streaming Media &#x200B;](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) Edge Network.

## Konfigurieren von Medien für Android

Legen Sie die Medienkonfigurationsschlüssel beim Initialisieren von SDK fest:

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

Erstellen Sie dann einen Tracker, um eine Mediensitzung zu verwalten:

```kotlin
val tracker = Media.createTracker()
```

Konfigurationsschlüssel und die vollständige Tracker-API finden Sie in der [Media for Edge Network-API-Referenz](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Medien-Events tracken

Verfolgen Sie bei erstelltem Tracker jedes Medienereignis mit der entsprechenden Tracker-Methode. Die genauen Aufrufe finden Sie auf der Registerkarte **0[&#x200B; auf jeder Seite &#x200B;](/help/implementation/events/overview.md)Ereignis[&#x200B; und &#x200B;](/help/implementation/variables/overview.md)Variable .**

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media für Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Einrichten von Android für Streaming-Medien mit Tags](android-tags.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)

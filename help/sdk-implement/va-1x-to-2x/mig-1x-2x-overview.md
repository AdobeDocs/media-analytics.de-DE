---
title: Migrationsübersicht
description: Erfahren Sie mehr über die Migration von 1.x zu 2.x-Versionen des Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 94%

---

# Migrationsübersicht{#migration-overview}

Die Migration von VHL 1.x zu VHL 2.x ist dank vereinfachter APIs für Initialisierung, Konfiguration und Player-Delegates unkompliziert.

Im Folgenden finden Sie die Unterschiede zwischen den Versionen 1.x und 2.x:

* **Plugins, Delegates:** Sie müssen keine Plugins und Delegates mehr für Analytics, VideoPlayer und Heartbeat implementieren.
* **Konfiguration:** Sie müssen keine Konfigurationen mehr für die 1.x-Plugins instanziieren.

## Vorteile von 2.x {#benefits-of-two-x}

* Alle öffentlichen Methoden sind in der Klasse `MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern.
* Alle Konfigurationen sind nun in der Klasse `MediaHeartbeatConfig` konsolidiert.
* Sie müssen die Konfigurationen für die Analytics-, VideoPlayer- und Heartbeat-Plug-ins nicht mehr instanziieren. Sie müssen die `MediaHeartbeat`-Klasse nur mit den `MediaHeartbeatDelegate`- und `MediaHeartbeatConfig`-Instanzen instanziieren. Dies ist die einzige erforderliche Implementierung zur Initialisierung von Media Analytics.

   Mit der Initialisierung von `MediaHeartbeat` können Sie die gesamte Implementierung für die Analytics-, VideoPlayer- und Heartbeat-Plug-ins löschen. Entfernen Sie außerdem die gesamte vorhandene Implementierung für die Initialisierung, die ein Array von Plug-ins als Eingabe akzeptiert. Unter [Codevergleich: 1.x gegenüber 2.x](./code-comparison-1x-2x.md) finden Sie einen Direktvergleich der 1.x- und 2.x-Implementierungen.

Die neuen APIs in 2.x sind hier detailliert beschrieben: [Konversion von API 1.x zu 2.x](./1x-2x-api-change.md).

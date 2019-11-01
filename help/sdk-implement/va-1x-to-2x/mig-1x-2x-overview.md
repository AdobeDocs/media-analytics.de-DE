---
title: Migrationsübersicht
description: Dieses Thema bietet einen Überblick über die Migration von 1.x auf 2.x-Versionen des Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Migrationsübersicht{#migration-overview}

Die Migration von VHL 1.x zu VHL 2.x ist dank vereinfachter APIs für Initialisierung, Konfiguration und Player-Delegates unkompliziert.

Im Folgenden finden Sie die Unterschiede zwischen den Versionen 1.x und 2.x:

* **Plugins, Delegates:** Sie müssen keine Plugins und Delegates mehr für Analytics, VideoPlayer und Heartbeat implementieren.
* **Konfiguration:** Sie müssen keine Konfigurationen mehr für die 1.x-Plugins instanziieren.

## Vorteile von 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Sie müssen keine Konfigurationen mehr für die Analytics-, VideoPlayer- und Heartbeat-Zusatzmodule instanziieren. Sie müssen die `MediaHeartbeat` Klasse nur mit `MediaHeartbeatDelegate` und `MediaHeartbeatConfig` Instanzen instanziieren. Dies ist die einzige Implementierung, die zum Initialisieren von Media Analytics erforderlich ist.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Entfernen Sie außerdem die gesamte vorhandene Implementierung für die Initialisierung, die ein Array von Plugins als Eingabe akzeptiert. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Die neuen APIs in 2.x sind hier detailliert beschrieben: [Konversion von API 1.x zu 2.x](./1x-2x-api-change.md).

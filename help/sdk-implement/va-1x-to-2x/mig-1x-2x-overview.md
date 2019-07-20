---
seo-title: Migrationsübersicht
title: Migrationsübersicht
uuid: d 84 f 55 bc-fa 90-45 c 1-b 97 d-cb 5 fe 58 e 80 c 0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Migrationsübersicht{#migration-overview}

Die Migration von VHL 1.x zu VHL 2.x ist dank vereinfachter APIs für Initialisierung, Konfiguration und Player-Delegates unkompliziert.

Im Folgenden finden Sie die Unterschiede zwischen den Versionen 1.x und 2.x:

* **Plugins, Delegates:** Sie müssen keine Plugins und Delegates mehr für Analytics, VideoPlayer und Heartbeat implementieren.
* **Konfiguration:** Sie müssen keine Konfigurationen mehr für die 1.x-Plugins instanziieren.

## Benefits of 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Sie müssen keine Konfigurationen mehr für die Analytics-, videoplayer- und Heartbeat-Plugins instanziieren. You only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. Dies ist die einzige Implementierung, die zum Initialisieren von Media Analytics erforderlich ist.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Entfernen Sie außerdem alle vorhandenen Implementierungen für die Initialisierung, die ein Array von Plugins als Eingabe akzeptiert. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Die neuen APIs in 2.x sind hier detailliert beschrieben: [Konversion von API 1.x zu 2.x](./1x-2x-api-change.md).

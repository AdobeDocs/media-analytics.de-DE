---
title: Migrationsübersicht
description: Erfahren Sie mehr über die Migration von 1.x zu 2.x-Versionen des Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 87%

---

# Übersicht der Legacy-Migration für VHL 1.x zu VHL 2.x {#migration-overview}

Die Migration von VHL 1.x zu VHL 2.x ist dank vereinfachter APIs für Initialisierung, Konfiguration und Player-Delegates unkompliziert

Im Folgenden finden Sie die Unterschiede zwischen den Versionen 1.x und 2.x:

* **Plug-ins, Delegaten -** Sie müssen keine Plug-ins und Delegaten mehr für Analytics, VideoPlayer und Heartbeat implementieren.
* **Konfiguration -** Sie müssen die Konfigurationen für die 1.x-Plug-ins nicht mehr instanziieren.

## Vorteile von 2.x {#benefits-of-two-x}

* Alle öffentlichen Methoden sind in der Klasse `MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern.
* Alle Konfigurationen sind nun in der Klasse `MediaHeartbeatConfig` konsolidiert.
* Sie müssen die Konfigurationen für die Analytics-, VideoPlayer- und Heartbeat-Plug-ins nicht mehr instanziieren. Sie müssen die `MediaHeartbeat`-Klasse nur mit den `MediaHeartbeatDelegate`- und `MediaHeartbeatConfig`-Instanzen instanziieren. Dies ist die einzige erforderliche Implementierung zur Initialisierung von Media Analytics.

  Mit der Initialisierung von `MediaHeartbeat` können Sie die gesamte Implementierung für die Analytics-, VideoPlayer- und Heartbeat-Plug-ins löschen. Entfernen Sie außerdem die gesamte vorhandene Implementierung für die Initialisierung, die ein Array von Plug-ins als Eingabe akzeptiert. Unter [Codevergleich: 1.x gegenüber 2.x](./code-comparison-1x-2x.md) finden Sie einen Direktvergleich der 1.x- und 2.x-Implementierungen.

Die neuen APIs in 2.x sind hier detailliert beschrieben: [Konversion von API 1.x zu 2.x](./1x-2x-api-change.md).

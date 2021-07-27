---
title: Senden von QoE-Daten
description: Erfahren Sie mehr über das Senden von Ereignissen mit einem JSON-Schlüssel „qoeData“.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Senden von QoE-Daten {#sending-qoe-data}

Jedes Ereignis kann mit einem zusätzlichen JSON-Schlüssel namens `qoeData` ausgestattet werden, der sich im JSON-Anfrageinhalt neben dem `params`-Schlüssel befindet.

>[!NOTE]
>
>Sie sollten die [JSON-Validierungsschemas](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) überprüfen, um Parametertypen zu verifizieren und herauszufinden, ob sie erforderlich oder optional sind.

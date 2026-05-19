---
title: Timeout-Bedingungen
description: Erfahren Sie mehr über die Zeitüberschreitungsbedingungen der Mediensammlungs-API.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# Timeout-Bedingungen{#timeout-conditions}

**Timeout-Bedingungen für die Media Collection API**

Die Media Collection API verfügt als zustandlose API nicht über den gleichen Mechanismus zur Vergabe einer neuen Sitzungs-ID bei Timeout-Bedingungen wie das Media SDK. Wenn eine Zeitüberschreitungsbedingung auftritt, wird die Sitzung vom Back-End geschlossen und alle nachfolgenden Aufrufe, die mit dieser Sitzungs-ID getätigt werden, werden entfernt. Die Logik, die ein Sitzungs-Timeout verarbeitet, muss im Client gehandhabt werden. Das heißt, der Player muss die Zeitüberschreitungsbedingungen überwachen und eine neue Sitzungs-ID abrufen, wenn eine Zeitüberschreitung auftritt.

* **10 Minuten ohne API-Ereignisse**

  Wenn das Backend keine API-Ereignisse empfängt, schließt es die Sitzung.
* **30 Minuten ohne Änderung der Abspielleiste**

  Wenn sich die Abspielleiste 30 Minuten lang nicht verändert (z. B. wenn der Benutzer die Wiedergabe anhält und das Gerät verlässt), schließt das Backend die Sitzung.

>[!NOTE]
>
>Sie können das Sitzungsende auch erzwingen, indem Sie eine `events`-Anforderung mit dem Ereignistyp `sessionEnd` senden.

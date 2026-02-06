---
title: Timeout-Bedingungen
description: Erfahren Sie mehr über die Zeitüberschreitungsbedingungen der Mediensammlungs-API.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '165'
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

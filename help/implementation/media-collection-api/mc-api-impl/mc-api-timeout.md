---
title: Timeout-Bedingungen
description: Erfahren Sie mehr über die Zeitüberschreitungsbedingungen der Mediensammlungs-API.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 95%

---

# Timeout-Bedingungen{#timeout-conditions}

**Timeout-Bedingungen für die Media Collection API**

Die Media Collection API verfügt als zustandlose API nicht über den gleichen Mechanismus zur Vergabe einer neuen Sitzungs-ID bei Timeout-Bedingungen wie das Media SDK. Wenn eine Timeout-Bedingung erfüllt ist, schließt das Backend die Sitzung und alle nachfolgenden Aufrufe mit dieser Sitzungs-ID werden verworfen. Die Logik, die Sitzungs-Timeouts verarbeitet, muss sich auf dem Client befinden. Somit muss der Player die Timeout-Bedingungen überwachen und bei Timeouts eine neue Sitzungs-ID anfordern.

* **10 Minuten ohne API-Ereignisse**

  Wenn das Backend keine API-Ereignisse empfängt, schließt es die Sitzung.
* **30 Minuten ohne Änderung der Abspielleiste**

  Wenn sich die Abspielleiste 30 Minuten lang nicht verändert (z. B. wenn der Benutzer die Wiedergabe anhält und das Gerät verlässt), schließt das Backend die Sitzung.

>[!NOTE]
>
>Sie können das Sitzungsende auch erzwingen, indem Sie eine `events`-Anforderung mit dem Ereignistyp `sessionEnd` senden.

---
title: Timeout-Bedingungen
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Timeout-Bedingungen{#timeout-conditions}

**Zeitlimitbedingungen für Medienkollektions-API**

Da die Medienkollektions-API stateless ist, verfügt sie nicht über denselben Mechanismus wie das Media SDK für die Ausgabe einer neuen Sitzungs-ID, wenn Timeout-Bedingungen auftreten. Wenn eine Timeout-Bedingung erfüllt ist, schließt das Backend die Sitzung und alle nachfolgenden Aufrufe mit dieser Sitzungs-ID werden verworfen. Die Logik, die Sitzungs-Timeouts verarbeitet, muss sich auf dem Client befinden. Somit muss der Player die Timeout-Bedingungen überwachen und bei Timeouts eine neue Sitzungs-ID anfordern.

* **10 Minuten: Keine API-Ereignisse**

   Wenn das Back-End keine API-Ereignisse erhält, wird die Sitzung geschlossen.
* **30 Minuten: Keine Änderung am Abspielkopf**

   Wenn sich der Abspielkopf 30 Minuten lang nicht bewegt (z. B. wenn der Benutzer Pause trifft und weggeht), wird die Sitzung am Ende geschlossen.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.


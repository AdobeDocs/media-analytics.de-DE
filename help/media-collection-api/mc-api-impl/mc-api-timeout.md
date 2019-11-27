---
title: Timeout-Bedingungen
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Timeout-Bedingungen {#timeout-conditions}

**Timeout-Bedingungen für die Media Collection API**

Die Media Collection API verfügt als zustandlose API nicht über den gleichen Mechanismus zur Vergabe einer neuen Sitzungs-ID bei Timeout-Bedingungen wie das Media SDK. Wenn eine Timeout-Bedingung erfüllt ist, schließt das Backend die Sitzung und alle nachfolgenden Aufrufe mit dieser Sitzungs-ID werden verworfen. Die Logik, die Sitzungs-Timeouts verarbeitet, muss sich auf dem Client befinden. Somit muss der Player die Timeout-Bedingungen überwachen und bei Timeouts eine neue Sitzungs-ID anfordern.

* **10 Minuten ohne API-Ereignisse**

   Wenn das Backend keine API-Ereignisse empfängt, schließt es die Sitzung.
* **30 Minuten ohne Änderung der Abspielleiste**

   Wenn sich die Abspielleiste 30 Minuten lang nicht verändert (z. B. wenn der Benutzer die Wiedergabe anhält und das Gerät verlässt), schließt das Backend die Sitzung.

>[!NOTE]
>
>Sie können das Sitzungsende auch erzwingen, indem Sie eine `events`-Anforderung mit dem Ereignistyp `sessionEnd` senden.


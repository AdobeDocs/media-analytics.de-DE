---
seo-title: Timeout-Bedingungen
title: Timeout-Bedingungen
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Timeout-Bedingungen{#timeout-conditions}

**Media Collection-API-Timeout-Bedingungen**

Die Media Collection-API hat nicht den gleichen Mechanismus wie das Media SDK für die Ausgabe einer neuen Sitzungs-ID, wenn Zeitüberschreitungsbedingungen eintreten. Wenn eine Timeout-Bedingung erfüllt ist, schließt das Backend die Sitzung und alle nachfolgenden Aufrufe mit dieser Sitzungs-ID werden verworfen. Die Logik, die Sitzungs-Timeouts verarbeitet, muss sich auf dem Client befinden. Somit muss der Player die Timeout-Bedingungen überwachen und bei Timeouts eine neue Sitzungs-ID anfordern.

* **10 Minuten: Keine API-Ereignisse**

   Wenn das Back-End keine API-Ereignisse empfängt, schließen Sie die Sitzung.
* **30 Minuten: Keine Abspielkopfzeile**

   Wenn die Abspielleiste 30 Minuten lang nicht bewegt wird (d. h. der Benutzer hält die Pause an und geht sie weg), schließt das Back-Ende die Sitzung.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.


---
seo-title: Test 2 Media-Unterbrechung
title: Test 2 Media-Unterbrechung
uuid: eeccd 344-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 2: Medienunterbrechung{#test-media-interruption}

Dieser Testfall ist im Rahmen des Anfrageformulars für die Zertifizierung erforderlich und überprüft das Unterbrechungsverhalten auf Mobilgeräten.

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Starten des Medienplayers**

   Wenn der Medienplayer gestartet wird, werden die folgenden Aufrufe in der folgenden Reihenfolge gesendet:

   1. Media Analytics-Start
   1. Heartbeat-Start
   1. Heartbeat-Analyse-Start
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **Medien-Hauptinhalt für mindestens 5 Minuten wiedergeben**

   **Content Play**

   Während der normalen Wiedergabe des Hauptinhalts werden alle zehn Sekunden Heartbeat-Aufrufe an den Heartbeat-Server gesendet.

   Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **App oder Browser im Hintergrund ausführen**

   Während die App im Hintergrund ausgeführt wird, sollten ab VHL-Version 1.6.6 nur „main:pause“-Aufrufe an den Heartbeat-Server gesendet werden.

1. **App oder Browser erneut anzeigen**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Medien-Hauptinhalt für mindestens 5 Minuten wiedergeben**

   Aufrufparameter und Metadaten finden Sie unter [Testrufdetails.](/help/sdk-implement/validation/test-call-details.md)

1. **Schließen des Medienplayers**

   Nachdem der Medienplayer geschlossen wurde, werden keine zusätzlichen Verfolgungsaufrufe ausgelöst.


---
seo-title: Test 2 Video-Unterbrechung
title: Test 2 Video-Unterbrechung
uuid: eeccd 344-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Test 2: Videounterbrechung{#test-video-interruption}

Dieser Testfall ist im Rahmen des Anfrageformulars für die Zertifizierung erforderlich und überprüft das Unterbrechungsverhalten auf Mobilgeräten.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Videoplayer starten**

   Wenn der Videoplayer gestartet wird, werden die Aufrufe in folgender Reihenfolge gesendet:

   1. Media Analytics-Start
   1. Heartbeat-Start
   1. Heartbeat-Analyse-Start
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Hauptinhaltsvideo mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   **Content Play**

   Während der normalen Wiedergabe des Hauptinhalts werden alle zehn Sekunden Heartbeat-Aufrufe an den Heartbeat-Server gesendet.

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **App oder Browser im Hintergrund ausführen**

   Während die App im Hintergrund ausgeführt wird, sollten ab VHL-Version 1.6.6 nur „main:pause“-Aufrufe an den Heartbeat-Server gesendet werden.

1. **App oder Browser erneut anzeigen**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Hauptinhaltsvideo mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **Videoplayer schließen**

   Nachdem das Video geschlossen wurde, sollten keine zusätzlichen Tracking-Aufrufe mehr ausgelöst werden.


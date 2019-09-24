---
seo-title: Medien-Unterbrechung testen 2
title: Medien-Unterbrechung testen 2
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Medienunterbrechung{#test-media-interruption}

In diesem Testfall wird das Verhalten der mobilen Unterbrechung überprüft. Dies ist ein erforderliches Element Ihrer Zertifizierungsanforderung.

## Zertifizierungsantrag

**Hier können Sie das Zertifizierungsanforderungsformular herunterladen: ==&gt;** Formular für die [Zertifizierungsanforderung.](cert_req_form.docx)

## Prüfverfahren

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Medienplayer starten**

   Beim Start des Medienplayers werden die folgenden Aufrufe in der folgenden Reihenfolge gesendet:

   1. Adobe Analytics (AppMeasurement) Start
   1. Media Analytics (Heartbeats) Start
   1. Media Analytics (Heartbeats) - Adobe Analytics Start-Aufruf angefordert
   Die ersten beiden Aufrufe oben enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Der dritte Aufruf oben teilt dem Medienanalyseserver mit, dass das Media SDK angefordert hat, den Adobe Analytics Start-Aufruf (`pev2=ms_s`) an den Adobe Analytics-Server zu senden.

1. **Hauptinhalt mindestens 5 Minuten ununterbrochen wiedergeben**

   **Content Play**

   Während der Inhaltswiedergabe sendet das Media SDK alle zehn Sekunden Wiedergabeaufrufe (Heartbeats) an den Medienanalyseserver.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **App oder Browser im Hintergrund ausführen**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **App oder Browser wieder in den Vordergrund rücken**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Medien mit Hauptinhalt mindestens 5 Minuten ununterbrochen abspielen**

   Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Medienplayer schließen**

   Nach dem Schließen des Medienplayers sollten keine weiteren Verfolgungsaufrufe ausgelöst werden.


---
seo-title: Test 2 Media-Unterbrechung
title: Test 2 Media-Unterbrechung
uuid: eeccd 344-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Medienunterbrechung{#test-media-interruption}

In diesem Testfall wird das Verhalten von Mobilgeräten überprüft. Es ist ein erforderliches Element Ihrer Zertifizierungsanforderung.

## Zertifizierungsanforderungsformular

**Laden Sie das Zertifikatanforderungsformular hier herunter: = = &gt;**  [Zertifizierungsanforderungsformular.](cert_req_form.docx)

## Testverfahren

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Starten des Medienplayers**

   Wenn der Medienplayer gestartet wird, werden die folgenden Aufrufe in der folgenden Reihenfolge gesendet:

   1. Adobe Analytics (appmeasurement) starten
   1. Media Analytics (Heartbeats) starten
   1. Media Analytics (Heartbeats) Adobe Analytics Start-Aufruf angefordert
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Der dritte oben genannte Aufruf teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, dass der Adobe Analytics Start-Aufruf (`pev2=ms_s`) an den Adobe Analytics-Server gesendet wird.

1. **Hauptinhalt für mindestens 5 Minuten wiedergeben**

   **Content Play**

   Während der Wiedergabe von Inhalten sendet das Media SDK alle zehn Sekunden Play-Aufrufe (Heartbeats) an den Media Analytics-Server.

   Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **App oder Browser im Hintergrund ausführen**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **App oder Browser zurück zum Vordergrund bringen**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Medien-Hauptinhalt für mindestens 5 Minuten wiedergeben**

   Aufrufparameter und Metadaten finden Sie unter [Testrufdetails.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Schließen des Medienplayers**

   Nachdem der Medienplayer geschlossen wurde, werden keine zusätzlichen Verfolgungsaufrufe ausgelöst.


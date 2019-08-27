---
seo-title: Test 1 Standard-Wiedergabe
title: Test 1 Standard-Wiedergabe
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Test 1: Standardwiedergabe{#test-standard-playback}

In diesem Testfall wird die allgemeine Wiedergabe und Sequenzierung überprüft. Es ist ein erforderliches Element Ihrer Zertifizierungsanforderung.

## Zertifizierungsanforderungsformular

**Laden Sie das Zertifikatanforderungsformular hier herunter: = = &gt;**  [Zertifizierungsanforderungsformular.](cert_req_form.docx)

## Zertifizierungstest 1 Übersicht

Die Implementierungen von Media Analytics umfassen zwei Arten von Tracking-Aufrufen:
* Aufrufe direkt an Ihren Adobe Analytics (appmeasurement)-Server - Diese Aufrufe erfolgen auf "Media Start" - und" Ad Start" -Ereignissen.
* Aufrufe an den Media Analytics-Server (Heartbeats) - Diese beinhalten In-Band- und Out-of-Band-Aufrufe:
   * In-Band - Das SDK sendet zeitgesteuerte Play-Aufrufe oder "Pings" bei 10-Sekunden-Intervallen während der Wiedergabe von Inhalten und in einer Intervallen von 1 Sekunden während der Anzeige.
   * Out-of-Band - Diese Aufrufe können jederzeit erfolgen und umfassen Pause, Pufferung, Fehler, Inhaltsbeendigungen, Anzeigenbeendigung usw.

>[!NOTE]
>Die Medienverfolgung verhält sich auf allen Plattformen gleich.

## Testverfahren

Schließen Sie die folgenden Aktionen ab (in der Reihenfolge):

1. **Seite oder App laden**

   **Tracking-Server** (für alle Websites und mobilen Apps):

   * **Adobe Analytics (appmeasurement)-Server -** Ein RDC-Tracking-Server oder CNAME, der zu einem RDC-Tracking-Server aufgelöst wird, ist für den Experience Cloud Besucher-ID-Dienst erforderlich. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats)-Server -** Dieser Server hat immer das Format "`[namespace].hb.omtrdc.net`, wobei `[namespace]` Ihr Firmenname angegeben wird. Dieser Name wird von Adobe bereitgestellt.
   Sie müssen bestimmte wichtige Variablen überprüfen, die über alle Verfolgungsaufrufe hinweg universell sind:

   **Adobe Besucher-ID (`mid`):** Die `mid` Variable wird verwendet, um den Wert zu erfassen, der im AMCV-Cookie festgelegt ist. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Es findet sich in Adobe Analytics- (appmeasurement) und Media Analytics-Aufrufen (Heartbeats).

   * **Adobe Analytics Start-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Website-Seitenaufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Lebenszyklus-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics-Startanruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Bei Media Analytics Start-Aufrufen (`s:event:type=start`) sind die `mid` Werte möglicherweise nicht vorhanden. Das ist in Ordnung. Sie werden ggf. erst angezeigt, wenn die Media Analytics-Play-Aufrufe ( `s:event:type=play`) vorhanden sind.

   * **Media Analytics Play-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Starten des Medienplayers**

   Wenn der Medienplayer beginnt, sendet das Media SDK die Schlüsselaufrufe an die beiden Server in der folgenden Reihenfolge:

   1. Adobe Analytics-Server - Start-Aufruf
   1. Media Analytics-Server - Start-Aufruf
   1. Media Analytics-Server - "Adobe Analytics Startanruf angefordert «
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Der dritte oben genannte Aufruf teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, dass der Adobe Analytics Start-Aufruf (`pev2=ms_s`) an den Adobe Analytics-Server gesendet wird.

1. **Werbeunterbrechung anzeigen (sofern verfügbar)**

   * **Ad Start**
   Wenn die Anzeige beginnt, werden die folgenden Schlüsselaufrufe in der folgenden Reihenfolge gesendet:

   1. Adobe Analytics-Server - Ad-Start-Aufruf
   1. Media Analytics-Server - Anzeigenstart-Aufruf
   1. Media Analytics-Server - "Adobe Analytics Ad Start-Aufruf angefordert «
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   Der dritte Aufruf teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, dass der Adobe Analytics Ad Start-Aufruf (`pev2=msa_s`) an den Adobe Analytics-Server gesendet wird.

   * **Ad Play**

      Während der Anzeigenwiedergabe sendet das Media Analytics-SDK jede Sekunde mit dem Media Analytics-SDK auf den Media Analytics-Server.

   * **Ad Complete**

      Bei einer Anzeige von 100% sollte ein Media Analytics Complete-Aufruf gesendet werden.



1. **Werbewiedergabe mindestens 30 Sekunden lang anhalten, sofern verfügbar.**  **Ad Pause**

   Während der Anzeige werden die Media Analytics-Heartbeat- oder "ping" -Aufrufe vom SDK jede Sekunde an den Media Analytics-Server gesendet.

   >[!NOTE]
   >
   >Der Wert der Abspielleiste sollte während der Pause konstant bleiben.

   Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Hauptinhalt für 10 Minuten wiedergeben.**  **Content Play**

   Während der Wiedergabe des Hauptinhalts sendet das Media SDK Heartbeats (Play-Aufrufe) alle 10 Sekunden an den Media Analytics-Server.

   Hinweise:

   * Die Position der Abspielleiste sollte bei jedem Play-Aufruf um 10 erhöht werden.
   * Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

      Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Wiedergabe mindestens 30 Sekunden lang anhalten.** Bei Anhalten des Medienplayers werden die Ereignisaufrufe vom SDK alle 10 Sekunden vom SDK an den Media Analytics-Server gesendet. Wird das Video fortgesetzt, sollten erneut Wiedergabeereignisse gesendet werden.

   Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Suchen/Scrubben von Medien.** Beim Scrubbing von Medien-Playhead werden keine speziellen Verfolgungsaufrufe gesendet, wenn die Medienwiedergabe nach dem Scrubbing fortgesetzt wird. Der Wert der Abspielleiste sollte die neue Position im Hauptinhalt widerspiegeln.

1. **Medien wiedergeben (nur VOD)** Wenn Medien wiederholt werden, sollte ein neuer Satz von Media Start-Aufrufen gesendet werden (als wäre dies ein Neustart).

1. **Zeigen Sie die nächsten Medien in der Wiedergabeliste an.** Beim Medienstart der nächsten Medien in einer Wiedergabeliste sollte ein neuer Satz von Media Start-Aufrufen gesendet werden.

1. **Medien oder Stream wechseln** Beim Wechsel von Live-Streams sollte ein Media Analytics-complete-Aufruf des ersten Streams nicht gesendet werden. Die Media Start-Aufrufe und Play-Aufrufe sollten mit der neuen Ansicht und dem Stream-Namen beginnen und mit den korrekten Werten für Abspielkopf und Dauer für die neue Anzeige beginnen.


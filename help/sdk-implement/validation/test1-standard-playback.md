---
seo-title: Test 1 Standard-Wiedergabe
title: Test 1 Standard-Wiedergabe
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Test 1: Standardwiedergabe{#test-standard-playback}

In diesem Testfall werden die allgemeine Wiedergabe und Sequenzierung validiert. Dies ist ein erforderliches Element Ihrer Zertifizierungsanforderung.

## Zertifizierungsantrag

**Hier können Sie das Zertifizierungsanforderungsformular herunterladen: ==&gt;** Formular für die [Zertifizierungsanforderung.](cert_req_form.docx)

## Zertifizierungstest 1 - Überblick

Media Analytics-Implementierungen umfassen zwei Arten von Verfolgungsaufrufen:
* Aufrufe, die direkt an Ihren Adobe Analytics-Server (AppMeasurement) gesendet werden - Diese Aufrufe erfolgen bei "Media Start"- und "Ad Start"-Ereignissen.
* Aufrufe des Media Analytics-Servers (Heartbeats) - Dazu gehören In-Band- und Out-of-Band-Aufrufe:
   * In-Band - Das SDK sendet zeitgesteuerte Wiedergabe-Aufrufe oder "Pings"in Intervallen von 10 Sekunden während der Inhaltswiedergabe und in Intervallen von einer Sekunde während der Anzeige.
   * Out-of-Band-Aufrufe: Diese Aufrufe können zu jedem beliebigen Zeitpunkt erfolgen und umfassen Pause, Pufferung, Fehler, Inhaltsbeendigung, Anzeigenbeendigung usw.

>[!NOTE]
>Die Medienverfolgung verhält sich auf allen Plattformen gleich.

## Prüfverfahren

Führen Sie die folgenden Aktionen aus und zeichnen Sie sie auf (in der richtigen Reihenfolge):

1. **Seite oder App laden**

   **Tracking-Server** (für alle Websites und mobilen Apps):

   * **Adobe Analytics (AppMeasurement)-Server -** Ein RDC-Tracking-Server oder CNAME, der zu einem RDC-Tracking-Server aufgelöst wird, ist für den Experience Cloud-Besucher-ID-Dienst erforderlich. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats)-Server -** Dieser Server hat immer das Format "`[namespace].hb.omtrdc.net`", wobei der Name Ihres Unternehmens `[namespace]` angegeben wird. Dieser Name wird von Adobe bereitgestellt.
   Sie müssen bestimmte Schlüsselvariablen validieren, die für alle Verfolgungsaufrufe universell sind:

   **`mid`Adobe-Besucher-ID (**): Die `mid` Variable wird verwendet, um den im AMCV-Cookie festgelegten Wert zu erfassen. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Sie finden sie sowohl in Adobe Analytics- (AppMeasurement) als auch in Media Analytics- (Heartbeats-) Aufrufen.

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

   * **Media Analytics Start-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Bei Media Analytics Start-Aufrufen (`s:event:type=start`) sind die `mid` Werte möglicherweise nicht vorhanden. Das ist in Ordnung. Sie werden möglicherweise erst angezeigt, wenn Media Analytics Play aufruft ( `s:event:type=play`).

   * **Media Analytics Play-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Medienplayer starten**

   Beim Starten des Medienplayers sendet das Media SDK die Schlüsselaufrufe in der folgenden Reihenfolge an die beiden Server:

   1. Adobe Analytics-Server - Start-Aufruf
   1. Media Analytics-Server - Start-Aufruf
   1. Media Analytics-Server - "Adobe Analytics-Startaufruf angefordert"
   Die ersten beiden Aufrufe oben enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Der dritte Aufruf oben teilt dem Medienanalyseserver mit, dass das Media SDK angefordert hat, den Adobe Analytics Start-Aufruf (`pev2=ms_s`) an den Adobe Analytics-Server zu senden.

1. **Werbeunterbrechung anzeigen (sofern verfügbar)**

   * **Ad Start**
   Beim Start der Anzeige werden die folgenden Tastenaufrufe in der folgenden Reihenfolge gesendet:

   1. Adobe Analytics-Server - Ad Start-Aufruf
   1. Medienanalyseserver - Ad-Start-Aufruf
   1. Media Analytics-Server - "Adobe Analytics Ad Start-Aufruf angefordert"
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   Der dritte Aufruf teilt dem Medienanalyseserver mit, dass das Media SDK angefordert hat, den Adobe Analytics Ad Start-Aufruf (`pev2=msa_s`) an den Adobe Analytics-Server zu senden.

   * **Ad Play**

      Während der Wiedergabe der Anzeige sendet das Media Analytics-SDK alle Sekunden Wiedergabeereignisse des Typs "Anzeige"an den Media Analytics-Server.

   * **Ad Complete**

      Am 100 %-Punkt einer Anzeige sollte ein Media Analytics Complete-Aufruf gesendet werden.



1. **Werbewiedergabe mindestens 30 Sekunden lang anhalten, sofern verfügbar.**  **Ad Pause**

   Während der Werbeunterbrechung werden Media Analytics-Heartbeat- oder Ping-Aufrufe vom SDK jede Sekunde an den Medienanalyseserver gesendet.

   >[!NOTE]
   >
   >Der Wert der Abspielleiste sollte während der Pause konstant bleiben.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Wiedergabe des Hauptinhalts für 10 Minuten ohne Unterbrechung.**  **Content Play**

   Während der Wiedergabe des Hauptinhalts sendet das Media SDK alle 10 Sekunden Heartbeats (Wiedergabe-Aufrufe) an den Medienanalyseserver.

   Hinweise:

   * Die Position der Abspielleiste sollte bei jedem Play-Aufruf um 10 erhöht werden.
   * Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

      Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Wiedergabe mindestens 30 Sekunden lang anhalten.** Beim Anhalten des Medienplayers sendet das SDK alle 10 Sekunden Ereignisaufrufe an den Medienanalyseserver. Wird das Video fortgesetzt, sollten erneut Wiedergabeereignisse gesendet werden.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter Details zu [Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Medien suchen/scrubben.** Beim Scrubbing der Medienabspielposition werden keine besonderen Verfolgungsaufrufe gesendet. Wenn die Medienwiedergabe nach dem Scrubbing fortgesetzt wird, sollte der Wert der Abspielleiste die neue Position im Hauptinhalt widerspiegeln.

1. **Wiedergabemedien (nur VOD).** Wenn Medien wiedergegeben werden, sollte ein neuer Satz von Media Start-Aufrufen gesendet werden (als wäre dies ein Neustart).

1. **Nächste Medien in der Wiedergabeliste anzeigen.** Beim Medienstart des nächsten Mediums in einer Wiedergabeliste sollte ein neuer Satz von Media Start-Aufrufen gesendet werden.

1. **Wechseln Sie zwischen Medien oder Stream.** Beim Wechseln von Live-Streams sollte kein Media Analytics-complete-Aufruf für den ersten Stream gesendet werden. Die Media Start-Aufrufe und die Wiedergabe-Aufrufe sollten mit dem neuen Anzeige- und Stream-Namen und mit den richtigen Abspielkopf- und Zeitwerten für die neue Sendung beginnen.


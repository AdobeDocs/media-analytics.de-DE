---
title: Test 1 Standardwiedergabe
description: Erfahren Sie mehr über den Standardwiedergabetest, der bei der Validierung verwendet wird.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 100%

---

# Test 1: Standardwiedergabe{#test-standard-playback}

In diesem Testfall werden die allgemeine Wiedergabe und Sequenzierung validiert.

Media Analytics-Implementierungen umfassen zwei Arten von Tracking-Aufrufen:
* Aufrufe, die direkt an Ihren Adobe Analytics (AppMeasurement)-Server gesendet werden. Diese Aufrufe erfolgen bei „Medienstart“- und „Anzeigenstart“-Ereignissen.
* Aufrufe an den Media Analytics (Heartbeats)-Server. Dazu gehören In-Band- und Out-of-Band-Aufrufe:
   * In-Band-Aufrufe: Das SDK sendet zeitgesteuerte Wiedergabeaufrufe oder „Pings“ in Intervallen von 10 Sekunden während der Inhaltswiedergabe und in Intervallen von einer Sekunde während Anzeigen.
   * Out-of-Band-Aufrufe: Diese Aufrufe können zu jedem beliebigen Zeitpunkt erfolgen und umfassen Pause, Pufferung, Fehler, Inhaltsbeendigung, Anzeigenbeendigung usw.

>[!NOTE]
>Das Medien-Tracking verhält sich auf allen Plattformen gleich.

## Testverfahren

Führen Sie die folgenden Aktionen aus und zeichnen Sie sie auf (in der angegebenen Reihenfolge):

1. **Seite oder App laden**

   **Tracking-Server** (für alle Websites und mobilen Apps):

   * **Adobe Analytics (AppMeasurement)-Server:** Ein RDC-Tracking-Server bzw. ein CNAME, der aufgelöst auf einen RDC-Tracking-Server verweist, ist für den Experience Cloud-Besucher-ID-Dienst erforderlich. Der Adobe Analytics-Tracking-Server sollte mit „`.sc.omtrdc.net`“ enden oder ein CNAME sein.

   * **Media Analytics (Heartbeats)-Server:** Dieser Server hat immer das Format „`[namespace].hb.omtrdc.net`“, wobei `[namespace]` Ihren Unternehmensnamen angibt. Dieser Name wird von Adobe bereitgestellt.

   Sie müssen bestimmte Schlüsselvariablen validieren, die für alle Tracking-Aufrufe universell sind:

   **Adobe-Besucher-ID (`mid`):** Die `mid`-Variable wird verwendet, um den im AMCV-Cookie eingestellten Wert zu erfassen. Die `mid`-Variable ist der primäre Identifikationswert für sowohl Websites als auch mobile Apps und zeigt außerdem an, dass der Experience Cloud-Besucher-ID-Dienst ordnungsgemäß eingerichtet ist. Sie finden sie sowohl in Adobe Analytics (AppMeasurement)- als auch in Media Analytics (Heartbeats)-Aufrufen.

   * **Adobe Analytics Start-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Website-Seiten-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Lebenszyklus-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Start-Aufruf für Media Analytics**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Bei Start-Aufrufen für Media Analytics (`s:event:type=start`) sind die `mid`-Werte möglicherweise nicht vorhanden. Das ist in Ordnung. Sie werden möglicherweise erst mit dem Abspielaufruf für Media Analytics Play (`s:event:type=play`) angezeigt.

   * **Abspielaufruf für Media Analytics**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Medienplayer starten**

   Beim Starten des Medienplayers sendet das Media SDK die Schlüsselaufrufe in der folgenden Reihenfolge an die beiden Server:

   1. Adobe Analytics-Server – Start-Aufruf
   1. Media Analytics-Server – Start-Aufruf
   1. Media Analytics-Server – „Start-Aufruf für Adobe Analytics angefordert“

   Die ersten beiden Aufrufe oben enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Der dritte Aufruf oben teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, den Start-Aufruf für Adobe Analytics (`pev2=ms_s`) an den Adobe Analytics-Server zu senden.

1. **Werbeunterbrechung anzeigen (sofern verfügbar)**

   * **Ad Start**

   Wenn die Werbeanzeige startet, werden die folgenden Schlüsselaufrufe in folgender Reihenfolge gesendet:

   1. Adobe Analytics-Server – Anzeigenstart-Aufruf
   1. Media Analytics-Server – Anzeigenstart-Aufruf
   1. Media Analytics-Server – „Anzeigenstart-Aufruf für Adobe Analytics angefordert“

   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf](/help/legacy/validation/test-call-details.md#view-ad-playback).

   Der dritte Aufruf teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, den Start-Aufruf für Adobe Analytics (`pev2=msa_s`) an den Adobe Analytics-Server zu senden.

   * **Ad Play**

      Während der Anzeigenwiedergabe sendet das Media Analytics-SDK jede Sekunde Wiedergabeereignisse des Typs „ad“ (Anzeige) an den Media Analytics-Server.

   * **Ad Complete**

      Wenn eine Anzeige vollständig abgespielt wurde, sollte ein Abgeschlossen-Aufruf für Media Analytics gesendet werden.



1. **Werbewiedergabe mindestens 30 Sekunden lang anhalten, sofern verfügbar.** **Ad Pause**

   Während der Werbeunterbrechung sendet das SDK jede Sekunde einen Heartbeat oder „Ping“-Aufruf für Media Analytics an den Media Analytics-Server.

   >[!NOTE]
   >
   >Der Abspielleistenwert sollte während der Unterbrechung gleich bleiben.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Hauptinhalt für 10 Sekunden unterbrechungsfrei wiedergeben.** **Content Play**

   Während der Wiedergabe des Hauptinhalts sendet das Media SDK alle 10 Sekunden Heartbeats (Abspielaufrufe) an den Media Analytics-Server.

   Hinweise:

   * Die Position der Abspielleiste sollte bei jedem Abspielanruf um 10 erhöht werden.
   * Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

      Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Wiedergabe mindestens 30 Sekunden lang anhalten.** Beim Anhalten des Medienplayers sendet das SDK alle 10 Sekunden Pause-Ereignisaufrufe an den Media Analytics-Server. Wird das Video fortgesetzt, sollten erneut Wiedergabeereignisse gesendet werden.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf](/help/legacy/validation/test-call-details.md#pause-main-content).

1. **Medien suchen/scrubben.** Beim Scrubbing der Medienabspielleiste werden keine speziellen Tracking-Aufrufe gesendet. Wenn die Wiedergabe jedoch nach dem Scrubbing fortgesetzt wird, sollte der Abspielleistenwert jedoch die neue Position innerhalb des Hauptinhalts widerspiegeln.

1. **Medien wiedergeben (nur VOD).** Wenn Medien wiedergegeben werden, sollte eine neue Reihe von Medienstart-Aufrufen gesendet werden (als wäre dies ein Neustart).

1. **Nächstes Medium in der Wiedergabeliste anzeigen.** Wird das nächste Medium in der Wiedergabeliste gestartet, sollte eine neue Reihe von Medienstart-Aufrufen gesendet werden.

1. **Zwischen Medien oder Streams wechseln.** Beim Wechseln von Live-Streams sollte für den ersten Stream kein Abgeschlossen-Aufruf für Media Analytics gesendet werden. Die Medienstart- und Abspielaufrufe sollten mit dem neuen Sendungs- und Stream-Namen sowie mit den richtigen Werten für Abspielleiste und Dauer für die neue Sendung beginnen.

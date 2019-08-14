---
seo-title: Test 1 Standard-Wiedergabe
title: Test 1 Standard-Wiedergabe
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 1: Standardwiedergabe{#test-standard-playback}

In diesem Testfall wird die allgemeine Wiedergabe und Sequenzierung überprüft. Sie ist im Rahmen des Zertifizierungsanforderungsformulars erforderlich.

**Laden Sie das Zertifikatanforderungsformular hier herunter: = = &gt;**  [Zertifizierungsanforderungsformular.](cert_req_form.docx)

Medienimplementierungen bestehen aus folgenden Arten von Tracking-Aufrufen:
* Medien- und Anzeigenstartanrufe werden direkt an den appmeasurement-Server (Adobe Analytics) gesendet.
* Media Analytics Heartbeat-Aufrufe werden am Start und alle zehn Sekunden (für Inhalte) oder einer Sekunde (für Anzeigen) dem Medienanalytics-Tracking-Server gesendet.

>[!NOTE]
>Die Medienverfolgung verhält sich auf allen Plattformen gleich.

Sie müssen diese Aktionen in der folgenden Reihenfolge ausführen und aufzeichnen:

1. **Seite oder App laden**

   **Tracking-Server** (für alle Websites und mobilen Apps):

   * **Appmeasurement (Adobe Analytics) -** Ein RDC-Tracking-Server oder CNAME, der zu einem RDC-Tracking-Server aufgelöst wird, ist für den Experience Cloud Besucher-ID-Dienst erforderlich. The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats):** Dieser Server hat immer das Format "`[namespace].hb.omtrdc.net`, wo `[namespace]` Ihr Firmenname angegeben ist. Dieser Name wird von Adobe bereitgestellt.
   Sie müssen bestimmte wichtige Variablen überprüfen, die über alle Verfolgungsaufrufe hinweg universell sind:

   **Adobe Besucher-ID (`mid`):** Die `mid` Variable wird verwendet, um den Wert zu erfassen, der im AMCV-Cookie festgelegt ist. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Sie findet sie sowohl in appmeasurement- als auch in Media Analytics-Aufrufen.

   * **Media Analytics Play-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics-Startaufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Webseitenaufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Lebenszyklus-Aufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Heartbeat-Startaufruf**

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `s:event:type` | start |

   * **VA-Startaufruf**

      >[!NOTE]
      >
      >Bei VA Start-Aufrufen (`s:event:type=start`) sind die `mid` Werte möglicherweise nicht vorhanden. Das ist in Ordnung. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ms_s |


1. **Starten des Medienplayers**

   Wenn der Medienplayer beginnt, werden die wichtigsten Aufrufe in der folgenden Reihenfolge gesendet:

   1. Media Analytics-Start
   1. Heartbeat-Start
   1. Heartbeat-Analyse-Start
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **Werbeunterbrechung anzeigen (sofern verfügbar)**

   * **Ad Start**
   Wenn die Medienanzeige beginnt, werden die folgenden wichtigen Aufrufe in der folgenden Reihenfolge gesendet:

   1. Start der Medienanzeige
   1. Heartbeat-Anzeigenstart
   1. Start der Heartbeat-Anzeigenanalyse
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Ad Play**

      Während der Wiedergabe des Werbeinhalts werden Heartbeat-Aufrufe im Sekundentakt an den Heartbeat-Server gesendet.

   * **Ad Complete**

      Bei einem 100%-Punkt auf einer Medienanzeige wird ein Heartbeat Complete-Aufruf gesendet.



1. **Werbewiedergabe mindestens 30 Sekunden lang anhalten, sofern verfügbar.**  **Ad Pause**

   Während der Werbeinhalt angehalten wird, werden Heartbeat-Aufrufe im Sekundentakt an den Heartbeat-Server gesendet.

   >[!NOTE]
   >
   >Der Wert der Abspielleiste sollte während der Pause konstant bleiben.

1. **Spielen Sie das Hauptinhaltsmedium für 10 Minuten ununterbrochen ab.**  **Content Play**

   Während der Wiedergabe des Hauptinhalts werden alle zehn Sekunden Heartbeat-Aufrufe an den Media Analytics-Server gesendet.

   Hinweise:

   * Die Position der Abspielleiste sollte bei jedem Abspielanruf um 10 erhöht werden.
   * Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

      Aufrufparameter und Metadaten finden Sie unter [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Wiedergabe mindestens 30 Sekunden lang anhalten.** Bei Pause des Medienplayers werden alle 10 Sekunden Ereignisaufrufe gesendet. Wird das Video fortgesetzt, sollten erneut Wiedergabeereignisse gesendet werden.

1. **Suchen/Scrubben von Medien.** Beim Scrubbing von Medien-Playhead werden keine speziellen Verfolgungsaufrufe gesendet, wenn die Medienwiedergabe nach dem Scrubbing des Abspielkopfwerts die neue Position im Hauptinhalt wiedergeben sollte.

1. **Medien wiedergeben (nur VOD)** Wenn Medien wiederholt werden, sollte ein neuer Satz an Medienstart-Aufrufen gesendet werden, als ob dies eine neue Medienansicht ist.

1. **Zeigen Sie die nächsten Medien in der Wiedergabeliste an.** Beim Medienstart der nächsten Medien in einer Wiedergabeliste sollte ein neuer Satz an Medienstart-Aufrufen gesendet werden.

1. **Medien oder Stream wechseln** Beim Wechseln von Live-Streams sollte kein Heartbeat-Abschlussaufruf für den ersten Stream gesendet werden. Die Medienstart-Aufrufe und Medienplay-Aufrufe sollten mit der neuen Anzeige und dem Stream-Namen beginnen und mit den korrekten Werten für Abspielkopf und Dauer für die neue Anzeige beginnen.


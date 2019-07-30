---
seo-title: Test 1 Standard-Wiedergabe
title: Test 1 Standard-Wiedergabe
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Test 1: Standardwiedergabe{#test-standard-playback}

Dieser Testfall überprüft allgemeine Wiedergabe und Sequenzierung und ist im Rahmen des Zertifizierungsanforderungsformulars erforderlich. Das Anfrageformular für die Zertifizierung können Sie hier herunterladen:[ Zertifizierungsanfrageformular.](cert_req_form_nielsen.docx)

Videoimplementierungen bestehen aus folgenden Arten von Tracking-Aufrufen:
* Video Start- und Ad Start-Aufrufe werden direkt an den AppMeasurement-Server gesendet.
* Heartbeat-Aufrufe von Media Analytics (MA) werden am Anfang und alle zehn Sekunden an den Adobe VA-Tracking-Server gesendet.

>[!NOTE]
>Das Video-Tracking verhält sich auf allen Plattformen – Desktop oder Mobilgeräte – gleich.

Sie müssen die Aktionen in folgender Reihenfolge abschließen und aufzeichnen:

1. **Seite oder App laden**

   **Tracking-Server** (für alle Websites und mobilen Apps):

   * **AppMeasurement (Adobe Analytics):** Ein RDC-Tracking-Server bzw. ein CNAME, der aufgelöst auf einen RDC-Server verweist, ist für den Experience Cloud-Besucher-ID-Dienst erforderlich. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics (Heartbeats):** Dieser Server hat immer das Format `[namespace].hb.omtrdc.net`, in `[namespace]` dem sich Ihr Anmeldeunternehmen befindet und von Adobe bereitgestellt wird.
   Sie müssen bestimmte wichtige, universelle Variablen über alle Tracking-Aufrufe hinweg validieren:

   **Adobe Besucher-ID (`mid`):** Die `mid` Variable wird verwendet, um den Wert zu erfassen, der im AMCV-Cookie festgelegt ist. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Sie befindet sich sowohl in appmeasurement- als auch in Media Analytics (MA)-Aufrufen.

   * **Heartbeat Play-Aufruf**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. Das ist in Ordnung. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parameter | Wert (Beispiel) |
      |---|---|
      | `pev2` | ms_s |


1. **Videoplayer starten**

   Wenn der Videoplayer gestartet wird, werden die Aufrufe in folgender Reihenfolge gesendet:

   1. Video Analytics-Start
   1. Heartbeat-Start
   1. Heartbeat-Analyse-Start
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **Werbeunterbrechung anzeigen (sofern verfügbar)**

   * **Ad Start**
   Wenn die Werbeanzeige startet, werden die grundlegenden Aufrufe in folgender Reihenfolge gesendet:

   1. Start der Anzeigenanalyse
   1. Heartbeat-Anzeigenstart
   1. Start der Heartbeat-Anzeigenanalyse
   Die ersten beiden Aufrufe enthalten zusätzliche Metadaten und Variablen. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Ad Play**

      Während der Wiedergabe des Werbeinhalts werden Heartbeat-Aufrufe im Sekundentakt an den Heartbeat-Server gesendet.

   * **Ad Complete**

      Wenn die Videoanzeige vollständig abgespielt wurde, wird ein entsprechender Heartbeat-Aufruf gesendet.



1. **Werbewiedergabe mindestens 30 Sekunden lang anhalten, sofern verfügbar.**  **Ad Pause**

   Während der Werbeinhalt angehalten wird, werden Heartbeat-Aufrufe im Sekundentakt an den Heartbeat-Server gesendet.

   >[!NOTE]
   >
   >Der Wert der Abspielleiste sollte während der Pause konstant bleiben.

1. **Inhalt mindestens 10 Minuten lang unterbrechungsfrei wiedergeben.** **Content Play **

   Während der normalen Wiedergabe des Hauptinhalts werden alle zehn Sekunden Heartbeat-Aufrufe an den Heartbeat-Server gesendet.

   Hinweise:

   * Die Position der Abspielleiste sollte bei jedem Abspielanruf um 10 erhöht werden.
   * Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Wiedergabe mindestens 30 Sekunden lang anhalten.** Wird das Video angehalten, werden alle zehn Sekunden entsprechende Aufrufe gesendet. Wird das Video fortgesetzt, sollten erneut Wiedergabeereignisse gesendet werden.

1. **Zu verschiedenen Positionen im Video springen.** Beim Verschieben der Abspielleiste des Videos werden keine speziellen Tracking-Aufrufe gesendet. Wenn die Wiedergabe jedoch nach dem Verschieben fortgesetzt wird, sollte der Positionswert jedoch die neue Position innerhalb des Hauptinhalts widerspiegeln.

1. **Video erneut abspielen (nur VOD).** Wenn ein Video erneut wiedergegeben wird, sollte eine neue Gruppe von Videostartaufrufen gesendet werden, da es sich um eine neue Wiedergabe handelt.

1. **Nächstes Video in der Wiedergabeliste ansehen.** Wird das nächste Video in der Wiedergabeliste gestartet, sollte eine neue Gruppe von Videostartaufrufen gesendet werden.

1. **Video oder Stream wechseln.** Beim Wechseln von Live-Streams sollte kein Heartbeat-Abschlussaufruf für den ersten Stream gesendet werden. Die Videostart- und -wiedergabeaufrufe sollten mit dem neuen Sendungs- und Stream-Namen sowie mit den richtigen Positions- und Dauerwerten für die neue Sendung beginnen.


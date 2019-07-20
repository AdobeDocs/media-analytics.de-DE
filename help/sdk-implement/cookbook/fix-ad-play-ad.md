---
seo-title: Beheben der Hauptinhaltswiedergabe zwischen Anzeigen
title: Beheben der Hauptinhaltswiedergabe zwischen Anzeigen
uuid: 228 b 4812-c 23 e -40 c 8-ae 2 b-e 15 ca 69 b 0 bc 2
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Beheben von „main:play“ zwischen Anzeigen{#resolving-main-play-appearing-between-ads}

## PROBLEM

In einigen Tracking-Szenarios treten möglicherweise zwischen dem Ende der einen und dem Anfang der nächsten Anzeige unerwartete `main:play`-Aufrufe auf. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. Wenn diese `main:play`-Aufrufe während einer Pre-Roll-Werbeunterbrechung auftreten, wird die Metrik zum Inhaltsstart möglicherweise zu früh festgelegt.

Eine Lücke zwischen Anzeigen wie die oben beschriebene wird vom Medien-SDK als Hauptinhalt interpretiert, da keine Überlappung mit Anzeigeninhalten besteht. Dem Medien-SDK liegen keine Anzeigeninformationen vor und der Player befindet sich im Wiedergabestatus. Wenn keine Anzeigeninformationen vorliegen und der Player im Wiedergabestatus ist, rechnet das Medien-SDK die Dauer der Lücke standardmäßig dem Hauptinhalt zu. Es kann die Wiedergabedauer nicht den fehlenden Anzeigeninformationen zuordnen.

## ERKENNUNG

Wenn Sie Adobe Debug oder einen Netzwerkpaket-Sniffer wie Charles verwenden, wenn in einer Pre-Roll-Werbeunterbrechung die folgenden Heartbeat-Aufrufe angezeigt werden:

* Sitzungsstart: `s:event:type=start` &amp; `s:asset:type=main`
* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(unexpected)**

* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(expected)**

## LÖSUNG

***Verzögern Sie den Ad Complete-Aufruf.***

Beseitigen Sie die Lücke innerhalb des Players, indem Sie `trackEvent:AdComplete` für die erste Anzeige später aufrufen, sodass `trackEvent:AdStart` für die zweite Anzeige umgehend folgt. Die Anwendung sollte das `AdComplete`-Ereignis nicht gleich zum Ende der ersten Anzeige aufrufen. Stellen Sie sicher, dass Sie bei der letzten Anzeige der Werbeunterbrechung `trackEvent:AdComplete` aufrufen. Wenn der Player erkennen kann, dass das aktuelle Anzeigen-Asset das letzte der Werbeunterbrechung ist, rufen Sie umgehend `trackEvent:AdComplete` auf. Durch diese Lösung wird der ersten Anzeigeneinheit eine zusätzliche Sekunde an Besuchszeit angerechnet.

**Beim Start der Werbeunterbrechung, einschließlich Pre-Roll:**

* Erstellen Sie die `adBreak`-Objektinstanz für die Werbeunterbrechung, z. B. `adBreakObject`.

* Aufruf `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Bei jedem Start eines Anzeigen-Assets:**

* **Aufruf`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Rufen Sie dies nur auf, wenn die vorherige Anzeige nicht abgeschlossen war. Erwägen Sie hierzu einen booleschen Wert, um einen `isinAd`-Status für die vorherige Anzeige festzulegen.

* Erstellen Sie die Anzeigen-Objektinstanz für das Anzeigen-Asset, z. B. `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Aufruf `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**Bei jedem Abschluss eines Anzeigen-Assets:**

* **Kein Aufruf tätigen**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**Beim Überspringen einer Anzeige:**

* Aufruf `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Beim Abschluss einer Werbeunterbrechung:**

* **Aufruf`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* Aufruf `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.


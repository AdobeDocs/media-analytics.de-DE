---
title: Beheben von Hauptabspielen zwischen Anzeigen
description: '"Erfahren Sie, wie Sie unerwartete main:play -Aufrufe zwischen Anzeigen verarbeiten."'
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 96%

---

# Beheben von „main:play“ zwischen Anzeigen {#resolving-main-play-appearing-between-ads}

## PROBLEM

In einigen Tracking-Szenarios treten möglicherweise zwischen dem Ende der einen und dem Anfang der nächsten Anzeige unerwartete `main:play`-Aufrufe auf. Wenn die Verzögerung zwischen dem Aufruf zum Abschluss der ersten Anzeige und dem Start der nächsten mehr als 250 Millisekunden beträgt, sendet das Medien-SDK `main:play`-Aufrufe. Wenn diese `main:play`-Aufrufe während einer Pre-Roll-Werbeunterbrechung auftreten, wird die Metrik zum Inhaltsstart möglicherweise zu früh festgelegt.

Eine Lücke zwischen Anzeigen wie die oben beschriebene wird vom Medien-SDK als Hauptinhalt interpretiert, da keine Überlappung mit Anzeigeninhalten besteht. Dem Medien-SDK liegen keine Anzeigeninformationen vor und der Player befindet sich im Wiedergabestatus. Wenn keine Anzeigeninformationen vorliegen und der Player im Wiedergabestatus ist, rechnet das Medien-SDK die Dauer der Lücke standardmäßig dem Hauptinhalt zu. Es kann die Wiedergabedauer nicht den fehlenden Anzeigeninformationen zuordnen.

## ERKENNUNG

Wenn Sie Adobe Debug oder einen Netzwerk-Packet-Sniffer wie Charles verwenden und während einer Pre-Roll-Werbeunterbrechung folgende Heartbeat-Aufrufe in dieser Reihenfolge angezeigt werden:

* Sitzungsstart: `s:event:type=start` &amp; `s:asset:type=main`
* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(unerwartet)**

* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Abschluss der Anzeige: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(erwartet)**

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
   >Führen Sie diesen Aufruf nur durch, wenn die vorherige Anzeige nicht abgeschlossen wurde. Erwägen Sie hierzu einen booleschen Wert, um einen `isinAd`-Status für die vorherige Anzeige festzulegen.

* Erstellen Sie die Anzeigen-Objektinstanz für das Anzeigen-Asset, z. B. `adObject`.
* Fügen Sie die Anzeigenmetadaten hinzu: `adCustomMetadata`.
* Aufruf `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Rufen Sie `trackPlay()` auf, wenn es sich um die erste Anzeige in einer Pre-Roll-Werbeunterbrechung handelt.

**Bei jedem Abschluss eines Anzeigen-Assets:**

* **Führen Sie keinen Aufruf durch**

   >[!NOTE]
   >
   >Wenn die Anwendung weiß, dass es sich um die letzte Anzeige in der Werbeunterbrechung handelt, rufen Sie `trackEvent:AdComplete` hier auf und überspringen Sie `trackEvent:AdComplete` in `trackEvent:AdBreakComplete`.

**Beim Überspringen einer Anzeige:**

* Aufruf `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Beim Abschluss einer Werbeunterbrechung:**

* **Aufruf`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Wenn dieser Schritt bereits weiter oben im Rahmen des letzten `trackEvent:AdComplete`-Aufrufs durchgeführt wurde, können Sie ihn hier überspringen.

* Aufruf `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

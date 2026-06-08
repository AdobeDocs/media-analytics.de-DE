---
title: Anzeigen verfolgen
description: Überblickt über die Implementierung des Anzeigen-Trackings mit dem Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# Anzeigen verfolgen

Das Tracking der Anzeigenwiedergabe deckt Anzeigenunterbrechungen, Anzeigenstarts, Anzeigenabschlüsse und Anzeigensprünge ab. Verwenden Sie die API des Media Players , um wichtige Player-Ereignisse zu identifizieren und die erforderlichen Anzeigenvariablen zu füllen.

## Player-Ereignisse

| Player-Ereignis | Aktion |
| --- | --- |
| Start der Werbeunterbrechung | Erstellen eines Werbeunterbrechungsobjekts; Aufruf von AdBreakStart |
| Anzeigenstart | Werbeobjekt erstellen; AdStart aufrufen |
| Hinzufügen abgeschlossen | Anzeige abschließen |
| Überspringen einer Anzeige | Call AdSkip |
| Werbeunterbrechung abgeschlossen | AdBreakComplete aufrufen |

## Implementierungsschritte

1. Ermitteln Sie, wann die Begrenzung der Anzeigenunterbrechung beginnt, einschließlich der Vorab-Rolle, und erstellen Sie ein Objekt für die Anzeigenunterbrechung. Siehe [Name der Werbeunterbrechung](/help/implementation/variables/ads/ad-break-name.md) und [Startzeit der Werbeunterbrechung](/help/implementation/variables/ads/ad-break-start-time.md) für Felddefinitionen.
1. Rufen Sie [Start der Werbeunterbrechung](/help/implementation/events/ads/ad-break-start.md) auf, um mit der Verfolgung der Werbeunterbrechung zu beginnen.
1. Ermitteln Sie, wann die Anzeige gestartet wird, und erstellen Sie ein Anzeigenobjekt. Felddefinitionen finden Sie unter [Anzeigename](/help/implementation/variables/ads/ad-name.md), [Anzeigen](/help/implementation/variables/ads/ad-id.md), [Anzeigenlänge](/help/implementation/variables/ads/ad-length.md), [Anzeige in Pod-Position](/help/implementation/variables/ads/ad-in-pod-position.md) und [Anzeigenplayer](/help/implementation/variables/ads/ad-player-name.md).
1. Fügen Sie optional Standard-Anzeigenmetadaten hinzu. Unter [Advertiser](/help/implementation/variables/ads/advertiser.md), [Kampagnen-ID](/help/implementation/variables/ads/campaign-id.md), [Creative ID](/help/implementation/variables/ads/creative-id.md), [Creative URL](/help/implementation/variables/ads/creative-url.md), [Platzierungs-ID](/help/implementation/variables/ads/placement-id.md) und [Site-ID](/help/implementation/variables/ads/site-id.md) finden Sie verfügbare Schlüssel.
1. Rufen Sie [Anzeigenstart](/help/implementation/events/ads/ad-start.md) auf, um mit dem Tracking der Anzeige zu beginnen.
1. Wenn die Anzeige bis zum Abschluss wiedergegeben wird, rufen Sie [Anzeige abgeschlossen](/help/implementation/events/ads/ad-complete.md) auf.
1. Wenn der Viewer die Anzeige übersprungen hat, rufen Sie [Anzeigenüberspringen](/help/implementation/events/ads/ad-skip.md) anstelle von „Anzeige abgeschlossen“ auf.
1. Für weitere Anzeigen in derselben Werbeunterbrechung wiederholen Sie die Schritte 3 bis 7.
1. Wenn die Werbeunterbrechung abgeschlossen ist, rufen Sie [Werbeunterbrechung abgeschlossen](/help/implementation/events/ads/ad-break-complete.md) auf.

>[!IMPORTANT]
>
>**Pre-Roll-Anzeigen: Rufen Sie `trackPlay` nicht vor dem `AdBreakStart` und `AdStart` auf.** Das erste `play`-Ping für Hauptinhaltsinkremente [Inhaltsstarts](/help/reporting/metrics/content-starts.md). Wenn `trackPlay` aufgerufen wird, bevor die Pre-Roll-Anzeigenereignisse ausgelöst werden, und der Viewer während der Anzeige ausfällt, wird der Inhalt gestartet erhöht, obwohl nie Hauptinhalt wiedergegeben wurde. Verzögern Sie bei Pre-Roll-Szenarien `trackPlay`, bis `AdBreakStart` und `AdStart` gesendet wurden.

>[!NOTE]
>
>Der während der Anzeigenwiedergabe angezeigte Abspielkopfwert stellt die Position des Viewers innerhalb des **Hauptinhalts** und nicht innerhalb der Anzeige dar. Bei einer Pre-Roll-Anzeige, die einem 10-minütigen Video vorausgeht, wird der Abspielkopf während der gesamten Anzeige `0`. Bei einer Mid-Roll-Anzeige, die mit der 5-Minuten-Markierung beginnt, bleibt der Abspielkopf für die Dauer der Anzeige bei `300` (Sekunden).

## Häufige Probleme

### Unerwartete Haupt:playAufrufe zwischen Anzeigen

Wenn `main:play` Aufrufe zwischen aufeinander folgenden Anzeigen auftreten, besteht eine Lücke von mehr als 250 Millisekunden zwischen dem AdComplete-Aufruf und dem nächsten AdStart-Aufruf. Wenn diese Lücke auftritt, sendet Media SDK Haupt-Inhalts-Pings, wodurch die Inhaltsstartmetrik für Pre-Roll-Szenarien vorzeitig festgelegt werden kann.

**Ursache:** Für Media SDK sind keine Anzeigeninformationen festgelegt und der Player befindet sich in einem Wiedergabestatus, sodass die Lückendauer dem Hauptinhalt zugeschrieben wird.

**Lösung:** den AdComplete-Aufruf für jede Anzeige (mit Ausnahme der letzten) verzögern, anstatt ihn sofort nach dem Ende der Anzeige aufzurufen. Batch-Aufrufe werden wie folgt durchgeführt:

* Bei jedem **Anzeigenstart**: Wenn eine frühere Anzeige existiert und noch nicht als abgeschlossen markiert wurde, rufen Sie AdComplete *vor)* AdStart für die neue Anzeige auf.
* Bei jedem **Ende eines Anzeigen-Assets**: AdComplete nicht sofort aufrufen, sondern verzögern.
* Bei **Abschluss der Werbeunterbrechung**: Rufen Sie „AdComplete“ für die letzte Anzeige auf (falls noch nicht aufgerufen) und rufen Sie dann „AdBreakComplete“ auf.

Dieses Muster stellt sicher, dass AdComplete und der nächste AdStart aufeinander folgen, sodass keine Lücken entstehen.

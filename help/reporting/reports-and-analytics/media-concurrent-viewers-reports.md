---
title: Gleichzeitige Medienbetrachter
description: Erfahren Sie mehr über das Dashboard „Gleichzeitige Medienbetrachter“, mit dem gleichzeitige Betrachter an einem Tag angezeigt werden. Die Daten können nach Inhalt, Gerätetyp oder Land gefiltert werden.
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# Berichte zu gleichzeitigen Medienbetrachtern {#media-concurrent-viewers}

Im Dashboard „Gleichzeitige Medienbetrachter“ werden gleichzeitige Viewer an einem Tag angezeigt. Die Daten können nach Inhalt, Gerätetyp und Land gefiltert werden.

>[!TIP]
>
> Grundlage für diesen Bericht bilden gleichzeitig aktive Mediensitzungen.  Wenn Sie gleichzeitige Betrachtungen für einen Unique Visitor anzeigen und dabei weitere Funktionen, Aufschlüsselung mit Vergleich, auf ein Segment anwenden möchten, nutzen Sie dafür das [Bedienfeld für gleichzeitige Medienbetrachter in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=de).
>

![](assets/video-concurrent-viewers.png)

## Berichtsfunktionen {#report-features}

Hier sind einige Funktionen des Berichts:

* Die Daten werden nicht in Echtzeit angezeigt. Der Bericht weist eine normale Adobe Analytics-Latenz auf.
* Der Bericht deckt einen Zeitraum von 24 Stunden ab. Die X-Achse ist die Tageszeit, die auf der Zeitzone der Report Suite basiert.
* Dadurch werden gleichzeitige Betrachter mit extrem hoher Granularität angezeigt.
* Es gibt einen *Bericht über gleichzeitige Medienbetrachter*, der zeigt, wie viele Betrachter den gesamten Inhalt ansehen oder ihm zuhören.
* Es gibt einen Bericht über gleichzeitige Medienbetrachter innerhalb des *Berichts über Mediendetails*, der angibt, wie viele Betrachter ein bestimmtes Medienelement ansehen oder ihm zuhören.
* Der Bericht betrachtet jeweils nur einen einzigen Tag.
* Der Kunde kann sich Verlaufsberichte zu gleichzeitigen Zuschauern anzeigen (beschränkt auf einzelne Tage).

## Einschränkungen {#limitations}

Für diesen Bericht gelten folgende Einschränkungen:

* Es werden keine Daten angezeigt, wenn das ausgewählte Intervall keinen gesamten Tag darstellt.
* Sie können die Daten nicht exportieren, z. B. ReportBuilder.
* Sie können die Daten nicht in einem Tabellenformat darstellen.
* Sie können keinen Bericht per E-Mail senden.
* Auch wenn Sie keine Anzeigen verfolgen, müssen Sie die Medienverfolgung erneut aktivieren und das Medienanzeigemodul auswählen.
* Diese Funktion bietet genaue Daten, wenn eine Heartbeats-Bibliothek verwendet wird, in die eine Funktion für Pausenverfolgung integriert ist.

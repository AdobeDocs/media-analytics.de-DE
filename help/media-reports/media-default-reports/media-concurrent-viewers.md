---
title: Gleichzeitige Medienbetrachter
description: „Erfahren Sie mehr über das Dashboard 'Gleichzeitige Medienbetrachter', mit dem gleichzeitige Betrachter an einem Tag angezeigt werden. Die Daten können nach Inhalt, Gerätetyp und Land gefiltert werden.“
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Media Analytics, Reports & Analytics Basics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 100%

---

# Gleichzeitige Medienbetrachter{#media-concurrent-viewers}

Im Dashboard „Gleichzeitige Medienbetrachter“ werden gleichzeitige Viewer an einem Tag angezeigt. Die Daten können nach Inhalt, Gerätetyp und Land gefiltert werden.

>[!TIP]
>
> Grundlage für diesen Bericht bilden gleichzeitig aktive Mediensitzungen.  Wenn Sie gleichzeitige Betrachtungen für einen Unique Visitor anzeigen und dabei weitere Funktionen, Aufschlüsselung mit Vergleich, auf ein Segment anwenden möchten, nutzen Sie dafür das [Bedienfeld für gleichzeitige Medienbetrachter in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=de).

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

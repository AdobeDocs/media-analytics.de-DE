---
title: Kapitel und Segmente verfolgen
description: Implementieren des Kapitel- und Segment-Trackings mit dem Media SDK.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# Kapitel und Segmente verfolgen

Das Tracking von Kapiteln und Segmenten ist für benutzerdefinierte Medienkapitel oder -segmente verfügbar. Zu den Anwendungsfällen für Kapitel-Tracking zählt die Definition von Kundensegmenten basierend auf Medieninhalten, z. B. Baseball-Innings, oder die Definition von Inhaltssegmenten zwischen Werbeunterbrechungen. Das Kapitel-Tracking ist **nicht** für die Implementierung des Core-Medien-Trackings erforderlich.

Das Kapitel-Tracking beinhaltet Kapitelstarts, -beendigungen und übersprungene Kapitel. Verwenden Sie die Media Player-API mit benutzerdefinierter Segmentierungslogik, um Kapitelereignisse zu identifizieren und die Kapitelvariablen zu füllen.

## Player-Ereignisse

| Player-Ereignis | Aktion |
| --- | --- |
| Kapitelstart | Kapitelobjekt erstellen; ChapterStart aufrufen |
| Kapitel abgeschlossen | Kapitel abschließen |
| Kapitelübersprung | Kapitelsprung aufrufen |

## Implementierungsschritte

1. Ermitteln Sie, wann das Kapitelstartereignis auftritt, und erstellen Sie das Kapitelobjekt. Siehe [Kapitelname](/help/implementation/variables/chapters/chapter-name.md), [Kapitelposition](/help/implementation/variables/chapters/chapter-position.md), [Kapitellänge](/help/implementation/variables/chapters/chapter-length.md) und [Kapitelversatz](/help/implementation/variables/chapters/chapter-offset.md) für Felddefinitionen.
1. Erstellen Sie optional Kontextdatenvariablen für benutzerdefinierte Kapitelmetadaten.
1. Rufen Sie [Kapitelstart](/help/implementation/events/chapters/chapter-start.md) auf, um mit der Verfolgung des Kapitels zu beginnen.
1. Wenn die Wiedergabe die Kapitelendgrenze erreicht, rufen Sie &quot;[ abgeschlossen“ ](/help/implementation/events/chapters/chapter-complete.md).
1. Wenn der Benutzer das Kapitel vor Abschluss überspringt, rufen Sie [Kapitelüberspringen](/help/implementation/events/chapters/chapter-skip.md) auf.
1. Für weitere Kapitel wiederholen Sie die Schritte 1 bis 5.

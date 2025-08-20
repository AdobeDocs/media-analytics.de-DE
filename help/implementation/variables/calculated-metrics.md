---
title: Berechnete Metriken
description: Erfahren Sie mehr über berechnete Metriken und Metrikformeln in Streaming-Mediendiensten.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 72%

---

# Berechnete Metriken{#calculated-metrics}

Berechnete Metriken für Adobe Streaming Media Services sind benutzerdefinierte Metriken, mit denen Sie zielgerichtete Streaming-Mediendaten abrufen können, z. B. durchschnittliche Anzeigenbesuchszeit oder durchschnittliche Anzeigen pro Medien-Stream.

Weitere Informationen zu berechneten Adobe Analytics-Metriken finden Sie unter [Berechnete und erweiterte berechnete (abgeleitete) Metriken](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=de) im Adobe Analytics-Komponenten-Handbuch.

>[!NOTE]
>
>Diese berechneten Metriken wurden am 13.9.18 eingeführt.

| Metrik | Beschreibung | Formel |
|---|---|---|
| Durchschnittliche Anzeigen pro Medienstream | Anzeigenstarts pro Medienstart | `Ad Starts / Media Starts` |
| Durchschnittliche Kapitel pro Medienstream | Kapitelstarts pro Medienstart | `Chapter Start / Media Starts` |
| Durchschnittl. Besuchszeit für Medien | Gesamtzeit pro Medienstart (`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| Durchschnittl. Inhaltsbesuchszeit | Besuchszeit für den Inhalt nach gestarteten Inhalten (`HH:MM:SS`) | `Content Time Spent / Content Start` |
| Durchschnittl. Besuchszeit für Anzeige | Besuchszeit für die Anzeige pro gestarteter Anzeige (`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| Durchschnittl. Besuchszeit für Kapitel | Besuchszeit für das Kapitel pro gestartetem Kapitel (`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| Medienabschlussrate | Rate der Inhaltsbeendigung und Medienaufrufe im Vergleich (%) | `Content Completes/ Media Starts` |
| Inhaltsabschlussrate | Rate der Inhaltsbeendigungen und IInhaltsstarts im Vergleich (%) | `Content Completes / Content Starts` |
| Anzeigenabschlussrate | Anteil abgeschlossener Anzeigen und gestarteter Anzeigen im Vergleich (%) | `Ad Completes / Ad Starts` |
| Kapitelabschlussrate | Anteil abgeschlossener Kapitel und gestarteter Kapitel im Vergleich (%) | `Chapter Completes / Chapter Starts` |
| Drop-vor-Start-Rate | Drop-Rate vor Starts und Medienstarts im Vergleich (%) | `Drops before Starts / Media Starts` |
| Rate der Inhaltspausendauer | Rate der Pausengesamtdauer und Besuchszeit für die Inhalte (%) im Vergleich | `Total Pause Duration / Content Time Spent` |
| Rate der Inhaltspufferdauer | Rate der Länge der Inhaltspufferungen im Vergleich zur Inhaltsbesuchszeit (%) | `Total Buffer Duration / Content Time Spent` |
| Rate der Zeit für Inhalte bis zum Start | Rate der Zeit bis zum Start und der Inhaltsbesuchszeit im Vergleich (%) | `Time to Start / Content Time Spent` |
| Rate der Besuchszeit für Anzeigen | Rate der Besuchszeit für Anzeigen und der Besuchszeit für Inhalte im Vergleich (%) | `Ad Time Spent / Content Time Spent` |

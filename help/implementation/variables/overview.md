---
title: Übersicht über Streaming-Medienvariablen
description: Erfahren Sie, wie Streaming-Medienvariablen organisiert sind und wie sie in Adobe Analytics und Customer Journey Analytics zugeordnet sind.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# Übersicht über Streaming-Medienvariablen

Variablen sind die Daten, die Ihr Medien-Player zu einem Stream bereitstellt, z. B. Inhaltsname, Stream-Typ, Anzeigename und Wiedergabequalität. Die meisten Variablen werden beim Sitzungsstart festgelegt und vom Medien-Backend bis zum Sitzungsabschluss übertragen. Von dort werden sie zum Ausfüllen der Dimensionen und Metriken verwendet, die Sie für das Reporting verwenden. Jede Variablenseite dokumentiert, wie diese Variable für jede unterstützte Implementierungsmethode festgelegt wird.

## So werden Variablen an Adobe gesendet

Eine Variable trägt für jede Adobe-Anwendung oder jeden Service denselben Wert, aber das Format dieses Werts hängt davon ab, wohin Sie ihn senden. In der folgenden Tabelle sind alle Programme oder Services sowie das erwartete Variablenformat aufgeführt. Die Tabelle „Eigenschaften“ auf jeder Variablenseite zeigt den genauen Wert an, der in jedem Format verwendet werden soll.

| Datenformat | Beschreibung |
| --- | --- |
| Kontextdatenvariable | Das an Adobe Analytics gesendete Format, benannt mit einem `a.media` Präfix (z. B. `a.media.name`). |
| XDM-Sammlungsfeld | Das an Customer Journey Analytics gesendete Format, ausgedrückt als XDM-Feldpfad (z. B. `xdm.mediaCollection.sessionDetails.name`). |
| Audience Manager-Eigenschaft | Das an Audience Manager weitergeleitete Format mit dem Präfix `c_contextdata` (z. B. `c_contextdata.a.media.name`). |

>[!MORELIKETHIS]
>
>* [Ereignisübersicht](/help/implementation/events/overview.md): Die Player-Ereignisse, die Variablen enthalten
>* [Dimensions-Übersicht](/help/reporting/dimensions/overview.md): Die Berichtsdimensionen, mit denen Variablen gefüllt werden
>* [Metriken - Übersicht](/help/reporting/metrics/overview.md): Die Berichtsmetriken, mit denen Variablen gefüllt werden

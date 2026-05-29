---
title: Übersicht über Metriken für Streaming-Medien
description: Erfahren Sie, wie Streaming-Medienmetriken in Adobe Analytics und Customer Journey Analytics berechnet und organisiert werden.
feature: Metrics
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---


# Übersicht über Metriken für Streaming-Medien

Metriken in Streaming Media Analytics sind ereignisgesteuerte Zählungen und Dauern, die vom Medien-Backend berechnet werden. Der Medien-Player sendet Ereignisse wie Sitzungsstart, Wiedergabe, Ping und Anzeigenstart. Das Medien-Backend verarbeitet diese Ereignisse und schließt die Metrikwerte beim Sitzungsabschlussaufruf ab.

## So werden Metriken berechnet

Metriken für Streaming-Medien folgen vier Hauptberechnungsmustern:

* **Ereignisausgelöste Flags**: Legen Sie fest, wann das qualifizierende Ereignis zum ersten Mal in einer Sitzung eintrifft. Ein [`play`](/help/implementation/events/playback/play.md) Ereignis für den Hauptinhalt legt das Flag [[!UICONTROL Inhaltsstarts]](content-starts.md) fest. Ein [`adStart`](/help/implementation/events/ads/ad-start.md) Ereignis [[!UICONTROL Anzeigenstarts]](ad-starts.md). Das Flag wird einmal pro Sitzung beim Schließen-Aufruf gemeldet, nicht pro Ereignis.

* **Akkumulierte Dauer**: Addiert die Intervalle zwischen Ping-Ereignissen, während ein bestimmter Wiedergabestatus aktiv ist. [[!UICONTROL Besuchszeit für Inhalt]](content-time-spent.md) wird während der Wiedergabe des Hauptinhalts gesammelt; [[!UICONTROL Besuchszeit für Anzeige]](ad-time-spent.md) wird während der Wiedergabe einer Anzeige gesammelt. Das von Adobe empfohlene Ping-Intervall beträgt 10 Sekunden für den Hauptinhalt und 1 Sekunde für Anzeigen, sodass die Besuchszeitmetriken nur so detailliert sein können wie das Ping-Intervall Ihrer Implementierung.

* **Anzahl der Ereignisse**: Verfolgen Sie die Gesamtzahl der Vorfälle innerhalb der Sitzung. Qualitätsmetriken wie [[!UICONTROL Pufferereignisse]](buffer-events.md), [[!UICONTROL Bitratenänderungen]](bitrate-changes.md), [[!UICONTROL Fehlerereignisse]](error-events.md) und [[!UICONTROL Pause-Ereignisse]](pause-events.md) zählen jedes Vorkommnis, nicht nur das erste.

* **Betroffene Streams**: Kennzeichen auf Sitzungsebene auf „1“ gesetzt, wenn das entsprechende Ereignis zu einem beliebigen Zeitpunkt während der Sitzung aufgetreten ist, unabhängig davon, wie oft das Ereignis aufgetreten ist. Verwenden Sie diese Metriken, um die Reichweite zu messen, während Sie die Ereigniszählungsmetrik verwenden, um den Schweregrad zu messen. Beispielsweise können Sie mit &quot;[[!UICONTROL &#x200B; Streams“ den &#x200B;]](buffer-impacted-streams.md) der Sitzungen ermitteln, die von der Pufferung in allen Wiedergabesitzungen betroffen waren.

## Verfügbarkeit nach Berichtssystem

| Meldesystem | Wie Metriken ankommen |
| --- | --- |
| Adobe Analytics | Wird mit [Kontextdatenvariablen“ &#x200B;](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/page-vars/contextdata). Einige Metriken füllen Lösungsereignisse automatisch mit diesen Kontextdatenvariablen auf, während andere mithilfe von [Verarbeitungsregeln“ einem benutzerdefinierten Ereignis &#x200B;](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) werden müssen. Für Metriken, die Werte automatisch ausfüllen, muss zunächst die entsprechende Einstellung [Streaming Media Report Suite](../../implementation/media-sdk/setup/media-reports-enable.md) aktiviert werden. |
| Customer Journey Analytics | XDM-Felder in `xdm.mediaReporting.sessionDetails` und zugehörigen Knoten, die aus einem Datensatz bezogen werden, der Streaming-Mediendaten enthält. Sie müssen jede Metrik mit den gewünschten Einstellungen in [Einstellungen der Datenansichtskomponente](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/component-settings/overview) erstellen. |
| Daten-Feeds | Metriken werden in den Spalten `event_list` und `post_event_list` als Ereignis-IDs angezeigt. Jede Feed-Datei enthält eine `events.csv`-Datei, die die Suche nach allen Metriken enthält, einschließlich der Metriken für Streaming-Medien. |

>[!MORELIKETHIS]
>
>* [Dimensionsübersicht](../dimensions/overview.md): Referenz zu Streaming-Mediendimensionen
>* [Berechnete Metriken](/help/reporting/calculated-metrics.md): Verhältnisse und abgeleitete Metriken, die aus den oben genannten Basismetriken erstellt wurden
>* [Parameterzuordnung](/help/implementation/parameters-mapping.md): Vollständiger Verweis von Ereignis zu Spalte zu XDM
>* [Ereignisübersicht](/help/implementation/events/overview.md): Die Player-Ereignisse, die die Metrikberechnung steuern

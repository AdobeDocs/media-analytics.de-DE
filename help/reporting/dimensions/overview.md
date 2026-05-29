---
title: Übersicht über Streaming-Mediendimensionen
description: Erfahren Sie, wie Streaming-Mediendimensionen in Adobe Analytics und Customer Journey Analytics gefüllt und organisiert werden.
feature: Dimensions
role: User, Admin
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# Übersicht über Streaming-Mediendimensionen

Mit Dimensionen in Streaming Media Analytics können Sie Metriken nach Inhaltsname, Stream-Typ, Anzeigename und Dutzenden anderen Attributen sortieren und filtern. Die meisten werden vom Spieler zu Beginn der Sitzung festgelegt und bis zum Ende der Sitzung übertragen.

## So werden Dimensionen ausgefüllt

Streaming-Mediendimensionen folgen drei Hauptpopulationsmustern:

* **Vom Medien-Player bereitgestellt**: Die Quelle für die meisten Dimensionen. Der Player sendet diese Werte im Aufruf [Sitzungsstart](/help/implementation/events/session/session-start.md) und das Medien-Backend hängt sie an jedes nachfolgende Ereignis in der Sitzung an. Was der Player beim Sitzungsstart sendet, wird in Berichten angezeigt. Beispiele sind [[!UICONTROL Stream-]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL Inhaltsname]](/help/reporting/dimensions/content-name.md) und [[!UICONTROL Inhaltslänge]](/help/reporting/dimensions/content-length.md).

* **Abgeleitete Werte**: Dimensionen, die das Medien-Backend aus dem akkumulierten Wiedergabestatus berechnet, anstatt einen vom Player bereitgestellten Wert zu lesen. [[!UICONTROL Inhaltssegment]](/help/reporting/dimensions/content-segment.md) wird im Verlauf der Wiedergabe aus der Abspielposition berechnet. [[!UICONTROL Medienpfad]](/help/reporting/dimensions/media-path.md) verfolgt Übergänge zwischen Inhalts- und Anzeigenstatus über die gesamte Sitzung hinweg. Diese Dimensionen können vom Player nicht überschrieben werden.

* **Classifications**: Optional. Anstatt separate Dimensionen auszufüllen, können Sie Klassifizierungsdaten mithilfe von [Klassifizierungssätze](https://experienceleague.adobe.com/de/docs/analytics/components/classifications/sets/overview) (Adobe Analytics) oder [Lookup-Datensätze](https://experienceleague.adobe.com/en/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics) verwalten.

## Verfügbarkeit nach Berichtssystem

| Meldesystem | So kommen Dimensionen an |
| --- | --- |
| Adobe Analytics | Wird mit [Kontextdatenvariablen“ ](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/page-vars/contextdata). Einige Dimensionen werden automatisch mithilfe dieser Kontextdatenvariablen mit Dimensionen gefüllt, während andere mithilfe von [Verarbeitungsregeln“ ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) werden müssen. Für Dimensionen, die Werte automatisch ausfüllen, muss zunächst die entsprechende Einstellung [Streaming Media Report Suite](../../implementation/media-sdk/setup/media-reports-enable.md) aktiviert werden. |
| Customer Journey Analytics | XDM-Felder befinden sich normalerweise in `xdm.mediaReporting.sessionDetails` und werden aus jedem Datensatz bezogen, der Streaming-Mediendaten enthält. Sie müssen jede Dimension mit den gewünschten Einstellungen in [Komponenteneinstellungen für die Datenansicht](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview) erstellen. |
| Daten-Feeds | Dimensionen werden automatisch mit eigenen Daten-Feed-Spaltennamen ausgefüllt (z. B. `videostreamtype`, `videoname` oder `videolength`). Dimensionen, für die Verarbeitungsregeln erforderlich sind, verwenden `evar` Spaltennamen. |
| Audience Manager | Kontextdaten aus Adobe Analytics weitergeleitet. Nur verfügbar, wenn Server-seitige Weiterleitung von Analytics an Audience Manager konfiguriert ist. |

>[!MORELIKETHIS]
>
>* [Ereignisübersicht](/help/implementation/events/overview.md): Die Player-Ereignisse, die Dimensionen befüllen
>* [Variablenübersicht](/help/implementation/variables/overview.md): Die Daten, die Ereignisse an Adobe übertragen
>* [Metriken - Übersicht](/help/reporting/metrics/overview.md): Die Berichtsmetriken, mit denen Variablen gefüllt werden

---
title: Medienpfad
description: Erfasst die Inhalts-ID als Traffic-Variable für die Pfadanalyse.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 4%

---


# Medienpfad

Die Dimension **Medienpfad** erfasst die Inhalts-ID als Traffic-Variable (Prop), sodass sie in der Pfadanalyse verwendet werden kann (z. B. in den Flussberichten für den nächsten Inhalt und den vorherigen Inhalt). Dies gilt nur für Adobe Analytics: Customer Journey Analytics speichert keine Traffic-Variablen und die Pfade werden direkt für die Dimension „Inhalt (ID)“ festgelegt.

## So wird diese Dimension ausgefüllt

Der Medienpfad wird automatisch aus der Inhalts-ID abgeleitet, die beim Sitzungsstart festgelegt wurde. Es gibt keine separate Variable zum Festlegen. Die Daten-Feed-Spalte `videopath` wird immer dann ausgefüllt, wenn Content (ID) ausgefüllt wird.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus Kontextdaten erfasst, die als Traffic-Variable (Prop) `a.media.name` werden, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | K. A. - [Inhalt](content.md) für Pfadanalyse verwenden |
| Daten-Feeds | `videopath, post_videopath` |

>[!IMPORTANT]
>
>In Pfadsetzungsberichten wird der Eigenschaftswert über Treffer innerhalb desselben Besuchs hinweg verglichen. Wenn sich Inhalt (ID) während eines Besuchs ändert (z. B. wenn ein Viewer von einem Inhaltselement zu einem anderen wechselt), zeigt der Pfadbericht diesen Fluss an.

## Dimensionselemente

Jedes Element ist eine Inhalts-ID, die während eines Besuchs gemeldet wird. Verwenden Sie die Berichte Nächster Seitenfluss und Vorheriger Seitenfluss unter Inhalt > Medienpfad in Adobe Analytics, um Navigationspfade zwischen Inhalten und Inhalten anzuzeigen.

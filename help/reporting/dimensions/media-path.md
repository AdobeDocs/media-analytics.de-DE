---
title: Medienpfad
description: Erfasst die Inhalts-ID als Traffic-Variable für die Pfadanalyse.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 6%
---

# Medienpfad

Die Dimension **Medienpfad** erfasst die Inhalts-ID als Traffic-Variable (Prop), sodass sie in der Pfadanalyse verwendet werden kann (z. B. in den Flussberichten für den nächsten Inhalt und den vorherigen Inhalt). Dies gilt nur für Adobe Analytics: Customer Journey Analytics speichert keine Traffic-Variablen und die Pfade werden direkt für die Dimension „Inhalt (ID)“ festgelegt.

## So wird diese Dimension ausgefüllt

Der Medienpfad wird automatisch aus der Inhalts-ID abgeleitet, die beim Sitzungsstart festgelegt wurde. Es gibt keine separate Variable zum Festlegen. Die Daten-Feed-Spalte `videopath` wird immer dann ausgefüllt, wenn Content (ID) ausgefüllt wird.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus Kontextdaten erfasst, die als Traffic-Variable (Prop) `a.media.name` werden, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | Nicht zutreffend - Verwenden Sie [Inhalt](content.md) für die Pfadanalyse. |
| Daten-Feeds | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Adobe Analytics-Props sind auf 100 Byte begrenzt. Werte, die länger als 100 Byte sind, werden abgeschnitten.

>[!IMPORTANT]
>
>In Pfadsetzungsberichten wird der Eigenschaftswert über Treffer innerhalb desselben Besuchs hinweg verglichen. Wenn sich Inhalt (ID) während eines Besuchs ändert (z. B. wenn ein Viewer von einem Inhaltselement zu einem anderen wechselt), zeigt der Pfadbericht diesen Fluss an.

## Dimensionselemente

Jedes Element ist eine Inhalts-ID, die während eines Besuchs gemeldet wird. Sie können Fluss-Bedienfelder verwenden, um Navigationspfade zwischen Inhalten anzuzeigen.

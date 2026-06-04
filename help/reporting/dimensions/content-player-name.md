---
title: Name des Inhalts-Players
description: Gibt an, welcher Player jede Mediensitzung gerendert hat.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---


# Name des Inhalts-Players

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Name des Content-Players**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/content-player-name.md) unter „Name des Inhalts-Players“*

>[!ENDSHADEBOX]

Die **Name des Content** Players“ gibt an, welcher Player jede Mediensitzung gerendert hat (z. B. `HTML5 Player`, `Brightcove` oder `Roku Player`). Verwenden Sie sie, um die Interaktion, den Abschluss und die Qualität zwischen den Playern in derselben Eigenschaft zu vergleichen.

## So wird diese Dimension ausgefüllt

Der Player-Name wird vom Player beim Sitzungsstart festgelegt und bleibt für die Dauer der Sitzung bestehen. Der Wert wird bei jedem Ereignis gesendet und sowohl in Adobe Analytics als auch in Customer Journey Analytics gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.playerName`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Wenn der Player-Name nicht festgelegt ist, wird die Dimension für diese Sitzung nicht ausgefüllt. Sitzungen ohne Player-Namen können im Reporting nicht nach Player aufgeschlüsselt werden.

## Dimensionselemente

Jedes Element ist die literale Zeichenfolge, die beim Sitzungsbeginn festgelegt wird. Verwenden Sie einen stabilen, eindeutigen Namen pro Player, damit Daten von verschiedenen Playern nicht in einem einzigen Zeileneintrag zusammenfallen.

---
title: Migrieren von Profilen in die neuen Streaming-Medienfelder
description: Erfahren Sie, wie Sie Profile zu den neuen Streaming Media-Feldern migrieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 0%

---

# Migrieren von Profilen in die neuen Streaming-Medienfelder

In diesem Dokument wird der Prozess der Migration des Profilfilterdienstes beschrieben, der zusätzlich zu den Adobe-Datenerfassungsflüssen vorhanden ist, die für Adobe Analytics für Streaming-Mediendaten aktiviert sind. Bei der Migration wird der Profilfilterdienst von mithilfe des Datentyps „Media“ für Adobe-Streaming-Mediendienste in den neuen Datentyp &quot;[ Media Reporting Details“ ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details).

## Profile migrieren

Um die Profilfilterung vom alten Datentyp namens „Media“ zum neuen Datentyp namens &quot;[Media Reporting Details“ ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details), müssen Sie die vorhandenen Profilfilterregeln bearbeiten:

1. Wechseln Sie in Adobe Experience Platform [!UICONTROL **Abschnitt**] Quellen“ zur Registerkarte [!UICONTROL **Datenflüsse**].

1. Suchen Sie den Datenfluss, der für den Import von Streaming-Mediendaten von Adobe Analytics nach Adobe Experience Platform über die Adobe-Datenerfassung verantwortlich ist.

1. Wählen Sie [!UICONTROL **Datenfluss aktualisieren**], um die Einrichtung der Profilfilterung zu ändern, indem Sie jede benutzerdefinierte Regel, die ein verworfenes Feld enthält, durch das neue entsprechende Feld aus dem neuen XDM-Objekt ersetzen.

1. Suchen Sie die Filter, die Felder aus dem veralteten Objekt „Medien“ enthalten.

1. Hängen Sie diese Filter an, indem Sie Felder aus dem neuen Objekt „Details zur Medienberichterstattung“ hinzufügen.

1. Verwenden Sie einen OR-Operator zwischen den beiden Feldern.

1. Überprüfen Sie, ob die Profile weiterhin erwartungsgemäß funktionieren.

Informationen zum Zuordnen zwischen den alten [ den neuen Feldern finden Sie unter dem Parameter ](/help/reporting/dimensions/content.md)Content ID](/help/media-overview.md) und unter den übrigen unter [Streaming-Mediendienste dokumentierten Streaming-Medienvariablen . Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“.

## Beispiel

Um die Befolgung der Migrationsrichtlinien zu vereinfachen, sehen Sie sich den folgenden Beispiel-Datenfluss an, der eine einzelne Profilfilterregel enthält. Da es in diesem Fall nur eine einzige Regel gibt, müssen Sie die Migrationsrichtlinien nur einmal anwenden.

1. Wechseln Sie in Adobe Experience Platform [!UICONTROL **Abschnitt**] Quellen“ zur Registerkarte [!UICONTROL **Datenflüsse**].

&#x200B;1. Suchen Sie den Datenfluss, der für den Import von Streaming-Mediendaten von Adobe Analytics nach Adobe Experience Platform über Adobe Analytics verantwortlich ist.

1. Wählen **[!UICONTROL Datenfluss aktualisieren]**, um in die Bearbeitungsbenutzeroberfläche zu gelangen, wie in der folgenden Abbildung dargestellt.

   ![AEP-Datenflussprofil](assets/aep-dataflow-profile.jpeg)

1. Wählen Sie **[!UICONTROL Weiter]**, um zur Registerkarte Filterung zu wechseln.

   ![Registerkarte &quot;AEP-Datenflussfilter“](assets/aep-dataflow-filtering-profile.jpeg)

1. Identifizieren Sie auf **[!UICONTROL Registerkarte]** die Filterregeln, die auf `media.mediaTimed` Feldern basieren.

   ![AEP-Datenflussfilterregeln](assets/dataflow-filtering-rules-profile.jpeg)


   Suchen Sie für jeden Filter, der das media.mediaTimed-Objekt verwendet, mithilfe der unter „Streaming-Mediendienste“ dokumentierten Streaming[Medienvariablen im `mediaReporting`-Objekt ](/help/media-overview.md) Zuordnung zwischen den alten und den neuen Feldern. Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, während der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“ zu finden ist. Beispielsweise wird für [Medienstarts](/help/reporting/metrics/media-starts.md) der Korrespondent für `media.mediaTimed.impressions.value` `mediaReporting.sessionDetails.isViewed`.

   ![Neue und alte XDM-Felder](assets/xdm-fields-new-and-old.jpeg)

1. Ziehen Sie das entsprechende `mediaReporting` in die Filterregel und verwenden Sie zwischen den beiden Regeln den OR-Operator. Fügen Sie bei Verwendung des neuen Felds dieselbe Regel wie die vorhandene hinzu.

   ![Filterregeln hinzufügen](assets/add-filter-rules.jpeg)

1. Klicken Sie **[!UICONTROL Weiter]**, um Ihre Änderungen zu speichern.

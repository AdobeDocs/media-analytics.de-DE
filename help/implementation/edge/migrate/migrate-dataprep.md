---
title: Migrieren der Datenvorbereitung für benutzerdefinierte Felder in die neuen Felder für Streaming-Medien
description: Erfahren Sie, wie Sie den Datentyp Datenvorbereitung für benutzerdefinierte Felder in die neuen Felder für Streaming-Medien migrieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7294b147-2bef-463f-bada-cb67c16d01b0
TQID: https://experienceleague.adobe.com/57wAwVCwAUlRcMAbFW-X6T6Fe7Ap6leOaQw2Vx9r3OA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 700
ht-degree: 0%

---

# Migrieren der Datenvorbereitung für benutzerdefinierte Felder in die neuen Felder für Streaming-Medien

In diesem Dokument wird der Prozess der Migration des Datenvorbereitungs-Service beschrieben, der zusätzlich zu den Adobe-Datenerfassungsflüssen vorhanden ist, die für Adobe Streaming Media Collection-Daten aktiviert sind. Bei der Migration wird eine Datenvorbereitung-Zuordnung aus dem Datentyp „Medien“ der Streaming-Mediensammlung von Adobe in den neuen entsprechenden Datentyp &quot;[ Media Reporting Details“ ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details).

## Migrieren der Datenvorbereitung für benutzerdefinierte Felder

Um die Datenvorbereitungs-Zuordnungen vom alten Datentyp namens „Media“ zum neuen Datentyp namens &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) zu migrieren, müssen Sie die Datenvorbereitungs-Zuordnungen bearbeiten:

>[!IMPORTANT]
>
>Um Datenverluste zu vermeiden, stellen Sie sicher, dass der Analytics-Quell-Connector mithilfe der neuen `mediaReporting` bereitgestellt wurde, bevor Sie die Schritte in diesem Abschnitt ausführen.

1. Wechseln Sie in Adobe Experience Platform **[!UICONTROL Abschnitt]** Quellen“ zur Registerkarte **[!UICONTROL Datenflüsse]**.

1. Suchen Sie den Datenfluss, der für den Import von Streaming-Mediendaten von Adobe Analytics nach Adobe Experience Platform über die Adobe-Datenerfassung verantwortlich ist.

1. Wählen Sie **[!UICONTROL Datenfluss aktualisieren]**, um die Datenvorbereitungs-Einrichtung zu ändern, indem jede benutzerdefinierte Quellzuordnung, die ein veraltetes Feld enthält, durch das neue entsprechende Feld aus dem neuen XDM-Objekt ersetzt wird.

1. Suchen Sie die Zuordnungen, die Quellfelder aus dem veralteten Objekt „Media“ enthalten.

1. Ersetzen Sie diese Quellen mithilfe von Feldern aus dem neuen Objekt „Details zur Medienberichterstattung“.

1. Überprüfen Sie, ob die Zuordnungen weiterhin erwartungsgemäß funktionieren.

Informationen zum Zuordnen zwischen den alten [ den neuen Feldern finden Sie unter dem Parameter ](/help/reporting/dimensions/content.md)Content ID](/help/media-overview.md) und unter den übrigen unter [Streaming-Mediendienste dokumentierten Streaming-Medienvariablen . Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, während der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“ zu finden ist.

## Beispiel

Um die Befolgung der Migrationsrichtlinien zu vereinfachen, sehen Sie sich den folgenden Beispiel-Datenfluss an, der eine einzelne Zuordnung enthält. In diesem Fall müssen Sie die Migrationsrichtlinien nur einmal anwenden.

1. Wechseln Sie in Adobe Experience Platform **[!UICONTROL Abschnitt]** Quellen“ zur Registerkarte **[!UICONTROL Datenflüsse]**.

1. Suchen Sie den Datenfluss, der für den Import von Streaming-Mediendaten von Adobe Analytics nach Adobe Experience Platform über die Adobe-Datenerfassung verantwortlich ist.

1. Wählen **[!UICONTROL Datenfluss aktualisieren]**, um in die Bearbeitungsbenutzeroberfläche zu gelangen, wie in der folgenden Abbildung dargestellt.

   ![AEP-Datenfluss](../../assets/aep-dataflow.jpeg)

1. Wählen Sie auf der **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Benutzerdefiniert]** aus.

1. Identifizieren Sie die benutzerdefinierten Zuordnungen, die auf `media.mediaTimed` Feldern als Quellen basieren.

   ![AEP-Datenfluss fortgesetzt](../../assets/aep-dataflow2.jpeg)

   Da Sie in diesem Beispiel eine benutzerdefinierte Feldergruppe für das Schema in Ihrer Entwicklungsorganisation erstellt haben, befindet sich das Zielfeld unter `_dcbl`. Der Pfad der benutzerdefinierten Feldergruppe unterscheidet sich je nach Organisationsname.

1. Suchen Sie für jede Zuordnung, die das `media.mediaTimed`-Objekt verwendet, mithilfe dieser Dokumentation im `mediaReporting`-Objekt nach der entsprechenden Person.

   Beispiel: Für „Network“ wird der Korrespondent für &quot;`media.mediaTimed.primaryAssetViewDetails`.broadcastNetwork“ `xdm.mediaReporting.sessionDetails.network`.

   ![Aktualisierter XDM-Feldpfad](../../assets/xdm-field-path-old-and-new.jpeg)

1. Ersetzen Sie im ]****[!UICONTROL  Source den `media.mediaTimed` durch den `mediaReporting`. Das Zielfeld bleibt unverändert.

   ![AEP-Datenfluss fortgesetzt](../../assets/aep-dataflow3.jpeg)

1. Klicken Sie **[!UICONTROL Weiter]**, um Ihre Änderungen zu speichern.

   Der Status wird als &quot;**[!UICONTROL &quot;]**. Nachdem die Änderungen angewendet wurden, wird der Status als &quot;**[!UICONTROL &quot;]**.

   ![AEP-Datenfluss fortgesetzt](../../assets/aep-dataflow5.jpeg)

## Beispiel mit verschiedenen Datentypen

Im obigen Beispiel waren alle beteiligten Datentypen „String“, sodass die Zuordnungsersetzung direkt erfolgte.

Wenn der Quellfelddatentyp nicht mit dem Zielfelddatentyp übereinstimmt, müssen Sie die Richtlinien im [Handbuch zur Fehlerbehebung bei der Datenvorbereitung](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/troubleshooting-guide), [Umgang mit Datenformaten mit der ](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/data-handling) und [Funktionen zur Datenvorbereitung](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/data-handling).

Wenn beispielsweise der Quelltyp eine Zeichenfolge und der Zieltyp ein boolescher Wert ist, kann die Datenvorbereitung den Wert automatisch analysieren und den Quellwert in einen booleschen Wert konvertieren.

Wenn der Quelltyp eine Zahl und der Zieltyp ein boolescher Wert ist, müssen Sie Datenmanipulationsfunktionen verwenden:

Zuordnung mit `media.mediaTimed` zu einem benutzerdefinierten Feld.

![AEP-Datenfluss fortgesetzt](../../assets/aep-dataflow6.jpeg)

Zuordnung mit `mediaReporting` zum selben benutzerdefinierten Feld:

![AEP-Datenfluss fortgesetzt](../../assets/aep-dataflow7.jpeg)

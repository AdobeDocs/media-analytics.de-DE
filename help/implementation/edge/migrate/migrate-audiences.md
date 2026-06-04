---
title: Migrieren von Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien migrieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
TQID: https://experienceleague.adobe.com/TqsfcR2JgxVjDNx3-CBBa9n6pwvuGk9JgQ--DvWeHg0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 1%

---

# Migrieren von Zielgruppen zu den neuen Streaming-Medienfeldern

In diesem Dokument wird beschrieben, wie eine Zielgruppe, die Felder aus dem Datentyp „Medien“ von Adobe Streaming Media Services verwendet, migriert werden sollte, um den neuen entsprechenden Datentyp namens &quot;[&#x200B; Media Reporting Details“ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) verwenden.

## Migrieren einer Zielgruppe

Um eine Zielgruppe vom alten Datentyp „Media“ in den neuen Datentyp &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot; zu migrieren, müssen Sie die Zielgruppe bearbeiten und in jeder Regel das alte Feld vom veralteten Datentyp durch das neue entsprechende Feld vom neuen Datentyp ersetzen:

1. Suchen Sie Regeln, die Felder aus dem veralteten Datentyp „Medien“ enthalten. Dies sind alle Felder, die `media.mediaTimed` mit dem Pfad beginnen.

1. Duplizieren Sie diese Regeln mithilfe der Felder aus dem neuen Datentyp [Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details).

1. Behalten Sie beide Regeln bei, bis Sie überprüfen, ob die Zielgruppen erwartungsgemäß funktionieren.

1. Entfernen Sie die Regeln, die Felder enthalten, aus dem veralteten Datentyp „Medien“.

1. Überprüfen Sie, ob die Zielgruppen weiterhin erwartungsgemäß funktionieren.

Informationen zum Zuordnen zwischen den alten [&#x200B; den neuen Feldern finden Sie unter dem Parameter &#x200B;](/help/reporting/dimensions/content.md)Content ID[&#128279;](/help/media-overview.md) und unter den übrigen unter Streaming-Mediendienste dokumentierten Streaming-Medienvariablen . Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, während der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“ zu finden ist.

![Alte und neue XDM-Feldpfade](../../assets/field-paths-updated.jpeg)

## Beispiel

Um die Befolgung der Migrationsrichtlinien zu vereinfachen, sehen Sie sich das folgende Beispiel an, das eine Zielgruppe mit einer einzigen Regel enthält. Da die Zielgruppe über eine einzige Regel verfügt, müssen Sie die Migrationsrichtlinien nur einmal anwenden.

1. Klicken Sie auf **[!UICONTROL Schaltfläche]** Zielgruppe bearbeiten“ in der oberen rechten Ecke.

1. Suchen Sie die für die Zielgruppe konfigurierten Regeln.

   ![Zielgruppe bearbeiten](../../assets/audience-edit.jpeg)

   ![Zielgruppe bearbeiten](../../assets/audience-edit2.jpeg)

1. Wählen Sie die Regel aus, um ihre Konfiguration zu öffnen.

   ![Zielgruppe bearbeiten](../../assets/audience-edit3.jpeg)

1. (Optional) Um den Pfad des in der Regel verwendeten Felds anzuzeigen, klicken Sie auf die Informationsschaltfläche neben dem Feldnamen.

   ![Zielgruppe bearbeiten](../../assets/audience-edit4.jpeg)

1. Identifizieren Sie den Feldnamen (in diesem Fall „Medienstarts„).

   ![Zielgruppe bearbeiten](../../assets/audience-edit5.jpeg)

1. Informationen zur Zuordnung zwischen den alten Feldern finden Sie in der Dokumentation [Streaming](/help/media-overview.md)Medienvariablen unter „Streaming-Mediendienste . Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“. Beispielsweise wird für den Parameter [Medienstarts](/help/reporting/metrics/media-starts.md) der Korrespondent für `media.mediaTimed.impressions.value` `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Aktualisierter XDM-Pfad](../../assets/updated-xdm-path.jpeg)

1. Fügen Sie dieselbe Regel wie bei der vorhandenen hinzu, indem Sie das neue Feld verwenden.

   ![Regel hinzufügen](../../assets/add-rule.jpeg)

   ![Regel hinzufügen](../../assets/add-rule2.jpeg)

   ![Regel hinzufügen](../../assets/add-rule3.jpeg)

1. Klicken Sie **[!UICONTROL Speichern]**, um die Zielgruppe zu speichern. Sie können diese Einrichtung so lange beibehalten, wie Sie überprüfen müssen, ob die Zielgruppe weiterhin wie erwartet funktioniert.

1. Entfernen Sie nach Abschluss der Validierung das alte Feld und klicken Sie auf **[!UICONTROL Speichern]** um die Audience zu speichern.

   ![Regel hinzufügen](../../assets/add-rule4.jpeg)

1. Validieren Sie die Zielgruppe erneut.

   Der Prozess zur Migration der Zielgruppe ist abgeschlossen.

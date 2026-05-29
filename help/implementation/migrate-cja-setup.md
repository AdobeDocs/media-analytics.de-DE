---
title: Migrieren von Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien migrieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 1%

---

# Migrieren von Customer Journey Analytics zur Verwendung der neuen Streaming-Medienfelder

In diesem Dokument wird beschrieben, wie ein Customer Journey Analytics-Setup, das den Datentyp Adobe Streaming Media Services namens „Media“ verwendet, so aktualisiert werden sollte, dass er den neuen entsprechenden Datentyp namens &quot;[&#x200B; Media Reporting Details“ &#x200B;](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details).

## Migrieren von Customer Journey Analytics

Um ein Customer Journey Analytics-Setup aus dem alten Datentyp „Media“ in den neuen Datentyp &quot;[Media Reporting Details](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details)&quot; zu migrieren, müssen Sie die folgenden Setups aktualisieren, die den alten Datentyp verwenden:

* Datenansichten

* Abgeleitete Felder

### Datenansichten migrieren

So migrieren Sie die Datenansichten in den neuen Datentyp:

1. Suchen Sie alle Datenansichten mithilfe des veralteten Datentyps „Medien“. Dies sind alle Felder, bei denen der Pfad mit `media.mediaTimed` beginnt.

1. Führen Sie einen der folgenden Schritte aus:

   * Fügen Sie in diese Datenansichten die Felder aus dem neuen Datentyp „Media Reporting Details“ ein.

   * Erstellen Sie ein abgeleitetes Feld, das den neuen Datentyp „Media Reporting Details“ verwendet, wenn er festgelegt ist, oder das auf den alten Datentyp „Media“ zurückgreift, wenn der Datentyp „Media Reporting Details“ nicht festgelegt ist.

### Migrieren abgeleiteter Felder

So migrieren Sie abgeleitete Felder in den neuen Datentyp:

1. Suchen Sie alle abgeleiteten Felder mit dem veralteten Datentyp „Medien“. Dies sind alle abgeleiteten Felder, die Felder enthalten, bei denen der Pfad mit `media.mediaTimed` beginnt.

1. Ersetzen Sie alle alten Felder im abgeleiteten Feld durch das neue entsprechende Feld aus „Details zur Medienberichterstattung“.

Informationen zum Zuordnen zwischen den alten [&#x200B; den neuen Feldern finden Sie unter dem Parameter &#x200B;](/help/reporting/dimensions/content.md)Content ID[&#128279;](/help/media-overview.md) und unter den übrigen unter Streaming-Mediendienste dokumentierten Streaming-Medienvariablen . Der alte Feldpfad befindet sich unter der Eigenschaft „XDM-Feldpfad“, während der neue Feldpfad unter der Eigenschaft „XDM-Feldpfad für Berichterstellung“ zu finden ist.

![Alte und neue XDM-Feldpfade](assets/field-paths-updated.jpeg)

## Beispiel

Um die Befolgung der Migrationsrichtlinien zu vereinfachen, sehen Sie sich das folgende Beispiel an, das eine Datenansicht mit Feldern aus dem alten, veralteten Datentyp „Medien“ enthält. In dieser Datenansicht müssen Sie die neuen entsprechenden Felder hinzufügen.

### Datenansicht aktualisieren

Sie können eine der folgenden Optionen verwenden, um die Datenansicht zu aktualisieren:

#### Option 1

1. Suchen Sie eine Metrik oder Dimension, die das alte Feld aus dem veralteten Datentyp verwendet.

   ![Alter Feldpfad in Datenansicht](assets/old-field-data-view.jpeg)

1. Aktivieren Sie das entsprechende neue Feld im Artikel [Kapitelversatz](/help/reporting/dimensions/chapter-offset.md) .

1. Suchen Sie das neue entsprechende Feld in der Datenansicht.

   ![Neuer Feldpfad in der Datenansicht](assets/new-field-data-view.jpeg)

1. Ziehen Sie das neue Feld auf die Metrik oder Dimension.

1. Wiederholen Sie diesen Vorgang für alle Metriken und Dimensionen, die Felder aus dem veralteten Datentyp „Medien“ verwenden.

#### Option 2

Mit dieser Option wird ein abgeleitetes Feld erstellt, das den Wert aus dem alten Feld oder den Wert aus dem neuen Feld auswählt, je nachdem, welches Feld für ein bestimmtes Ereignis vorhanden ist. Dieses abgeleitete Feld ersetzt in allen Projekten, in denen es verwendet wird, den alten Datentyp „Medien“.

Wenn Sie ein abgeleitetes Feld für den „Kapitelnamen“ erstellen möchten, das den neuen Datentyp „Details zur Medienberichterstattung“ verwendet, wenn er festgelegt ist, oder das auf den alten Datentyp „Medien“ zurückgreift, wenn der Datentyp „Details zur Medienberichterstattung“ nicht festgelegt ist:

1. Ziehen Sie eine „Wenn-Fall“-Klausel in die abgeleiteten Felder.

   ![Passen Sie das neue Feld an, um eine Datenansicht zu erstellen](assets/create-derived-field2.jpeg)

1. Füllen Sie die [!UICONTROL **If**]-Klausel mit dem Wert der **XDM-Feldpfad für Berichterstellung**, wie auf der Seite [Kapitelname](/help/reporting/dimensions/chapter-name.md) dargestellt.

   ![Kapitelname](assets/chapter-name.jpeg)

   ![Kapitelname](assets/chapter-name2.jpeg)

   ![Abgeleitete Feldbedingung](assets/derived-field-condition.jpeg)

   ![Abgeleitetes Feld: Kapitelname](assets/derived-field-chapter-name.jpeg)

1. Füllen Sie den Fallback-Wert mit dem alten Feld aus dem veralteten Datentyp „Media“.

   ![Fallback-Wert](assets/fallback-value.jpeg)

   ![Fallback-Wert](assets/fallback-value2.jpeg)

   Dies ist die endgültige Definition des abgeleiteten Feldes.

   ![Abgeleitetes Feld abgeschlossen](assets/derived-field-complete.jpeg)

1. Um die abgeleiteten Felder zu aktualisieren, suchen Sie ein abgeleitetes Feld, das die alten verworfenen Felder verwendet (Pfad, der mit `media.mediaTimed` beginnt).

   ![abgeleitetes Feld](assets/old-derived-field.jpeg)

1. Bewegen Sie den Mauszeiger über das abgeleitete Feld, das Sie aktualisieren möchten, und wählen Sie dann das Symbol [!UICONTROL **Bearbeiten**] aus.

1. Suchen Sie alle Felder aus dem alten Datentyp (Pfad, der mit `media.mediaTimed` beginnt) und ersetzen Sie sie durch das neue entsprechende Feld.

   ![Suchen eines Felds mit altem Datentyp](assets/locate-fields-with-old-datatype.jpeg)

1. Aktivieren Sie das entsprechende neue Feld im Artikel [Inhaltsname](/help/reporting/dimensions/content-name.md) .

1. Ersetzen Sie das alte Feld durch das neue Feld.

   ![Neues Feld](assets/derived-field-new.jpeg)

1. Wiederholen Sie diesen Vorgang für alle abgeleiteten Felder, die Felder aus dem alten, veralteten Datentyp „Medien“ verwenden.

   Die Migration der CJA-Einrichtung ist abgeschlossen.

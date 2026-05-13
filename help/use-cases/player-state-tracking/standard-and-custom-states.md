---
title: Über Standard- und benutzerdefinierte Status
description: Erfahren Sie mehr über die Player-Status-Tracking-Funktion einschließlich Anforderungen und Richtlinien für die Implementierung und das Reporting von Standard- und benutzerdefinierten Player-Status.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/QdUkyWt6cTcdmQXpj6Qe6-s3aYkGfro-G7DYegOVKvA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 96%

---

# Über Standard- und benutzerdefinierte Status

Es stehen fünf standardmäßige Player-Status zur Verfügung und Sie können Ihre eigenen benutzerdefinierten Status hinzufügen.

| Name des Standardstatus | Medien-SDK-Konstante | Name der Mediensammlungs-API |
|-----------------------|------------------------------------------|-----------------------------|
| Vollbild | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Verdeckter Untertitel | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Stummschaltung | `ADB.Media.PlayerState.Mute` | `mute` |
| Bild im Bild | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Fokus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Die Daten werden für Standard- und benutzerdefinierte Status auf dieselbe Weise berechnet, aber die Daten für Analytics-Berichte werden unterschiedlich gespeichert.

**Für Standardstatus**: Wenn Sie das Player-Status-Tracking über die Media Management-Konsole in Analytics-Berichten aktivieren (Admin-Seite), stehen 15 Lösungsvariablen für Berichte- und Datenexporte zur Verfügung.

**Für benutzerdefinierte Status**: Sie können eigene Verarbeitungsregeln erstellen, um die berechneten Werte in benutzerdefinierten Ereignissen zu speichern, und diese Regeln dann für Berichte und Datenexporte verwenden.

## Richtlinien

* Eine Videositzung ist auf zehn Player-Status beschränkt.
* Jede Statuskombination ist zulässig.
* Wenn mehrere Player-Status vorhanden sind, werden nur die ersten zehn beibehalten und an die VA-Verarbeitungskomponente (Videoanalyse) weitergeleitet.
* Die maximale Anzahl von zehn Status wird auf alle Status angewendet, unabhängig davon, ob sie abgeschlossen sind oder nicht.
* Ein Status kann mehrmals gestartet und beendet werden und wird als ein Status gezählt. `closedCapationing` kann beispielsweise fünfmal gestartet und gestoppt werden, es wird jedoch als einzelner Status gezählt.
* Alle Status, die die maximal zulässige Anzahl von 10 Status überschreiten, werden verworfen.

## Benutzerdefinierte Status

Mit der Möglichkeit, benutzerdefinierte Status zu erstellen, können Sie benutzerdefinierte Aktionen erfassen und benutzerdefinierte Metadaten während einer Wiedergabesitzung aktualisieren.

Weitere Informationen zum Erstellen benutzerdefinierter Status finden Sie im [Leitfaden zur Medien-API-Referenz: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)

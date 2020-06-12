---
title: Über Standard- und benutzerdefinierte Status
description: In diesem Kapitel wird die Player-Status-Tracking-Funktion beschrieben, einschließlich Anforderungen und Richtlinien für die Implementierung und das Reporting von Standard- und benutzerdefinierten Player-Status.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 66%

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

* Eine Videositzung ist auf 10 Player-Status beschränkt.
* Jede Statuskombination ist zulässig.
* Wenn mehrere Player-Zustände bestehen, werden nur die ersten 10 beibehalten und an die VA-Verarbeitungskomponente weitergeleitet.
* Die maximale Anzahl von zehn Status wird auf alle Status angewendet, unabhängig davon, ob sie abgeschlossen sind oder nicht.
* Ein Status kann mehrmals Beginn und beendet werden und wird als ein Status gezählt. Beispielsweise `closedCapationing` kann fünfmal gestartet und beendet werden, es wird jedoch als einzelner Status gezählt.
* Jeder Status, der die maximal zulässige Anzahl von 10 Status überschreitet, wird verworfen.

## Benutzerdefinierte Status

Mit der Möglichkeit, benutzerdefinierte Status zu erstellen, können Sie benutzerdefinierte Aktionen erfassen und benutzerdefinierte Metadaten während einer Wiedergabesitzung aktualisieren.

Weitere Informationen zum Erstellen benutzerdefinierter Status finden Sie im Handbuch [Media API Reference: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)

---
title: Über Standard- und Benutzerdefinierte Status
description: In diesem Thema wird die Player-Zustandsverfolgungsfunktion beschrieben, einschließlich Anforderungen und Richtlinien für die Implementierung und den Berichte-Standard- und benutzerdefinierten Player-Status.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Standard- und benutzerdefinierte Status

Es stehen fünf standardmäßige Player-Status zur Verfügung und Sie können Ihre eigenen benutzerdefinierten Status hinzufügen.

| Standardstatus | Media SDK-Konstante | Name der Media Collection-API |
|-----------------------|------------------------------------------|-----------------------------|
| Vollbild | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Untertitel | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Stumm | `ADB.Media.PlayerState.Mute` | `mute` |
| Bild in Bild | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Im Brennpunkt | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Die Daten werden auf dieselbe Weise für Standard- und benutzerdefinierte Status berechnet, aber die Daten werden für Analytics Berichte unterschiedlich gespeichert.

**Für Standardzustände**: Wenn Sie die Player-Statusverfolgung über die Media Management-Konsole in Analytics Berichte aktivieren (Admin-Seite), stehen 15 Lösungsvariablen für Berichte- und Datenexporte zur Verfügung.

**Für benutzerdefinierte Zustände**: Sie können eigene Verarbeitungsregeln erstellen, um die berechneten Werte in benutzerdefinierten Ereignissen zu speichern und diese dann für Berichte- und Datenexporte zu verwenden.

## Richtlinien

* Eine Videositzung ist auf 10 Player-Status beschränkt.
* Jede Statuskombination ist zulässig.
* Wenn mehrere Player-Zustände bestehen, werden nur die ersten 10 beibehalten und an die VA-Verarbeitungskomponente weitergeleitet.
* Die maximale Anzahl von 10 Status wird für alle Status angewendet, unabhängig davon, ob sie geschlossen sind oder nicht.
* Ein Status kann mehrmals Beginn und beendet werden und wird als ein Status gezählt. Beispielsweise `closedCapationing` kann fünfmal gestartet und beendet werden, es wird jedoch als einzelner Status gezählt.
* Jeder Status, der die maximal zulässige Anzahl von 10 Status überschreitet, wird verworfen.

## Benutzerdefinierte Status

Mit der Möglichkeit, benutzerdefinierte Status zu erstellen, können Sie benutzerdefinierte Aktionen erfassen und benutzerdefinierte Metadaten während einer Wiedergabesitzung aktualisieren.

Weitere Informationen zum Erstellen benutzerdefinierter Status finden Sie im Handbuch [Media API Reference: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)

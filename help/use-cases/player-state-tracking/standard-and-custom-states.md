---
title: Über Standard- und benutzerdefinierte Status
description: Erfahren Sie mehr über die Player-Status-Tracking-Funktion einschließlich Anforderungen und Richtlinien für die Implementierung und das Reporting von Standard- und benutzerdefinierten Player-Status.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '279'
ht-degree: 100%

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
* Ein Status kann mehrmals gestartet und beendet werden und wird als ein Status gezählt. `closedCapationing` kann beispielsweise fünfmal gestartet und beendet werden, es wird jedoch als einzelner Status gezählt.
* Alle Status, die die maximal zulässige Anzahl von 10 Status überschreiten, werden verworfen.

## Benutzerdefinierte Status

Mit der Möglichkeit, benutzerdefinierte Status zu erstellen, können Sie benutzerdefinierte Aktionen erfassen und benutzerdefinierte Metadaten während einer Wiedergabesitzung aktualisieren.

Weitere Informationen zum Erstellen benutzerdefinierter Status finden Sie im [Leitfaden zur Medien-API-Referenz: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)

---
title: Player-Statusverfolgung
description: In diesem Thema wird die Player-Statusverfolgungsfunktion beschrieben, einschließlich Anforderungen und Richtlinien für die Implementierung und den Berichte-Player-Status.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# Player-Statusverfolgung

Um Ihre Produkterfahrung zu optimieren und den Wert für Ihr Unternehmen zu steigern, ist es wichtig, das Kundenverhalten bei der Anzeige von Videos zu verstehen. Dies schließt die Zeit ein, die in verschiedenen Player-Status verbracht wird.  Um Ihr Verständnis zu optimieren, benötigen Sie die Flexibilität, um nach Bedarf neue Player-Status und -Ereignis zu erstellen und zu messen.

Die Player-Statusverfolgung bietet die Möglichkeit, die Interaktion des Viewers während der Wiedergabe mit einem Standardsatz von Lösungsvariablen für Vollbild, Untertitel, Stummschalten, Bild im Bild und Fokus zu erfassen.  Die Player-Statusverfolgung bietet außerdem die Flexibilität, benutzerdefinierte Player-Status zu erstellen.  Die Player-Statusverfolgungsvariablen sind für den Berichte in Analyse Workspace verfügbar.

Um Änderungen am Player-Status zu erfassen, aktualisiert die Player-Statusverfolgung die Videomessungsmetadaten. Um beispielsweise die Videointeraktion &quot;true&quot;zu ermitteln, misst die Player-Statusverfolgung die mit dem Sound verbrachte Zeit im Vergleich zu den passiven oder nicht aktiven Ansichten, wenn der Ton deaktiviert ist oder die  im Modus &quot;Normal&quot;im Vergleich zum Vollbildmodus abgelaufen ist.

Die Player-Statusverfolgung bietet folgende Vorteile:

* Stellt Standardvariablen bereit, mit denen allgemeine Status wie Vollbild oder Untertitel gemessen werden.
* Bietet anpassbare Variablen zum Messen benutzerdefinierter Zustände während einer Wiedergabesitzung
* Misst die in einem benutzerdefinierten Player-Status verbrachte Zeit
* Misst mehrere Zustände, die gleichzeitig sein können

![Player-Statusverfolgung](assets/player_state_tracking.png)

## Voraussetzungen

Zur Player-Statusverfolgung ist Folgendes für die Media Analytics-Erweiterung zur Verwendung mit Adobe Experience Platform (AEP SDK) erforderlich:
* Web: Adobe Media Analytics (3.x SDK) für Audio und Video, Version 1.0+
* Mobil: Adobe Media Analytics for Audio and Video v2.0+

Wenn Sie sich entscheiden, das AEP SDK nicht zu verwenden, können Sie Folgendes bei der Player-Statusverfolgung verwenden:
* Media JS SDK 3.0+
* Media Collection API-Version?

## Richtlinien

Beachten Sie vor der Implementierung der Player-Statusverfolgung die folgenden Richtlinien.

* Der Player-Status wird über alle Wiedergabestufen berechnet - (keine Aufteilung)
* Sie können mehrere Player-Status gleichzeitig messen
* Die maximale Anzahl von Player-Status, die während einer Wiedergabe verfolgt werden können, beträgt 10 
* Player-Statusmetriken werden NUR beim Media Close-Aufruf an Analytics zum Berichte gesendet
* Der Player-Status wird für jede einzelne Wiedergabesitzung erfasst. Der Player-Status wird nicht über die Wiedergabe hinweg berechnet 

---
title: Über das Player-Status-Tracking
description: In diesem Kapitel wird die Player-Status-Tracking-Funktion beschrieben, einschließlich der Anforderungen und Richtlinien für die Implementierung und die Reporting-Player-Status.
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 66%

---


# Über das Player-Status-Tracking

Um Ihre Produkterfahrung zu optimieren und einen Mehrwert für Ihr Unternehmen zu erhalten, ist es wichtig, das Kundenverhalten bei der Anzeige von Videos zu verstehen. Dies beinhaltet auch die Zeit, die Kunden in verschiedenen Player-Status verbringen.  Es ist auch wichtig, die Flexibilität zu haben, um neue Player-Status und -Ereignis nach Bedarf zu erstellen und zu messen.

Das Player-Status-Tracking bietet die Möglichkeit, die Interaktion des Betrachters während der Wiedergabe mit einem Standardsatz von Lösungsvariablen für Vollbild, verdeckte Untertitel, Stummschaltung, Bild im Bild und Fokus zu erfassen.  Das Player-Status-Tracking ermöglicht außerdem die flexible Erstellung benutzerdefinierter Player-Status. Sie können Player-Statusverfolgungsvariablen für den Berichte im Analysis Workspace verwenden.

Um Änderungen am Player-Status zu erfassen, aktualisiert das Player-Status-Tracking die Videomessungsmetadaten. Um beispielsweise die Videointeraktion „true“ zu ermitteln, misst das Player-Status-Tracking die mit aktiviertem Ton verbrachte Zeit im Vergleich zu passiven oder nicht aktiven Ansichten, wenn der Ton deaktiviert ist, oder die im Modus „Normal“ verbrachte Zeit im Vergleich zum Vollbildmodus.

Das Player-Status-Tracking bietet folgende Vorteile:

* Stellt Standardvariablen bereit, mit denen allgemeine Status wie Vollbild oder verdeckte Untertitel gemessen werden.
* Bietet anpassbare Variablen zum Messen benutzerdefinierter Status während einer Wiedergabesitzung
* Misst die in einem benutzerdefinierten Player-Status verbrachte Zeit
* Misst mehrere Status, die gleichzeitig sein können

![Player-Status-Tracking](assets/player_state_tracking.png)

## Voraussetzungen

Zur Player-Statusverfolgung ist bei der Datenerfassung eine der folgenden Voraussetzungen erforderlich:
* Media JS-SDK 3.0+
* Media Analytics Extension (zur Verwendung mit dem Adobe Experience Platform (AEP) SDK)
   * Web: Adobe Media Analytics (3.x SDK) für Audio und Video, Version 1.0+
   * Mobile: Adobe Media Analytics für Audio und Video, Version 2.0+
* Mediensammlungs-API

## Richtlinien

Beachten Sie vor der Implementierung des Player-Status-Trackings die folgenden Richtlinien.

* Der Player-Status wird über alle Wiedergabestufen berechnet (keine Aufteilung).
* Sie können mehrere Player-Status gleichzeitig messen.
* Die maximale Anzahl von Player-Status, die während einer Wiedergabe getrackt werden können, beträgt 10.
* Player-Statusmetriken werden nur beim Media Close-Aufruf zum Berichte an Analytics gesendet.
* Die Kenntnis des Anwendungsstatus wird nach dem Beenden eines Status nicht beibehalten. Nach dem Ende eines Status muss der Status erneut gestartet werden, um die Verfolgung fortzusetzen. Für jeden neuen Wiedergabestatus muss der Player-Status erneut gestartet werden.
* Der Player-Status wird für jede einzelne Wiedergabesitzung erfasst. Der Player-Status wird nicht für alle Wiedergaben berechnet.

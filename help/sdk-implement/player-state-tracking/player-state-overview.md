---
title: Player-Statusverfolgung
description: In diesem Thema wird die Player-Statusverfolgungsfunktion beschrieben, einschließlich Anforderungen und Richtlinien für die Implementierung und den Berichte-Player-Status.
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---


# Player-Statusverfolgung

Um Ihre Produkterfahrung zu optimieren und den Wert für Ihr Unternehmen zu steigern, ist es wichtig, das Kundenverhalten bei der Anzeige von Videos zu verstehen. Dies schließt die Zeit ein, die in verschiedenen Player-Status verbracht wird.  Es ist auch wichtig, die Flexibilität zu haben, um neue Player-Status und -Ereignis nach Bedarf zu erstellen und zu messen.

Die Player-Statusverfolgung bietet die Möglichkeit, die Interaktion des Viewers während der Wiedergabe mit einem Standardsatz von Lösungsvariablen für Vollbild, Untertitel, Stummschalten, Bild im Bild und Fokus zu erfassen.  Die Player-Statusverfolgung bietet außerdem die Flexibilität, benutzerdefinierte Player-Status zu erstellen. Sie können Player-Statusverfolgungsvariablen für den Berichte in Analyse Workspace verwenden.

Um Änderungen am Player-Status zu erfassen, aktualisiert die Player-Statusverfolgung die Videomessungsmetadaten. Um beispielsweise die Videointeraktion &quot;true&quot;zu ermitteln, misst die Player-Statusverfolgung die mit dem Sound verbrachte Zeit im Vergleich zu den passiven oder nicht aktiven Ansichten, wenn der Ton deaktiviert ist oder die  im Modus &quot;Normal&quot;im Vergleich zum Vollbildmodus abgelaufen ist.

Die Player-Statusverfolgung bietet folgende Vorteile:

* Stellt Standardvariablen bereit, mit denen allgemeine Status wie Vollbild oder Untertitel gemessen werden.
* Bietet anpassbare Variablen zum Messen benutzerdefinierter Zustände während einer Wiedergabesitzung
* Misst die in einem benutzerdefinierten Player-Status verbrachte Zeit
* Misst mehrere Zustände, die gleichzeitig sein können

![Player-Statusverfolgung](assets/player_state_tracking.png)

## Voraussetzungen

Zur Player-Statusverfolgung ist bei der Datenerfassung eine der folgenden Voraussetzungen erforderlich:
* Media JS SDK 3.0+
* Media Analytics Extension (zur Verwendung mit dem Adobe Experience Platform (AEP) SDK)
   * Web: Adobe Media Analytics (3.x SDK) für Audio und Video, Version 1.0+
   * Mobil: Adobe Media Analytics for Audio and Video v2.0+
* Mediensammlungs-API

## Richtlinien

Beachten Sie vor der Implementierung der Player-Statusverfolgung die folgenden Richtlinien.

* Der Player-Status wird über alle Wiedergabestufen berechnet (keine Aufteilung).
* Sie können mehrere Player-Status gleichzeitig messen.
* Die maximale Anzahl von Player-Status, die während einer Wiedergabe verfolgt werden können, beträgt 10.
* Player-Statusmetriken werden nur beim Media Close-Aufruf zum Berichte an Analytics gesendet.
* Die Kenntnis des Anwendungsstatus wird nach dem Beenden eines Status nicht beibehalten. Nach dem Ende eines Status muss der Status erneut gestartet werden, um die Verfolgung fortzusetzen. Für jeden neuen Wiedergabestatus muss der Player-Status erneut gestartet werden.
* Der Player-Status wird für jede einzelne Wiedergabesitzung erfasst. Der Player-Status wird nicht für alle Wiedergaben berechnet.

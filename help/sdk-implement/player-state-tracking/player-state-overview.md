---
title: Über das Player-Status-Tracking
description: Erfahren Sie mehr über die Player-Status-Tracking-Funktion einschließlich der Anforderungen und Richtlinien für die Implementierung und die Reporting-Player-Status.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Über das Player-Status-Tracking

Um Ihre Produkterfahrung zu optimieren und einen Mehrwert für Ihr Unternehmen zu erhalten, ist es wichtig, das Kundenverhalten bei der Anzeige von Videos zu verstehen. Dies beinhaltet auch die Zeit, die Kunden in verschiedenen Player-Status verbringen.  Es ist auch wichtig, die Flexibilität zu haben, bei Bedarf neue Player-Status und -Ereignisse zu erstellen und zu messen.

Das Player-Status-Tracking bietet die Möglichkeit, die Interaktion des Betrachters während der Wiedergabe mit einem Standardsatz von Lösungsvariablen für Vollbild, verdeckte Untertitel, Stummschaltung, Bild im Bild und Fokus zu erfassen.  Das Player-Status-Tracking ermöglicht außerdem die flexible Erstellung benutzerdefinierter Player-Status. Sie können Player-Status-Tracking-Variablen für Berichte in Analysis Workspace verwenden.

Um Änderungen am Player-Status zu erfassen, aktualisiert das Player-Status-Tracking die Videomessungsmetadaten. Um beispielsweise die Videointeraktion „true“ zu ermitteln, misst das Player-Status-Tracking die mit aktiviertem Ton verbrachte Zeit im Vergleich zu passiven oder nicht aktiven Ansichten, wenn der Ton deaktiviert ist, oder die im Modus „Normal“ verbrachte Zeit im Vergleich zum Vollbildmodus.

Das Player-Status-Tracking bietet folgende Vorteile:

* Stellt Standardvariablen bereit, mit denen allgemeine Status wie Vollbild oder verdeckte Untertitel gemessen werden.
* Bietet anpassbare Variablen zum Messen benutzerdefinierter Status während einer Wiedergabesitzung
* Misst die in einem benutzerdefinierten Player-Status verbrachte Zeit
* Misst mehrere Status, die gleichzeitig sein können

![Player-Status-Tracking](assets/player_state_tracking.png)

## Voraussetzungen

Für das Player-Status-Tracking ist bei der Datenerfassung eine der folgenden Voraussetzungen erforderlich:
* Media JS-SDK 3.0+
* Chromecast 3.0 SDK für Adobe Experience Cloud-Lösungen
* Media Analytic-Erweiterung (zur Verwendung für das Adobe Experience Platform-SDK (AEP))
   * Web: Adobe Media Analytics (3.x SDK) für Audio und Video, Version 1.0+
   * Mobile: Adobe Media Analytics für Audio und Video, Version 2.0+
* Mediensammlungs-API

## Richtlinien

Beachten Sie vor der Implementierung des Player-Status-Trackings die folgenden Richtlinien.

* Der Player-Status wird für alle Wiedergabestatus berechnet (keine Aufteilung).
* Sie können mehrere Player-Status gleichzeitig messen.
* Die maximale Anzahl von Player-Status, die während einer Wiedergabe getrackt werden können, beträgt 10.
* Player-Statusmetriken werden nur beim Media-Close-Aufruf an Analytics zum Reporting gesendet.
* Die Angabe des Anwendungsstatus wird nach dem Beenden eines Status nicht beibehalten. Nach dem Beenden eines Status muss der Status erneut gestartet werden, um das Tracking fortzusetzen. Der Status des Players muss für jeden neuen Wiedergabestatus erneut gestartet werden.
* Player-Status werden für jede einzelne Wiedergabesitzung erfasst – der Player-Status wird nicht über mehrere Wiedergaben hinweg berechnet.

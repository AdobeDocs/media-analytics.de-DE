---
title: Über das Player-Status-Tracking
description: Erfahren Sie mehr über die Player-Status-Tracking-Funktion einschließlich der Anforderungen und Richtlinien für die Implementierung und die Reporting-Player-Status.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

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
* Die Angabe des Anwendungsstatus wird nach dem Stoppen eines Status nicht beibehalten. Nach dem Beenden eines Status muss der Status erneut gestartet werden, um das Tracking fortzusetzen. Der Status des Players muss für jeden neuen Wiedergabestatus erneut gestartet werden.
* Player-Status werden für jede einzelne Wiedergabesitzung erfasst – der Player-Status wird nicht über mehrere Wiedergaben hinweg berechnet.

---
title: Aktualisieren einer Analytics-Quell-Connector-Implementierung auf neue XDM-Felder für Streaming-Medien-Services
description: Erfahren Sie mehr über das Migrieren einer Analytics-Quell-Connector-Implementierung in aktualisierte XDM Streaming Media-Felder
feature: Streaming Media
role: User, Admin, Developer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Aktualisieren einer Analytics-Quell-Connector-Implementierung auf neue XDM-Felder für Streaming-Medien-Services

>[!NOTE]
>
>Diese Informationen richten sich an Unternehmen, die den [Analytics-Quell-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) verwenden, um Streaming-Mediendaten von Adobe Analytics in Adobe Experience Platform zur Verwendung mit Customer Journey Analytics-Berichten oder anderen Platform-Services zu übertragen.
>
>Die Änderungen wirken sich nicht auf Adobe Analytics als eigenständige Anwendung aus, einschließlich Datenerfassung, Verarbeitung und Reporting. Tools wie Daten-Feeds und Verarbeitungsregeln sind davon nicht betroffen, sodass keine Aktualisierungen an der Analytics-Implementierung erforderlich sind.

Eine neue Implementierung des Adobe-Datenerfassungs-Connectors (Analytics Source Connector) für den Streaming Media-Service ist jetzt verfügbar, der von einem Satz von XDM-Feldern zu einem anderen migriert.

## Neuer XDM-Feldpfad

Im Rahmen dieser Migration wurde der `mediaReporting` XDM-Feldpfad zu den XDM-Schemata hinzugefügt, die in der Adobe-Datenerfassung (Analytics Source Connector) verwendet werden. Jedes bestehende und neu generierte Adobe-Datenerfassungsschema enthält automatisch dieses neue Feld.

## Ersetzen des alten XDM-Feldpfads

Alle Adobe-Datenerfassungsflüsse (Analytics-Quell-Connector), die Streaming-Mediendaten von Adobe Analytics an Adobe Experience Platform übertragen, senden derzeit Daten sowohl über den neuen `mediaReporting` XDM-Feldpfad als auch über den alten `media.mediaTimed` XDM-Feldpfad. Beide Feldpfade stehen bis Ende Oktober 2025 drei Monate lang zur Verfügung. Nach Oktober werden die `media.mediaTimed` Felder vollständig veraltet sein, und die Daten, die nach Oktober aufgenommen werden, enthalten nur `mediaReporting`. Nach der Einstellung sind die `media.mediaTimed` Felder nicht mehr in der Adobe Experience Platform-Schema-Benutzeroberfläche sichtbar und die Datenaufnahme in diesen Feldern wird gestoppt. Folglich sind diese Felder für die Verwendung in Adobe Experience Platform-Services nicht mehr verfügbar.

Daten, die vor diesem Datum aufgenommen wurden, stehen weiterhin für das Reporting zur Verfügung.

## Zusätzliche Unterschiede zum neuen XDM-Feldpfad

Mit der neuen Implementierung des Adobe-Quell-Connectors für Streaming-Medien werden jetzt Keep-Alive-Aufrufe von Adobe Analytics in Adobe Experience Platform aufgenommen.

Zuvor wurden diese Aufrufe nicht in Platform-Apps wie Customer Journey Analytics aufgenommen. Daher kann Ihre Organisation die folgenden Unterschiede beim Reporting feststellen:

* **Präzise Sitzungsanzahl**: In einigen Fällen kann dies zu einer Deflation der Sitzungsanzahl führen, da Keep-Alive-Aufrufe die Aufrechterhaltung aktiver Benutzersitzungen auch ohne direkte Medieninteraktionen unterstützen. Diese Keep-Alive-Aufrufe werden alle 20 Minuten nach dem letzten Ereignis pro Medienwiedergabe generiert, um den Besuch offen zu halten. Um eine optimale Sitzungsverfolgung in Customer Journey Analytics sicherzustellen, wird empfohlen, den Besuchsablauf in der Datenansicht auf 30 Minuten zu konfigurieren.

* **Erhöhung der Anzahl der Ereignisse**: Da Keep-Alive-Aufrufe jetzt in der Metrik Customer Journey Analytics-Ereignisse gezählt werden. Wenn Sie Keep-Alive-Aufrufe aus dem Reporting ausschließen möchten, können Sie einen Filter erstellen, der Ereignisse mit dem Ereignistyp `media.keepalive` ausschließt.

Durch diese Änderung wird eine bessere Abstimmung zwischen Analytics- und CJA-Reporting sichergestellt.

## Vorhandenes Setup migrieren

Um einen reibungslosen Übergang zu gewährleisten, müssen alle Kunden bestehende Setups von `media.mediaTimed` Feldern bis Ende Oktober 2025 auf `mediaReporting` Felder migrieren. Die betroffenen Bereiche sind diejenigen, die von der `media.mediaTimed` Nutzung abhängen, und sie sollten wie in den folgenden Abschnitten beschrieben migriert werden.

### Customer Journey Analytics**

Es gibt zwei Möglichkeiten, CJA-Berichte zu migrieren:

>[!NOTE]
>
>Nachdem Sie eine der folgenden Optionen ausgewählt haben, müssen Sie jedes in Customer Journey Analytics-Berichten verwendete `media.mediaTimed` manuell durch das entsprechende abgeleitete Feld oder den entsprechenden XDM-Feldpfad für die Berichterstellung ersetzen.

* **Aufbewahren historischer Daten**: Adobe-Teams haben eine vordefinierte Customer Journey Analytics-Vorlage entwickelt, mit der ein Satz abgeleiteter Felder eingeführt wird, die die alten und neuen XDM-Felder in einem einzigen Feld kombinieren. Diese Vorlage kann auf Anfrage pro Customer Journey Analytics-Verbindung aktiviert werden. Wenden Sie sich an das Adobe-Supportteam , um die neuen Felder zu aktivieren. Diese abgeleiteten Felder werden nicht auf die Anzahl der abgeleiteten Felder in Ihrem Unternehmen angerechnet.

  Eine Liste der Zuordnungen finden Sie unter [Media Analytics-Parameterzuordnung für Adobe Experience Platform und Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Wenn keine historischen Daten erforderlich sind**: Es ist ausreichend, den XDM-Feldpfad für Berichterstellung zum Zeitpunkt der Berichterstellung zu verwenden. Weitere Informationen finden Sie unter [Migrieren von Customer Journey Analytics zur Verwendung der neuen Felder für Streaming-Medien](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Alle Zielgruppen und Profile müssen auf `mediaReporting` basieren. Weitere Informationen finden Sie unter [Migrieren von Profilen in die neuen Felder für Streaming-Medien](/help/use-cases/xdm-updates/migrate-profiles.md).

### Datenstrom und Datenerfassung

Dynamische Konfigurationen und Datenzuordnung müssen `mediaReporting` verwenden. Weitere Informationen finden Sie unter [Migrieren der Datenvorbereitung für benutzerdefinierte Felder in die neuen Felder für Streaming-Medien](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Andere Services, die migriert werden müssen

* Adobe Journey Optimizer: Kampagnen- und Journey-Konfigurationen müssen `mediaReporting` enthalten.

* Ereignisweiterleitung: In -Konfigurationen sollten nur `mediaReporting` Felder enthalten sein.

* Abfrage-Services: Abfragen müssen auf `mediaReporting` Felder verweisen.

* Tags-Konfigurationen: Alle Tagging-Setups sollten auf `mediaReporting` Felder verweisen.

* Verbindungen und Ziele: Datenflüsse im Import und Export sollten um `mediaReporting` Felder herum strukturiert sein.

Beachten Sie, dass jeder andere Fluss, der sich auf `media.mediaTimed` Felder stützt, betroffen ist und logische Aktualisierungen erfordert.

## Nächste Schritte und Support

Alle Kunden, die die Adobe-Datenerfassung für Streaming-Medien verwenden, müssen ihre Migrationen innerhalb des vorgesehenen Übergangszeitraums abschließen.

Bei Fragen oder Support-Anfragen wenden Sie sich bitte an das Adobe Support-Team.

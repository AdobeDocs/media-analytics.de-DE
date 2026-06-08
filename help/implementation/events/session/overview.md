---
title: Tracking von Inhaltswiedergabe
description: Erfahren Sie mehr über das Tracking der Core-Wiedergabe, einschließlich des Trackings der Medienladung, des Medienstarts, der Medienpause und des Medienabschlusses.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 807
ht-degree: 3%

---


# Tracking von Inhaltswiedergabe

Core-Wiedergabe-Tracking umfasst das Laden, Starten, Pause, Fortsetzen, Abschließen und Sitzungsende von Medien. Die Pufferung und das Suchen-Tracking sind zwar nicht obligatorisch, sind aber auch Kernkomponenten einer vollständigen Wiedergabeimplementierung.

## Player-Ereignisse

| Player-Ereignis | Aktion |
| --- | --- |
| Medienladevorgang | Medienobjekt erstellen; SessionStart aufrufen |
| Medienstart | Rufumschaltung |
| Anhalten | PauseStart aufrufen |
| Aus Pause fortsetzen | Rufumschaltung |
| Medien abgeschlossen | Sitzung beendet |
| Medienabbruch/Entladen | Sitzung beenden |
| Pufferung beginnt | AnrufpufferStart |
| Puffer endet | Wiedergabe aufrufen (Fortsetzen) |
| Suchen beginnt | Suchstart aufrufen |
| Suchende | Rufen Sie SeekComplete auf, und rufen Sie dann Play auf |

## Implementierungsschritte

1. **Ermitteln Sie, wann der Benutzer die Wiedergabe** hat (der Benutzer klickt auf Wiedergabe oder die automatische Wiedergabe löst aus). Erstellen Sie ein Medienobjekt mit Inhaltsname, ID, Länge, Stream-Typ und Medientyp. Siehe [Inhaltsname](/help/implementation/variables/core/content-name.md), [Inhalts-ID](/help/implementation/variables/core/content-id.md), [Inhaltslänge](/help/implementation/variables/core/content-length.md), [Stream-Typ](/help/implementation/variables/core/stream-type.md) und [Content-Typ](/help/implementation/variables/core/content-type.md) für Felddefinitionen.
1. **Optional Metadaten anhängen**: Standardmetadaten (Sendung, Staffel, Folge usw.) und benutzerdefinierte Kontextdatenvariablen. Siehe [Anzeigen](/help/implementation/variables/standard-metadata/show.md), [Staffel](/help/implementation/variables/standard-metadata/season.md), [Folge](/help/implementation/variables/standard-metadata/episode.md), [Genre](/help/implementation/variables/standard-metadata/genre.md) und [Netzwerk](/help/implementation/variables/standard-metadata/network.md) für Standard-Metadatenschlüsselverweise.
1. **Rufen Sie [Sitzungsstart](/help/implementation/events/session/session-start.md)** auf, um mit dem Tracking der Sitzung zu beginnen. Dadurch werden die Daten und Metadaten geladen und die QoS-Messung mit der Zeit bis zum Start gestartet. SessionStart verfolgt die *Absicht*, die wiedergegeben werden soll, nicht den ersten Frame.
1. **Rufen Sie [Play](/help/implementation/events/playback/play.md)** auf, wenn der erste Frame mit Inhalten auf dem Bildschirm gerendert wird.
1. **Rufen Sie [Start anhalten](/help/implementation/events/playback/pause-start.md)** auf, wenn der Player pausiert. Die Wiedergabe wird erneut aufgerufen, wenn die Wiedergabe fortgesetzt wird. Es gibt kein separates Wiederaufnahmeereignis.
1. **Aufrufen [Sitzung abgeschlossen](/help/implementation/events/session/session-complete.md)** wenn der Viewer das Ende des Inhalts erreicht.
1. **Aufruf [Sitzungsende](/help/implementation/events/session/session-end.md)** wenn der Player entladen wird oder der Viewer Inhalte abbricht, ohne das Ende zu erreichen. SessionEnd schließt die Sitzung sofort. Danach können keine weiteren Ereignisse mehr verfolgt werden.

>[!IMPORTANT]
>
>`SessionEnd` markiert das Ende einer Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende angeschaut wurde, rufen Sie `SessionComplete` vor dem `SessionEnd` auf. Alle anderen Tracking-Aufrufe werden nach der `SessionEnd` ignoriert, mit Ausnahme von `SessionStart` für eine neue Sitzung.

## Core-Wiedergabe

Die folgenden Beispiele zeigen einen vollständigen Sitzungsfluss vom Sitzungsbeginn bis zum Abschluss des Inhalts und zum Sitzungsende.

Implementierungsdetails nach Plattform finden Sie unter [Sitzungsstart](/help/implementation/events/session/session-start.md), [Play](/help/implementation/events/playback/play.md), [Start anhalten](/help/implementation/events/playback/pause-start.md), [Sitzung abgeschlossen](/help/implementation/events/session/session-complete.md) und [Sitzung beendet](/help/implementation/events/session/session-end.md).

## Pufferung

Der Puffer-Start signalisiert, dass der Player auf Daten wartet. Das Ende des Puffers wird abgeleitet, wenn Sie nach dem BufferStart ein Play-Ereignis senden (XDM-basierte APIs). Rufen Sie auf Mobile SDK auch BufferComplete explizit auf.

Details zur Implementierung finden Sie unter [Pufferstart](/help/implementation/events/playback/buffer-start.md).

## Wird gesucht

Suchstartsignale, die der Viewer bereinigt. Auf das Suchende folgt die Wiedergabe, um die Inhaltswiedergabe fortzusetzen.

Weitere Informationen zur Implementierung finden Sie unter [Start anhalten](/help/implementation/events/playback/pause-start.md) (Suchstart) und [Abspielen](/help/implementation/events/playback/play.md) (Suchende).

## Behandeln von App-Interrupts

Die Wiedergabe in einer Medienanwendung kann auf verschiedene Weise unterbrochen werden. Beispiele sind das Drücken der Pause-Taste durch den Benutzer, das Wechseln der App in den Hintergrund oder ein Telefonanruf. Unabhängig von der Ursache sind die Tracking-Anweisungen dieselben:

1. Rufen Sie **PauseStart** auf, wenn die Anwendung unterbrochen wird (geht in den Hintergrund, Medienpausen usw.).
1. Rufen Sie **Play** auf, wenn die Anwendung in den Vordergrund zurückkehrt und/oder die Medienwiedergabe fortgesetzt wird.

>[!NOTE]
>
>Rufen Sie SessionStart nicht auf, wenn die App aus dem Hintergrund zurückkehrt. Durch den Aufruf von SessionStart wird die Wiedergabe bis zu diesem Zeitpunkt nicht auf die gesamte Wiedergabezeit angerechnet, und frühere Fortschrittsmarken, Segmente und Kapitelgrenzen gehen verloren.

**Wann sollte eine angehaltene Sitzung enden?** Wenn die Anwendung keine Hintergrundwiedergabe zulässt, rufen Sie sofort PauseStart und anschließend SessionEnd nach etwa einer Minute im Hintergrund auf. Die Anwendung kann nicht weiterhin Pause-Pings aus dem Hintergrund senden, und das unbegrenzte Halten der Sitzung bietet ein schlechtes Erlebnis. Wenn die Anwendung die Hintergrundwiedergabe unterstützt (Audio-Apps, Video-Podcast-Apps), senden Sie im Hintergrund weiterhin Pings.

**Neustart nach einer langen Hintergrundperiode:** Wenn die App lange genug im Hintergrund war, dass die Sitzung abgelaufen ist (30-minütige Inaktivität), rufen Sie SessionEnd auf, um alle verbleibenden Sitzungen sauber zu schließen, und rufen Sie SessionStart auf, um eine neue Sitzung zu beginnen, wenn der Viewer zurückkehrt.

## Wiederaufnehmen von inaktiven Sitzungen

Eine Sitzung läuft automatisch ab, wenn für 10 Minuten keine Ereignisse empfangen werden oder wenn für 30 Minuten keine Abspielkopfbewegung stattfindet. Wenn der Benutzer nach Ablauf einer Sitzung zurückkehrt, rufen Sie SessionStart erneut auf, um eine neue Sitzung zu öffnen.

**Geräteübergreifende Wiederaufnahme (geräteübergreifende Weiterleitung):** Wenn ein Viewer die Wiedergabe zwischen Geräten überträgt (z. B. von einem Telefon auf ein Fernsehgerät), verwenden Sie das Wiederaufnahme-Flag, um die Sitzungen in Analytics-Berichten zusammenzufügen:

1. Rufen Sie auf dem **Quellgerät** SessionEnd auf, wenn der Viewer die Umwandlung initiiert. SessionComplete nicht aufrufen - der Inhalt ist nicht abgeschlossen.
1. Rufen Sie auf dem **Zielgerät** „SessionStart“ auf, wobei das Fortsetzungs-Flag auf &quot;`true`&quot; gesetzt ist, und übergeben Sie dieselben Inhaltsmetadaten und die Abspielposition vom Quellgerät.

Durch Festlegen des Fortsetzungs-Flags erhöht [&#x200B; Analytics für den zweiten Abschnitt der Übergabe &#x200B;](/help/reporting/metrics/content-resumes.md)Inhaltswiederaufnahmen[&#x200B; anstatt &#x200B;](/help/reporting/metrics/media-starts.md)Medienstarts“.

**Manuelles Wiederaufnehmen einer zuvor geschlossenen Sitzung:** Wenn die Anwendung Benutzerdaten speichert und eine zuvor geschlossene Sitzung fortsetzen kann, setzen Sie das Wiederaufnahme-Flag beim Sitzungsstart. Siehe [Sitzungsstart](/help/implementation/events/session/session-start.md#resuming-a-session) für Implementierungsdetails auf allen Plattformen.

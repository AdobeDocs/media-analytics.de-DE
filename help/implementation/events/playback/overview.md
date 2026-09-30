---
title: Tracking der Wiedergabe
description: Erfahren Sie mehr über Wiedergabeereignisse und wie Sie Wiedergabe-, Pause-, Puffer-, Ping- und Bitratenänderungs-Tracking implementieren.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
    internal-label: Variables
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
    internal-label: Events
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 2%
---

# Tracking der Wiedergabe

Wiedergabeereignisse verfolgen Statusübergänge im Media Player während einer Sitzung. Sie bilden den Kern des Ereignis-Streams und gelten für jeden Inhaltstyp.

## Player-Ereignisse

| Player-Ereignis | Aktion |
| --- | --- |
| Medienwiedergabe oder -wiederaufnahme | Rufumschaltung |
| Medienpausen | Anrufpause - Start |
| Pufferung beginnt | Start des Anrufpuffers |
| Puffer endet | Rufumschaltung |
| Änderungen der Bitrate | Änderung der Anrufbitrate |
| Timer-Feuer | Ruf-Ping |

## Implementierungsschritte

1. **Rufen Sie [Play](play.md)** nach [Sitzungsstart](../session/session-start.md) auf, wenn der erste Frame mit Inhalten auf dem Bildschirm gerendert wird. Senden Sie auch die Wiedergabe, wenn die Wiedergabe nach einer Pause oder einem Pufferstau fortgesetzt wird. Es gibt kein separates Wiederaufnahmeereignis.
1. **Aufruf [Start anhalten](pause-start.md)** wenn der Benutzer die Wiedergabe anhält. Wiedergabe senden, wenn Wiedergabe fortgesetzt wird.
1. **Rufen Sie [Pufferstart](buffer-start.md)** auf, wenn der Player auf Daten wartet. Bei XDM-basierten APIs wird auf ein Pufferende geschlossen, wenn Sie das nächste Play-Ereignis senden. Rufen Sie auf der mobilen SDK `BufferComplete` auch explizit auf, wenn die Pufferung aufgelöst wird.
1. **Rufen Sie [Ping](ping.md)** alle 10 Sekunden während der Wiedergabe des Hauptinhalts und alle 1 Sekunde während der Anzeigenwiedergabe auf. Ping hält die Sitzung am Leben und zeichnet Abspielkopfbewegungen auf. Mobile SDKs senden Pings automatisch. Alle anderen Plattformen müssen sie manuell senden.
1. **Rufen Sie [Bitratenänderung“ auf](bitrate-change.md)** wenn der Player eine neue Bitrate aushandelt. Schließen Sie die aktuellen QoE-Daten (Bitrate, Frames pro Sekunde, ausgelassene Frames) ein, damit das Backend [durchschnittliche Bitrate](/help/reporting/metrics/average-bitrate.md) und zugehörige Qualitätsmetriken berechnen kann.

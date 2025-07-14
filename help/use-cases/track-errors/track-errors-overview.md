---
title: Erläuterung von Tracking-Fehlern
description: Machen Sie sich mit dem Fehler-Tracking mit dem Media SDK vertraut.
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
exl-id: 61c5f835-d66c-4621-a0af-2e4f47a922ac
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 100%

---

# Überblick {#overview}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Implementieren des Fehler-Trackings

1. Tracking von Fehlern im Medienplayer.

   Rufen Sie bei Fehlerereignissen `trackError` mit den Fehlerinformationen auf.

>[!NOTE]
>
>Das Tracking von Fehlern im Medienplayer stoppt die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd` nach `trackError` auf.

---
title: Player-Statusverfolgungsbeispiele
description: Dieses Thema enthält Beispiele für die Player-Statusverfolgung.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Player-Statusverfolgungsbeispiele

Hinzufügen Beispiele


## Beispiel für lange Pause

Wenn eine Videositzung länger als 30 Minuten dauert, erfordert die API eine neue Sitzung. In diesem Fall sollte der Client eine neue Sitzungs-ID generieren. Für beide Videositzungen sollte der Client alle Status beibehalten, in denen sich ein Player befindet, und alle Informationen als `stateStart` Ereignis direkt nach dem `sessionStart` Aufruf senden.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Nach dem Senden des Videos `sessionEnd` muss eine neue Videositzung gestartet werden, und die ersten API-Ereignis lauten:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Das Beispiel für lange Pausen zeigt, dass der Player auch seine Status speichert, sodass sie an die neue Videositzung gesendet werden können.

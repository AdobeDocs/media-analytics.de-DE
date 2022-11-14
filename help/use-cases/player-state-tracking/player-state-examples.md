---
title: Beispiele für Player-Status-Tracking
description: Dieses Kapitel enthält Beispiele für das Player-Status-Tracking.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 100%

---

# Beispiele für Player-Status-Tracking


## Beispiel für lange Pause

Wenn eine Videositzung eine Pause hat, die länger als 30 Minuten dauert, fordert die API eine neue Sitzung an. In diesem Fall sollte der Client eine neue Sitzungs-ID generieren. Für beide Videositzungen sollte der Client alle Status beibehalten, in denen sich ein Player befindet, und alle Informationen als ein `stateStart`-Ereignis direkt nach dem `sessionStart`-Aufruf senden.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Nach dem Senden von `sessionEnd` muss eine neue Videositzung gestartet werden, und die ersten API-Ereignisse lauten:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Das Beispiel einer langen Pausen zeigt, dass auch der Player seine Status speichert, sodass sie an die neue Videositzung gesendet werden können.

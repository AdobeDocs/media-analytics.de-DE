---
title: Beispiele für Player-Status-Tracking
description: Dieses Kapitel enthält Beispiele für das Player-Status-Tracking.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Beispiele für Player-Status-Tracking


## Beispiel für lange Pause

Wenn eine Videositzung eine Pause hat, die länger als 30 Minuten dauert, fordert die API eine neue Sitzung an. In diesem Fall sollte der Client eine neue Sitzungs-ID generieren. Für beide Videositzungen sollte der Client alle Status beibehalten, in denen sich ein Player befindet, und alle Informationen als ein `stateStart`-Ereignis direkt nach dem `sessionStart`-Aufruf senden.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Nach dem Senden von `sessionEnd` muss eine neue Videositzung gestartet werden, und die ersten API-Ereignisse lauten:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Das Beispiel einer langen Pausen zeigt, dass auch der Player seine Status speichert, sodass sie an die neue Videositzung gesendet werden können.

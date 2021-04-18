---
title: Steuern der Ereignisreihenfolge
description: Steuern der Ereignisreihenfolge
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# Steuern der Ereignisreihenfolge {#controlling-the-order-of-events}

Da es sich bei der Media Collection API um eine RESTful-API handelt und das Video-Tracking ein äußerst zeitabhängiger Vorgang ist, sollten Sie bei der Implementierung darauf achten, dass die Media Collection API-Tracking-Aufrufe in der richtigen Reihenfolge am Backend eingehen. Das Backend *versucht*, die Ereignisse in eine Warteschlange einzureihen und basierend auf dem Zeitstempel im Objekt `playerTime` neu zu ordnen. Dies funktioniert jedoch nur eingeschränkt. Aktuell kann die Neusortierung fehlschlagen, wenn die Verzögerung zwischen den in falscher Reihenfolge eingehenden Aufrufen mehr als eine Sekunde beträgt. Diese annehmbare Verzögerung wird möglicherweise in künftigen Updates optimiert und/oder kann vom Benutzer angepasst werden.

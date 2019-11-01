---
title: Steuern der Ereignisreihenfolge
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Steuern der Ereignisreihenfolge{#controlling-the-order-of-events}

Da die Media Collection-API RESTful ist und die Videoverfolgung eine hochgradig zeitabhängige Operation ist, könnte ein Implementor besorgt sein, wenn Media Collection-API-Verfolgungsaufrufe, die am Back-End eingehen, nicht ordnungsgemäß ausgeführt werden. Das Backend *versucht*, die Ereignisse in eine Warteschlange einzureihen und basierend auf dem Zeitstempel im Objekt `playerTime` neu zu ordnen. Dies funktioniert jedoch nur eingeschränkt. Aktuell kann die Neusortierung fehlschlagen, wenn die Verzögerung zwischen den in falscher Reihenfolge eingehenden Aufrufen mehr als eine Sekunde beträgt. Diese annehmbare Verzögerung wird möglicherweise in künftigen Updates optimiert und/oder kann vom Benutzer angepasst werden.

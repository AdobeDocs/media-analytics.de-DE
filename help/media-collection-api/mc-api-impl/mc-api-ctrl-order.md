---
seo-title: Steuern der Ereignisreihenfolge
title: Steuern der Ereignisreihenfolge
uuid: 007 fccc 6-be 72-4 b 79-826 d -588 c 957 ccf 15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Steuern der Ereignisreihenfolge{#controlling-the-order-of-events}

Da die Mediencollection-API restful ist und die Videoverfolgung ein sehr abhängiger Vorgang ist, könnte ein Implementor Bedenken bezüglich der Mediencollection-API-Tracking-Aufrufe haben, die am Ende der Bestellung auftraten. Das Backend *versucht*, die Ereignisse in eine Warteschlange einzureihen und basierend auf dem Zeitstempel im Objekt `playerTime` neu zu ordnen. Dies funktioniert jedoch nur eingeschränkt. Aktuell kann die Neusortierung fehlschlagen, wenn die Verzögerung zwischen den in falscher Reihenfolge eingehenden Aufrufen mehr als eine Sekunde beträgt. Diese annehmbare Verzögerung wird möglicherweise in künftigen Updates optimiert und/oder kann vom Benutzer angepasst werden.

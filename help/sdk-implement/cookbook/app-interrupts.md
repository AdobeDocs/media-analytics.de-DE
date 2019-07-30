---
seo-title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
uuid: 1 ccb 4507-bda 6-462 d-bf 67-e 22978 a 4 db 3 d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Behandlung von Anwendungsunterbrechungen während der Wiedergabe{#handling-application-interrupts-during-playback}

Die Wiedergabe in einer Medienanwendung kann auf verschiedene Arten unterbrochen werden: ein Benutzer explizit die Pause drückt oder wenn ein Benutzer die Anwendung in den Hintergrund legt. Unabhängig davon, was eine Unterbrechung der Medienwiedergabe verursacht, sind die Verfolgungsanweisungen gleich:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Dies führt dazu, dass die Wiedergabe bis zu diesem Punkt nicht für die Gesamtwiedergabezeit gezählt wird, zusammen mit früheren Fortschrittsmarkierungen, Segmenten usw. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## Häufige Fragen zur Behandlung von Anwendungsunterbrechungen: {#section_osf_xqs_h2b}

* _Wie lange sollte eine App im Hintergrund laufen, bevor die Sitzung beendet wird?_

   Wenn die Anwendung die Hintergrundwiedergabe erlaubt, kann das Tracking mit dem Aufruf unserer APIs fortgesetzt werden. Wir werden dann alle unsere regulären Verfolgungspings senden. Nicht viele Video-Apps ermöglichen die Hintergrundwiedergabe mit Ausnahme von youtube Rot. Alle Audioapps ermöglichen dies jedoch. Wenn die Anwendung keine Hintergrundwiedergabe zulässt, wird empfohlen, im Pausierungsstatus für eine Minute zu bleiben und die Verfolgungssitzung zu beenden. Die Anwendung kann die Pausenpings nicht weiter senden, da in den meisten Fällen nicht feststellen kann, ob der Benutzer erneut zum Anzeigen des Mediums zurückkehrt oder wann er zu Tode kommt. Es ist auch ein schlechtes Erlebnis, wenn Pings im Hintergrund versendet werden.

* _Welches ist der richtige Weg für einen Tracking-Neustart, wenn die App längere Zeit im Hintergrund war?_

   Die Anwendung sollte `trackSessionEnd` aufrufen, um die Tracking-Sitzung zu beenden. Ab Version 2.1 sendet das SDK ein „Ende“-Ping, um das Backend darüber zu informieren, dass die Tracking-Sitzung geschlossen wurde.

* _Wie sieht es mit einem Neustart der gleichen Sitzung aus?_

   Detaillierte Anweisungen zum Neustart einer Tracking-Sitzung finden Sie auf dieser Seite: [Fortsetzen inaktiver Sitzungen.](/help/sdk-implement/cookbook/resuming-inactive.md) Das SDK sendet ein „Fortsetzen“-Ping, um das Backend darüber zu informieren, dass der Anwender die Sitzung manuell fortsetzt.


---
seo-title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Behandlung von Anwendungsunterbrechungen während der Wiedergabe{#handling-application-interrupts-during-playback}

Die Wiedergabe in einer Medienanwendung kann auf verschiedene Arten unterbrochen werden: ein Benutzer explizit die Pause drückt oder die Anwendung in den Hintergrund setzt. Unabhängig davon, was eine Unterbrechung der Medienwiedergabe verursacht, gelten die folgenden Verfolgungsanweisungen:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Auf diese Weise wird die Wiedergabe bis zu diesem Punkt nicht in Bezug auf die Gesamtwiedergabezeit gezählt, sondern es gehen auch frühere Fortschrittsmarkierungen, Segmente usw. verloren. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## Häufige Fragen zur Behandlung von Anwendungsunterbrechungen: {#section_osf_xqs_h2b}

* _Wie lange sollte eine App im Hintergrund laufen, bevor die Sitzung beendet wird?_

   Wenn die Anwendung die Hintergrundwiedergabe erlaubt, kann das Tracking mit dem Aufruf unserer APIs fortgesetzt werden. Wir werden dann alle unsere regulären Verfolgungspings senden. Mit Ausnahme von YouTube Red sind nicht viele Video-Apps für die Hintergrundwiedergabe geeignet. Dies ist jedoch in allen Audio-Apps möglich. Wenn die Anwendung die Hintergrundwiedergabe nicht zulässt, sollten Sie eine Minute lang im Pausenstatus bleiben und dann die Verfolgungssitzung beenden. Die Anwendung kann nicht mit dem Senden von Pausen fortfahren, da sie in den meisten Fällen nicht feststellen kann, ob der Benutzer zurückkehren wird, um das Medium weiterhin anzuzeigen, oder feststellen kann, wann es getötet werden soll. Es ist auch ein schlechtes Erlebnis, wenn Pings im Hintergrund versendet werden.

* _Welches ist der richtige Weg für einen Tracking-Neustart, wenn die App längere Zeit im Hintergrund war?_

   Die Anwendung sollte `trackSessionEnd` aufrufen, um die Tracking-Sitzung zu beenden. Ab Version 2.1 sendet das SDK ein „Ende“-Ping, um das Backend darüber zu informieren, dass die Tracking-Sitzung geschlossen wurde.

* _Wie sieht es mit einem Neustart der gleichen Sitzung aus?_

   Detaillierte Anweisungen zum Neustart einer Tracking-Sitzung finden Sie auf dieser Seite: [Fortsetzen inaktiver Sitzungen.](/help/sdk-implement/cookbook/resuming-inactive.md) Das SDK sendet ein „Fortsetzen“-Ping, um das Backend darüber zu informieren, dass der Anwender die Sitzung manuell fortsetzt.


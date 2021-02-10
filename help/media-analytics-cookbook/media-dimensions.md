---
title: Was ist Media Stream Attribution?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
translation-type: ht
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---


# Medien-Stream-Zuordnung

Mit dieser Funktion können Sie Anwendungsaktionen mit Medien-Tracking-Daten verknüpfen, ohne dass zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen erforderlich sind.

## Mediendimensionen außerhalb des Media-Trackings

Mit der Medien-Stream-Zuordnung können Kunden jetzt beliebige Mediendimensionen zu allen anderen Analytics-Aufrufen hinzufügen, wie z. B. Seitenansichten und benutzerdefinierten Links. Während der Implementierung müssen Sie den Tracking-Aufrufen für Analytics die Parameter für die Kontextdaten der Medien hinzufügen. Die vollständige Liste der für Medien verwendeten Kontextdatenparameter finden Sie hier: [Audio- und Videoparameter.](/help/metrics-and-metadata/audio-video-parameters.md)

Außerdem müssen Sie die Konfiguration für das Medien-Tracking für jeden Bericht, für den Sie diese Funktion aktivieren möchten, über die Admin-Konsole erneut aktivieren.

>[!NOTE]
>
>Die Medienmetriken stehen _nicht_ zur Verwendung außerhalb des Medien-Trackings zur Verfügung, da die meisten dieser Metriken von Media Analytics anhand von Heartbeat-Ereignissen berechnet werden. Außerdem ist es wichtig, dass die Medienmetriken nicht durch verschiedene Implementierungen in die Höhe getrieben werden.

## Schritte

Im folgenden JavaScript-Beispiel wird ein Tracking-Aufruf für einen benutzerdefinierten Link erstellt, bei dem der Name auf „Hero Banner“ eingestellt ist.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In der Analytics-Berichterstellung können Sie die `Show`-eVar verwenden, um die Daten aufzuschlüsseln. Außerdem können Sie die Instanzen des Link-Trackings zählen. Die Berichterstellung sieht in etwa wie folgt aus:

![](/assets/myShow-rpt-1.png)

## Nutzungsszenarios

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

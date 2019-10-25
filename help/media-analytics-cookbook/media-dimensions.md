---
title: Mediendimensionen außerhalb der Medienverfolgung
seo-title: Mediendimensionen außerhalb der Medienverfolgung
translation-type: tm+mt
source-git-commit: 5d20df537cd244a10f6c2e66cea622e98aa17a16

---


# Mediendimensionen außerhalb der Medienverfolgung

Mit dieser Funktion können Sie Anwendungsaktionen mit Medienverfolgungsdaten verknüpfen, ohne dass zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen erforderlich sind.

Kunden können jetzt alle Mediendimensionen zu allen anderen Analytics-Aufrufen hinzufügen, z. B. Seitenansichten und benutzerspezifische Links. Während der Implementierung müssen Sie die Parameter für Medienkontextdaten zu den Analytics-Verfolgungsaufrufen hinzufügen. Die vollständige Liste der für Medien verwendeten Kontextdatenparameter finden Sie hier: Parameter [für Audio und Video.](/help/metrics-and-metadata/audio-video-parameters.md)

Außerdem müssen Sie die Medienverfolgungskonfiguration für jeden Bericht, für den Sie diese Funktion aktivieren möchten, über die Admin-Konsole erneut aktivieren.

>[!NOTE]
>Die Medienmetriken stehen _nicht_ zur Verwendung außerhalb der Medienverfolgung zur Verfügung, da die meisten dieser Metriken von Media Analytics berechnet werden
>basierend auf Heartbeat-Ereignissen. Außerdem ist es wichtig, dass die Medienmetriken nicht durch verschiedene Implementierungen in die Höhe getrieben werden.

## Schritte

Im folgenden JavaScript-Beispiel wird ein benutzerspezifischer Link-Verfolgungsaufruf generiert, bei dem der Name auf "Hero Banner"eingestellt ist.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In der Analytics-Berichterstellung können Sie die `Show` eVar verwenden, um die Daten aufzuschlüsseln, und Sie können die Instanzen von Nachverfolgungslinks zählen. Die Berichte sehen ähnlich aus:

![](/assets/myShow-rpt-1.png)

## Nutzungsszenarios

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

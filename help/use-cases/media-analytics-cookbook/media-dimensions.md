---
title: Was ist Media Stream Attribution?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 88%

---

# Media Stream-Zuordnung {#media-stream-attribution}

Mit Media Stream-Zuordnung können Sie Anwendungsaktionen mit Medien-Tracking-Daten verknüpfen, ohne dass zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen erforderlich sind.

## Mediendimensionen außerhalb des Medien-Trackings

Sie können Analysedaten wie Seitenaufrufe und benutzerdefinierte Links um Mediendimensionen ergänzen. Während der Implementierung müssen Sie den Tracking-Aufrufen für Analytics die Parameter für die Kontextdaten der Medien hinzufügen. Eine vollständige Liste der verfügbaren Kontextdatenparameter für Medien finden Sie unter [Audio- und Videoparameter.](/help/implementation/variables/audio-video-parameters.md)

Um diese Funktion für einen bestimmten Bericht zu aktivieren, aktivieren Sie die Konfiguration des Medien-Trackings in der Admin Console erneut.

>[!NOTE]
>
>Die Medienmetriken sind _nicht_ für die Verwendung außerhalb des Medien-Trackings verfügbar, da die meisten von ihnen von der Streaming-Mediensammlung auf der Grundlage von Heartbeat-Ereignissen berechnet werden. Außerdem ist es wichtig, dass die Medienmetriken nicht durch verschiedene Implementierungen in die Höhe getrieben werden.

## Verwenden von Media Stream-Zuordnung

Das nachstehende JavaScript-Beispiel generiert einen benutzerdefinierten Link-Tracking-Aufruf, dessen Name auf „Hero Banner“ festgelegt ist.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In der Analytics-Berichterstellung können Sie die `Show`-eVar verwenden, um die Daten aufzuschlüsseln. Außerdem können Sie die Instanzen des Link-Trackings zählen. Die Berichterstellung sieht in etwa wie folgt aus:

![](/assets/myShow-rpt-1.png)

## Nutzungsszenarios

Die folgenden Beispiele zeigen Anwendungsfälle für Folgendes:

* Kategorieplatzierung
* Hero-Platzierung
* Interaktion
* Abonnements

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

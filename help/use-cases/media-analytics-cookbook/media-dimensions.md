---
title: Was ist Media Stream Attribution?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 41%

---

# Medien-Stream-Zuordnung {#media-stream-attribution}

Mit der Medien-Stream-Zuordnung können Sie Anwendungsaktionen mit Medien-Tracking-Daten verknüpfen, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen benötigen zu müssen.

## Mediendimensionen außerhalb des Media-Trackings

Sie können Mediendimensionen zu Analytics-Aufrufen wie Seitenansichten und benutzerspezifischen Links hinzufügen. Während der Implementierung müssen Sie den Tracking-Aufrufen für Analytics die Parameter für die Kontextdaten der Medien hinzufügen. Eine vollständige Liste der verfügbaren Kontextdatenparameter für Medien finden Sie unter [Audio- und Videoparameter.](/help/implementation/variables/audio-video-parameters.md)

Um diese Funktion für einen bestimmten Bericht zu aktivieren, aktivieren Sie die Konfiguration des Medien-Trackings in der Admin Console erneut.

>[!NOTE]
>
>Die Medienmetriken sind _not_ zur Verwendung außerhalb des Medien-Trackings verfügbar sind, da die meisten dieser Werte von Streaming Media Analytics basierend auf Heartbeat-Ereignissen berechnet werden. Außerdem ist es wichtig, dass die Medienmetriken nicht durch verschiedene Implementierungen in die Höhe getrieben werden.

## Verwenden der Medien-Stream-Zuordnung

Im folgenden JavaScript-Beispiel wird ein Tracking-Aufruf für benutzerspezifische Links generiert, bei dem der Name auf &quot;Hero Banner&quot;festgelegt ist.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In der Analytics-Berichterstellung können Sie die `Show`-eVar verwenden, um die Daten aufzuschlüsseln. Außerdem können Sie die Instanzen des Link-Trackings zählen. Die Berichterstellung sieht in etwa wie folgt aus:

![](/assets/myShow-rpt-1.png)

## Nutzungsszenarios

Die folgenden Beispiele zeigen Anwendungsfälle für Folgendes:

* Kategorieplatzierung
* Hero Placement
* Interaktion
* Abonnements

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

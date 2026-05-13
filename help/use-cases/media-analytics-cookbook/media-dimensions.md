---
title: Was ist Media Stream Attribution?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e4f5f438-eabb-4c54-9133-b817e3d125f5id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# Media Stream-Zuordnung {#media-stream-attribution}

Mit Media Stream-Zuordnung können Sie Anwendungsaktionen mit Medien-Tracking-Daten verknüpfen, ohne dass zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen erforderlich sind.

## Mediendimensionen außerhalb des Medien-Trackings

Sie können Analysedaten wie Seitenaufrufe und benutzerdefinierte Links um Mediendimensionen ergänzen. Während der Implementierung müssen Sie den Tracking-Aufrufen für Analytics die Parameter für die Kontextdaten der Medien hinzufügen.

Um diese Funktion für einen bestimmten Bericht zu aktivieren, aktivieren Sie die Konfiguration des Medien-Trackings in der Admin Console erneut.

>[!NOTE]
>
>Die Medienmetriken sind _nicht_ für die Verwendung außerhalb des Medien-Trackings verfügbar, da die meisten von ihnen von den Streaming-Mediendiensten auf der Grundlage von Heartbeat-Ereignissen berechnet werden. Außerdem ist es wichtig, dass die Medienmetriken nicht durch verschiedene Implementierungen in die Höhe getrieben werden.

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

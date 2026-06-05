---
title: Informationen zu den Voraussetzungen für Adobe Streaming Media Services
description: Erste Schritte mit den Services für Streaming-Medien. Erfahren Sie, was Sie für die Implementierung benötigen.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# Voraussetzungen {#prerequisites}

Bevor Sie mit der Implementierung von Adobe Streaming Media Services beginnen, führen Sie die folgenden Aufgaben aus:

1. **Bestätigen des Preismodells**<br>
Das aktuelle Preismodell für das Add-on Customer Journey Analytics Streaming Media Collection und das Add-on Adobe Analytics for Streaming Media basiert auf Video-Streams. Wenden Sie sich bei Bedarf an Ihren Kundenbetreuer oder Ihr Adobe-Account-Team, da das Add-on separat für Adobe Analytics und Adobe Experience Platform erhältlich ist.

1. **Adobe Analytics-Berichte aktivieren** *(Nur-Analytics-Implementierungen)*<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte aktivieren. Siehe [Einrichten von Berichten für reine Analytics-Implementierungen](/help/reporting/setup/analytics-reporting.md).

1. **Identität konfigurieren**<br>

   Die Anforderungen an die Identitätskonfiguration hängen von Ihrer Implementierungsmethode ab:

   * **Edge-Implementierungen**: Die Identität wird über die Adobe Experience Platform Identity-Namespace-Konfiguration gehandhabt. Es ist keine separate Identity Service-Einrichtung erforderlich. Detaillierte Informationen finden Sie unter Übersicht über ](/help/implementation/edge/overview.md) Implementierung von [Edge .

   * **Nur Analytics-Implementierungen**: Der Adobe Experience Platform Identity Service muss aktiviert sein, damit Besuchende konsistent über CX Enterprise-Lösungen hinweg identifiziert werden können. Der Identity Service weist jedem Site-Besucher eine eindeutige, beständige ID zu und ermöglicht die Freigabe dieser ID für alle abonnierten CX Enterprise-Lösungen.

     Weitere Informationen finden Sie in der Dokumentation zum [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

1. **Anzeigen von zusätzlichen Voraussetzungen für Ihre Implementierungsmethode**

   Je nachdem, wie Sie Streaming-Medien-Services implementieren möchten, sehen Sie sich die Voraussetzungen für eine der folgenden Implementierungsmethoden an:

   * [Nur Analytics-Implementierung - Übersicht](/help/implementation/analytics-only/overview.md)

   * [Übersicht über die Edge-Implementierung](/help/implementation/edge/overview.md)

   Verwenden Sie den [Implementierungsüberblick](/help/implementation/overview.md), um zu bestimmen, welche Implementierungsmethode für Sie geeignet ist.

---
title: Was ist die Adobe Audience Manager-Aktivierung?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Audience Manager-Aktivierung{#audience-manager-enablement}

Adobe Audience Manager (AAM) ist eine Data Management Platform (DMP), die Ihnen hilft, Ihre Zielgruppen-Assets zu kombinieren. So können Sie ganz einfach geschäftlich relevante Informationen über Site-Besucher sammeln, vermarktbare Segmente erstellen und spezifische Werbung und Inhalte für die richtige Zielgruppe bereitstellen.

Mit AAM sind Sie nicht an eine Datenverkaufs-, Datenaustausch- oder Nachfrage-Plattform gebunden. Darüber hinaus ist AAM vollkommen unabhängig, wenn es um die Datenbestände Ihrer Partner geht. Dank des Zugriffs auf verschiedene Datenquellen bietet AAM digitalen Publishern die Möglichkeit, neben unserer privaten Datenkooperation verschiedenste Drittanbieterdaten zu verwenden. Weitere Informationen zu AAM finden Sie in der AAM-Dokumentation der [Audience Manager-Produktdokumentation](https://docs.adobe.com/content/help/de-DE/experience-cloud/user-guides/home.html).

**VA-Datenübertragung an AAM -** Sowohl bei Videoinhalten als auch bei Videoanzeigen können die Metriken und Metadaten, die mit (reservierten) Lösungsvariablen erfasst werden, automatisch an AAM gesendet werden. Die Datenübertragung ist auf allen Plattformen verfügbar, einschließlich Desktop, Mobile und OTT. Um diese Server-seitige Datenübertragung zu aktivieren, müssen Sie sich an den Adobe-Kundendienst wenden und die Aktivierung dieses Feeds beantragen.

>[!IMPORTANT]
>
>Um die reibungslose Übertragung der Daten an AAM zu gewährleisten, sollten Sie die neuesten Versionen der Media SDK-Bibliotheken verwenden.

Federated Data unterstützt die Datenweitergabe an AAM vollständig. Wenden Sie sich an Ihr Adobe-Team, um die Einstellungen für Federated Data zu prüfen.

## OTT-/AAM-Methoden {#ott-aam-methods}

Sie können diese Methoden verwenden, um Signale zu senden und Besuchersegmente von Audience Manager abzurufen:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn noch kein Signal gesendet wurde.

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn noch kein Signal gesendet wurde.

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  Gibt die aktuelle DPUUID zurück.

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  Legt die DPID und die DPUUID fest. Wenn DPID und DPUUID festgelegt sind, werden sie mit jedem Signal gesendet.

  ```js
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  Sendet ein Signal mit Eigenschaften an das Zielgruppen-Management.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
  ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

  Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn noch kein Signal gesendet wurde.

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn noch kein Signal gesendet wurde.

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  Gibt die aktuelle DPUUID zurück.

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  Legt die DPID und die DPUUID fest. Wenn DPID und DPUUID festgelegt sind, werden sie mit jedem Signal gesendet.

  ```js
  ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
  ```

* `audienceSubmitSignal -`

  Sendet ein Signal mit Eigenschaften an das Zielgruppen-Management.

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```

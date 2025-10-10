---
title: Was ist die Adobe Audience Manager-Aktivierung?
description: Erfahren Sie, wie Sie Programmaktionen mit Medien-Tracking-Daten verknüpfen können, ohne zusätzliche Verarbeitungsregeln und benutzerdefinierte Variablen zu benötigen.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Audience Manager-Aktivierung {#audience-manager-enablement}

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

---
seo-title: Audience Manager-Aktivierung
title: Audience Manager-Aktivierung
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Audience Manager-Aktivierung{#audience-manager-enablement}

Mit Adobe Audience Manager (AAM), einer Daten-Management-Plattform (DMP), können Sie Ihre verschiedenen Assets mit Zielgruppendaten zusammenführen, um so die Erfassung geschäftlich relevanter Zahlen zu Site-Besuchern zu vereinfachen, marktfähige Segmente zu erstellen und dem richtigen Publikum gezielte Werbeanzeigen und Inhalte bereitzustellen.

Mit AAM sind Sie nicht an einen Datenanbieter, eine Datenaustauschplattform oder eine Demand Side Platform gebunden. Darüber hinaus ist AAM mit allen Daten-Assets Ihrer Partner kompatibel. Dank des Zugriffs auf verschiedene Datenquellen bietet AAM digitalen Publishern die Möglichkeit, neben unserer privaten Datenkooperation verschiedenste Drittanbieterdaten zu verwenden. Weitere Informationen zu AAM finden Sie in der Produktdokumentation zu AAM [Audience Manager.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Datenübertragung von VA nach AAM:** Sowohl bei Videoinhalten als auch bei -anzeigen können die Metriken und Metadaten, die mit (reservierten) Lösungsvariablen erfasst werden, automatisch an AAM gesendet werden. Die Datenübertragung ist auf allen Plattformen verfügbar, einschließlich Desktop, Mobile und OTT. Um die serverseitige Datenübertragung zu aktivieren, müssen Sie dies beim Adobe-Kundendienst anfordern.

>[!IMPORTANT]
>
>Um eine reibungslose Übertragung der Daten auf AAM sicherzustellen, sollten Sie sich auf die neuesten Versionen der Media SDK-Bibliotheken einstellen.

Federated Data unterstützt die Datenweitergabe an AAM vollständig. Arbeiten Sie mit Ihrem Adobe-Team zusammen, um die Federated Data-Einstellungen zu bestätigen.

## OTT-/AAM-Methoden {#ott-aam-methods}

Sie können diese Methoden verwenden, um Signale zu senden und Besuchersegmente von Audience Manager abzurufen:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn bisher kein Signal eingegangen ist.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn bisher kein Signal eingegangen ist.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Gibt die aktuelle DPUUID zurück.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Legt die DPID und die DPUUID fest. Wenn die DPID und die DPUUID festgelegt sind, werden sie mit jedem Signal gesendet.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Sendet ein Signal mit Eigenschaften an das Zielgruppen-Management.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn bisher kein Signal eingegangen ist.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Gibt das zuletzt erfasste Besucherprofil zurück. Gibt ein leeres Objekt zurück, wenn bisher kein Signal eingegangen ist.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Gibt die aktuelle DPUUID zurück.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Legt die DPID und die DPUUID fest. Wenn die DPID und die DPUUID festgelegt sind, werden sie mit jedem Signal gesendet.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Sendet ein Signal mit Eigenschaften an das Zielgruppen-Management.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```


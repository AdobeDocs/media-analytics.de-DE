---
title: Festlegen von Benutzer-IDs
description: APIs zum Festlegen von Benutzer-IDs, die als eindeutige Kundenkennungen dienen.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: '"Media Analytics, API"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 94%

---

# Anwender-IDs festlegen{#set-user-ids}

Die Anwender-ID ist eine eindeutige anwenderspezifische Besucherkennung, die von der Anwendung für einen Anwender definiert wird.

Legen Sie die eindeutige Benutzer-ID im ADBMobile-SDK wie folgt fest und rufen Sie sie ab:

* **Legen Sie:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Abrufen:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```

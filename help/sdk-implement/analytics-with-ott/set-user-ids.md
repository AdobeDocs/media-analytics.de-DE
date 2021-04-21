---
title: Anwender-IDs festlegen
description: APIs zum Festlegen von Benutzer-IDs, die als eindeutige Kundenkennungen dienen.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '53'
ht-degree: 100%

---

# Anwender-IDs festlegen {#set-user-ids}

Die Anwender-ID ist eine eindeutige anwenderspezifische Besucherkennung, die von der Anwendung für einen Anwender definiert wird.

Legen Sie die eindeutige Unique User-ID im ADBMobile-SDK wie folgt fest und rufen Sie sie ab:

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

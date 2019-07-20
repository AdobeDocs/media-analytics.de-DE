---
seo-title: Anwender-IDs festlegen
title: Anwender-IDs festlegen
uuid: fdd 54 fec -79 cd -4 bf 8-b 17 e -4 d 61 d 84 f 6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Anwender-IDs festlegen{#set-user-ids}

Die Anwender-ID ist eine eindeutige anwenderspezifische Besucherkennung, die von der Anwendung für einen Anwender definiert wird.

Legen Sie die eindeutige Unique User-ID im ADBMobile-SDK wie folgt fest und rufen Sie sie ab:

* **Festlegen:**

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

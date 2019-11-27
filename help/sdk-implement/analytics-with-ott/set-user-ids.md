---
title: Anwender-IDs festlegen
description: APIs zum Festlegen von Benutzer-IDs, die als eindeutige Kundenkennungen dienen.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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

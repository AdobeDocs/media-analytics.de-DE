---
title: Festlegen von Benutzer-IDs
description: APIs zum Festlegen von Benutzer-IDs, die als Kennungen für Unique Customers dienen.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 69%

---

# Festlegen von Benutzer-IDs {#set-user-ids}

Die Benutzer-ID ist eine eindeutige benutzerdefinierte Besucherkennung, die von der Anwendung für einen Benutzer definiert wird.

Legen Sie die ID für Unique Visitors im ADBMobile-SDK wie folgt fest und rufen Sie sie ab:

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

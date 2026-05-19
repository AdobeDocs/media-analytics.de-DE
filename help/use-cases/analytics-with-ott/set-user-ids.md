---
title: Festlegen von Benutzer-IDs
description: APIs zum Festlegen von Benutzer-IDs, die als Kennungen für Unique Customers dienen.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: Streaming Media, API
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/AG7KGMEVhpDbGzHKhb94KF8QHzDTw-y1kdkklOdWCFI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 53
ht-degree: 69%

---

# Festlegen von Benutzer-IDs{#set-user-ids}

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

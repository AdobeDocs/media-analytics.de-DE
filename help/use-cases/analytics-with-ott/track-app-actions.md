---
title: App-Aktionen verfolgen
description: App-Aktionen sind die Ereignisse in der App, die Sie messen möchten.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 100%

---

# App-Aktionen verfolgen{#track-app-actions}

Aktionen sind die Ereignisse in Ihrer App, die Sie messen möchten.

Jede Aktion weist mindestens eine zugehörige Metrik auf, die bei jedem Vorkommen des Ereignisses erhöht wird. So könnten Sie z. B. einen `trackAction`-Aufruf für jedes neue Abonnement, jede Inhaltsbewertung oder jeden Abschluss einer Ebene senden.

Aktionen werden nicht automatisch verfolgt. Rufen Sie also `trackAction` auf, wenn ein zu verfolgendes Ereignis auftritt, und ordnen Sie die Aktion dann einem anwenderspezifischen Ereignis zu.

1. Wenn ein Ereignis auftritt, das Sie verfolgen möchten, rufen Sie `trackAction` auf.

   * **Roku:**

     ```js
     ADBMobile().trackAction("myapp.ActionName", {})
     ```

   * **Chromecast:**

     ```js
     ADBMobile.analytics.trackAction("myapp.ActionName", {});
     ```

1. Ordnen Sie die Aktion einem anwenderspezifischen Ereignis zu.

   * **Roku:**

     ```js
     dictionary = {} 
     dictionary["myapp.social.SocialSource"] = "Twitter"  
     ADBMobile().trackAction("myapp.SocialShare", dictionary)
     ```

   * **Chromecast:**

     ```js
     var dictionary = {}; 
     dictionary["myapp.social.SocialSource"] = "Twitter"; 
     ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
     ```

Sie können auch zusätzliche Kontextdaten mit jedem trackAction-Aufruf senden.

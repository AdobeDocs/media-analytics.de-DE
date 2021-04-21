---
title: App-Aktionen verfolgen
description: App-Aktionen sind die Ereignisse in der App, die Sie messen möchten.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '132'
ht-degree: 100%

---

# App-Aktionen verfolgen {#track-app-actions}

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

---
seo-title: App-Aktionen verfolgen
title: App-Aktionen verfolgen
uuid: 9 cdc 048 a -419 a -4725-bd 61-6 ca 6 d 009 cf 10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# App-Aktionen verfolgen{#track-app-actions}

Aktionen sind die Ereignisse in der App, die Sie messen möchten.

Jede Aktion weist mindestens eine zugehörige Metrik auf, die bei jedem Vorkommen des Ereignisses erhöht wird. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

Aktionen werden nicht automatisch verfolgt. Rufen Sie also `trackAction` auf, wenn ein zu verfolgendes Ereignis auftritt, und ordnen Sie die Aktion dann einem anwenderspezifischen Ereignis zu.

1. When an event that you want to track occurs, call `trackAction`.

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


---
seo-title: App-Zustände verfolgen
title: App-Zustände verfolgen
uuid: 2 f 98 fb 43-c 362-4 a 9 b -8732-fa 7 e 963 da 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# App-Zustände verfolgen{#track-app-states}

Zustände sind die verschiedenen Bildschirme oder Ansichten in der Anwendung. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. Status werden für gewöhnlich mithilfe eines Pfadsetzungsberichts angezeigt. Auf diese Weise können Sie sehen, wie Anwender in Ihrer App navigieren und welche Status am häufigsten angezeigt werden.

## trackState-Aufrufe

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In anderen Analytics-Schnittstellen wird "View State" als" Seitenname" gemeldet. " Statusansichten" wird als "Seitenansichten" gemeldet.

## Kontextdaten senden

Zusätzlich zu "State Name" können Sie zusätzliche Kontextdaten mit jedem Verfolgungsstatus-Aufruf senden.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>Die Kontextdatenwerte müssen benutzerdefinierten Variablen in Adobe Mobile Services zugeordnet werden.


---
seo-title: App-Zustände verfolgen
title: App-Zustände verfolgen
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# App-Zustände verfolgen{#track-app-states}

Zustände sind die verschiedenen Bildschirme oder Ansichten in der Anwendung. Jedes Mal, wenn in Ihrer Anwendung ein neuer Status angezeigt wird, sollten Sie einen `trackState` Aufruf senden. Wenn ein Benutzer beispielsweise von der Startseite zum Videodetailbildschirm navigiert, senden Sie einen `trackState` Aufruf. Status werden für gewöhnlich mithilfe eines Pfadsetzungsberichts angezeigt. Auf diese Weise können Sie sehen, wie Anwender in Ihrer App navigieren und welche Status am häufigsten angezeigt werden.

## trackState-Aufrufe

Normalerweise rufen Sie `trackState` jedes Mal, wenn die App einen neuen Bildschirm lädt, an.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In anderen Analytics-Schnittstellen wird "Anzeigestatus"als "Seitenname"gemeldet. "Statusansichten"wird als "Seitenansichten"gemeldet.

## Kontextdaten senden

Neben "Statusname"können Sie bei jedem Verfolgungsstatusaufruf zusätzliche Kontextdaten senden.

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


---
title: App-Zustände verfolgen
description: 'App-Status sind die verschiedenen Bildschirme oder Ansichten in Ihrer App, deren Anzeige zu einem trackState-Aufruf führen sollte. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# App-Zustände verfolgen {#track-app-states}

Zustände sind die verschiedenen Bildschirme oder Ansichten in der Anwendung. Jedes Mal, wenn in Ihrer App ein neuer Status angezeigt wird, sollten Sie einen `trackState`-Aufruf senden. Wenn ein Benutzer beispielsweise von der Startseite zum Videodetailbildschirm navigiert, senden Sie einen `trackState`-Aufruf. Status werden für gewöhnlich mithilfe eines Pfadsetzungsberichts angezeigt. Auf diese Weise können Sie sehen, wie Anwender in Ihrer App navigieren und welche Status am häufigsten angezeigt werden.

## trackState-Aufrufe

Normalerweise rufen Sie `trackState` jedes Mal auf, wenn die App einen neuen Bildschirm lädt.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

Der Statusname wird dann in der Variablen „Status anzeigen“ in Adobe Mobile Services gemeldet und für jeden `trackState`-Aufruf wird eine Ansicht aufgezeichnet. In anderen Analytics-Oberflächen wird „Status anzeigen“ als „Seitenname“ und „Statusansichten“ als „Seitenansichten“ gemeldet.

## Senden der Kontextdaten

Zusätzlich zum „Statusnamen“ können Sie mit jedem track state-Aufruf zusätzliche Kontextdaten senden.

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


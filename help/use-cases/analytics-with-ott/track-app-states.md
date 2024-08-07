---
title: App-Zustände verfolgen
description: Programmstatus sind die verschiedenen Bildschirme oder Ansichten in Ihrem Programm. Erfahren Sie, wie Sie den Programmstatus in Ihrem Programm mithilfe des trackState-Aufrufs verfolgen.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%

---

# App-Zustände verfolgen{#track-app-states}

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

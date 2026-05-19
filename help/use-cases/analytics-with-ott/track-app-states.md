---
title: App-Zustände verfolgen
description: Programmstatus sind die verschiedenen Bildschirme oder Ansichten in Ihrem Programm. Erfahren Sie, wie Sie den Programmstatus in Ihrem Programm mithilfe des trackState-Aufrufs verfolgen.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
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
source-wordcount: 188
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

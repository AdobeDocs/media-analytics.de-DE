---
title: Aktivierung von Medienberichten
description: Erfahren Sie mehr über die Media Report Suite, die Medienmetriken erfasst.  Führen Sie diese Schritte aus, um Medienberichte zu konfigurieren, bevor Mediendaten gesendet werden.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
  - id: ef60b66e-5984-4336-ba72-6d978b1b6f87
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 945
ht-degree: 81%

---

# Aktivierung von Medienberichten{#media-reports-enablement}

Jede Report Suite, die Medienmetriken erfasst, muss konfiguriert werden, bevor Mediendaten gesendet werden.

Fortgeschrittene Kunden können die Medien-Bedienfelder in Analysis Workspace nur verwenden, wenn Media Core und das Tracking für [Erlebnisqualität](/help/use-cases/track-qos/track-qos-overview.md) aktiviert sind.

>[!TIP]
>
>Um neue Funktionen nutzen zu können, sollten Bestandskunden von Streaming-Medien das Medien-Tracking für ihre RSIDs wieder aktivieren.

1. Klicken Sie in [Reports &amp; Analytics](https://my.omniture.com/login/) auf **[!UICONTROL Admin > Report Suites].**
1. Wählen Sie die Report Suites aus, in denen Sie Mediendaten erfassen, und klicken Sie anschließend auf **[!UICONTROL Einstellungen bearbeiten > Medienmanagement > Medienberichte].**

   ![](assets/media-reporting.png)

1. Aktivieren Sie auf der Seite **[!UICONTROL Medienberichte]** die Option **[!UICONTROL Media-Core],** und aktivieren Sie optional **[!UICONTROL Medienanzeigen],** **[!UICONTROL Medienkapitel],** und **[!UICONTROL Medienqualität].**

   Die Medienmessung enthält folgende Module:

   * **Medien-Core**

     Die Core-Medienmessung wird für Medieninhalte verwendet. Dabei werden Lösungs- (oder benutzerdefinierte) eVars verwendet, um Inhalt, Inhaltstyp, Inhalts-Player-Name und Inhaltskanal zu verfolgen. Lösungs- (oder benutzerdefinierte) Ereignisse werden für Medienstarts, Inhaltsstarts, Inhaltsbeendigungen und Besuchszeit für Inhalt verwendet.

   * **Medienanzeigen**

     Die Medienanzeigenmessung wird für die Messung von Anzeigen im Medieninhalt verwendet. Dabei werden Lösungs-eVars verwendet, um Anzeige, Name des Anzeigenplayers, Anzeigen-Pod und Anzeigenposition innerhalb der Werbeunterbrechung zu messen. Lösungsereignisse werden für Anzeigenstarts, Anzeigenbeendigungen, Besuchszeit für Anzeigen und Besuchszeit für Videos verwendet.

   * **Medienkapitel**

     Die Medienkapitelmessung wird für die Messung von Kapiteln verwendet. Ein Kapitel ist eine Unterteilung von Inhalt in einem einzelnen Medium. Dabei wird ein Lösungs-eVar zum Speichern der Kapitel-ID verwendet. Lösungsereignisse werden für Kapitelstarts, Kapitelbeendigungen, und Besuchszeit für Kapitel verwendet. Zusätzliche Kapitelmetadaten des Kapitelnamens und der Kapitelposition werden als Klassifizierungen der Kapitel-ID bereitgestellt.

   * **Medienqualität**

     Anhand der Videoqualitätsmessung wird die Qualität der Inhaltswiedergabe gemessen. Dabei werden Lösungs-eVars verwendet, um Zeit bis Start, Pufferereignisse, Gesamtpufferdauer, die Bitratenwechsel, durchschnittliche Bitrate, Fehler und Dropped Frames zu speichern. Die Lösungsereignisse werden für Folgendes verwendet: Zeit bis zum Start, vor dem Start übersprungen, vom Puffer betroffene Streams, Pufferereignisse, gesamte Pufferdauer, von Bitratenänderungen betroffene Streams, Bitratenänderungen, mittlere Bitrate, von Fehlern betroffene Streams, Fehlerereignisse, von übersprungenen Bildern betroffene Streams und übersprungene Bilder.

   * **Video und Videoanzeigenmetadaten**

     An ein Medium oder an eine Anzeige können Metadaten angefügt werden, die eine weitere Beschreibung und Kategorisierung enthalten. Über Lösungsvariablen und Klassifizierungen werden standardisierte Medien- und Anzeigen-Metadaten erfasst. Mögliche Werte: Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Network, Show Type, Ad Loads, MVPD, Authorized, Day Part, Media Session ID, Advertiser, Campaign ID und Creative ID.

   * **Audio und Audio-Anzeigemetadaten**

     Metadaten können an Audio- und/oder Werbeanzeigen angehängt werden, um diese Audio-/Werbeanzeigen näher zu beschreiben und zu kategorisieren. Standardisierte Audio- und Anzeigenmetadaten werden über Lösungsvariablen und Klassifizierungen erfasst. Zu verwendende Werte: Interpret, Album, Label, Autor, Verleger, Sender, Sendung, Staffel, Folge, Asset-ID, Genre, Erstes Sendedatum, Erstes Digitaldatum, Inhaltsbewertung, Urheber, Sendungstyp, Anzeigenladevorgänge, Tagesteil, Mediensitzungs-ID, Werbekunde, Kampagnen-ID und Creative-ID.

   Durch die Aktivierung jedes Moduls wird ein Variablensatz reserviert und ein neuer Satz von Berichten erstellt. Mit Ausnahme der Qualitätsberichte enthalten Berichte keine Daten, es sei denn, die entsprechende Implementierung wurde durchgeführt. Bei Implementierung des Kernmoduls wird auch das Qualitätsmodul implementiert, wenn Sie es aktivieren.

   Wenn Sie noch keine Anzeigen-, Kapitel- oder Wiedergabequalität verfolgen, können Sie jederzeit weitere Optionen aktivieren.

1. Klicken Sie auf **[!UICONTROL Speichern].**

   Wenn diese Report Suite bereits zur Erfassung von Mediendaten konfiguriert ist, wird eine zusätzliche Konfigurationsseite angezeigt, nachdem Sie auf **[!UICONTROL Speichern]** klicken. Wenn die Seite **[!UICONTROL Media-Core-Messung]** angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

1. (Situationsabhängig) Legen Sie auf der Seite **[!UICONTROL Media-Core-Messung]** fest, ob Sie weiterhin benutzerdefinierte Variablen oder Lösungsvariablen verwenden möchten.

   | Option | Hinweise |
   | --- | --- |
   | Weiterhin benutzerspezifische Variablen verwenden | Vorteile und Nachteile:<ul> <li> **Vorteile**: Die Inhaltstrend-Erstellung funktioniert auch nach der Migration. </li> <li> **Nachteile:** Erfordert die Beibehaltung von zwei benutzerdefinierten eVars und drei benutzerdefinierten Ereignissen für Medien. Sie können ein einziges benutzerspezifisches eVar und ein einziges benutzerspezifisches Ereignis erneut verwenden. </li> </ul> Wenn Sie weiterhin benutzerspezifische Variablen verwenden möchten: <ol> <li>Wählen Sie **[!UICONTROL Benutzerdefinierte Variablen verwenden]** aus und klicken Sie auf **[!UICONTROL Speichern.]** </li> <li>Wenn Sie dazu aufgefordert werden, ordnen Sie die aktuellen benutzerdefinierten eVars und Ereignisse zu und klicken Sie auf **[!UICONTROL Speichern:]** </li> </ol> |
   | Zu Lösungsvariablen migrieren | Vorteile und Nachteile:<ul> <li> **Vorteile:** Sie können drei benutzerspezifische eVars und vier benutzerspezifische Ereignisse erneut verwenden. </li> <li> **Nachteile:** Sie verlieren **alle** historischen Trends und Vergleiche für Medienberichte. Das bedeutet, dass Sie keine Trendansicht für Inhaltsdaten oder Inhaltszeiten erstellen können, die vor der Migration zu Heartbeats wiedergegeben wurden. </li> </ul> **Einschränkung:** Migrieren Sie nur dann zu Lösungsvariablen, wenn Sie sicher sind, dass Sie diese Trends nicht beibehalten möchten. Alle Kunden sollten nur dann Lösungsvariablen verwenden und Mediendaten anhand von Verarbeitungsregeln an vorhandene Props und eVars übergeben, wenn sie den Verlauf beibehalten müssen. Um zu Lösungsvariablen zu migrieren, wählen Sie **[!UICONTROL Lösungsvariablen verwenden]** und klicken Sie auf **[!UICONTROL Speichern].** <br><br> WICHTIG: Bei der Migration zu Lösungsvariablen verlieren Sie **alle** historischen Trends und Vergleiche für Medienberichte. |

>[!IMPORTANT]
>
>Ändern Sie nicht die Klassifizierungsnamen für Variablen, die in der Dokumentation zu den Variablen für Streaming-Medien (über den Link [Übersicht über Streaming-Medien-Services](/help/media-overview.md)) aufgeführt sind und dort unter „Berichterstellung/Reservierte Variable“ als „Klassifizierung“ beschrieben sind. Die Medienklassifizierungen werden definiert, wenn eine Report Suite für das Medien-Tracking aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe anhand der Namen der Variablen, ob die Klassifizierungen aktiviert sind. Wenn eine fehlt, fügt Adobe die fehlenden erneut hinzu.

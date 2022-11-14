---
title: Streaming-Mediensammlungs-API � Anforderungsparameter
description: „Was sind die Anforderungsparameter, Anforderungsschlüssel und Beschreibungen der Mediensammlungs-API?“
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 99%

---

# Anfrageparameter {#request-parameters}

## Analytics-Daten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | J | string | `sessionStart` | Die URL Ihres Adobe Analytics-Servers |
| `analytics.reportSuite` | J | Zeichenfolge | `sessionStart` | Die ID, die Ihre Analytics-Reporting-Daten identifiziert |
| `analytics.enableSSL` | N | boolean | `sessionStart` | True oder False für die SSL-Aktivierung |
| `analytics.visitorId` | N | Zeichenfolge | `sessionStart` | Die Adobe-Besucher-ID ist eine benutzerdefinierte ID, die Sie in mehreren Adobe-Anwendungen verwenden können. Die `visitorId` in Heartbeat entspricht der `VID.` in Analytics. |

## Besucherdaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | J | Zeichenfolge | `sessionStart` | Die Experience Cloud-Organisations-ID, die Ihre Organisation innerhalb der Adobe Experience Cloud-Umgebung identifiziert |
| `visitor.marketingCloudUserId` | N | Zeichenfolge | `sessionStart` | Dies ist die Experience Cloud-Benutzer-ID (ECID). In den meisten Szenarien ist dies die ID, die Sie zur Identifizierung eines Benutzers verwenden sollten. Die `marketingCloudUserId` in Heartbeat entspricht der `MID` in Adobe Analytics. Dieser Parameter ist zwar technisch nicht erforderlich, aber für den Zugriff auf die Apps der Experience Cloud-Familie erforderlich. |
| `visitor.aamLocationHint` | N | Ganzzahl | `sessionStart` | Stellt Adobe Audience Manager-Edge-Daten bereit – Wenn kein Wert eingegeben wird, ist der Wert null. |
| `appInstallationId` | N | Zeichenfolge | `sessionStart` | Die appInstallationId identifiziert Anwendung und Gerät eindeutig. |

## Inhaltsdaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | J | Zeichenfolge | `sessionStart` | Eindeutige Kennung für den Inhalt |
| `media.name` | N | Zeichenfolge | `sessionStart` | Lesbarer Name für den Inhalt |
| `media.length` | J | Anzahl | `sessionStart` | Inhaltsdauer (in Sekunden) |
| `media.contentType` | J | Zeichenfolge | `sessionStart` | Format des Streams (hierbei kann es sich um eine beliebige Zeichenfolge handeln, empfohlen werden jedoch Werte wie „Live“, „VOD“ oder „Linear“) |
| `media.playerName` | J | Zeichenfolge | `sessionStart` | Der Name des Players, der für das Rendering des Inhalts verantwortlich ist |
| `media.channel` | J | Zeichenfolge | `sessionStart` | Der Verbreitungskanal für den Inhalt. Dabei kann es sich um den Namen einer App, einer Website oder einer Eigenschaft handeln. |
| `media.resume` | N | boolean | `sessionStart` | Gibt an, ob ein Benutzer eine vorherige Sitzung fortsetzt (statt eine neue Sitzung zu starten) |
| `media.sdkVersion` | N | Zeichenfolge | `sessionStart` | Die vom Player verwendete SDK-Version |

## Standardmäßige Inhaltsmetadaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | Zeichenfolge | `sessionStart` | Streamformat, z. B. &quot;HD&quot; |
| `media.show` | N | Zeichenfolge | `sessionStart` | Der Name des Programms oder der Serie |
| `media.season` | N | Zeichenfolge | `sessionStart` | Die Staffelnummer der Sendung oder Serie |
| `media.episode` | N | Zeichenfolge | `sessionStart` | Die Folge der Sendung oder Serie |
| `media.assetId` | N | Zeichenfolge | `sessionStart` | Die eindeutige ID für den Inhalt des Video-Assets, z. B. die Kennung einer Serienfolge, eines Film-Assets oder eines Live-Events. Normalerweise stammen diese IDs von Metadatensystemen wie EIDR, TMS/Gracenote oder Rovi. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen. |
| `media.genre` | N | Zeichenfolge | `sessionStart` | Die Art des Inhalts nach Definition des Inhaltserstellers |
| `media.firstAirDate` | N | Zeichenfolge | `sessionStart` | Das Datum der Erstausstrahlung des Inhalts im Fernsehen |
| `media.firstDigitalDate` | N | Zeichenfolge | `sessionStart` | Das Datum der Erstausstrahlung des Inhalts auf einer digitalen Plattform |
| `media.rating` | N | Zeichenfolge | `sessionStart` | Die Alterseinstufung nach der Definition von TV Parental Guidelines |
| `media.originator` | N | Zeichenfolge | `sessionStart` | Der Ersteller des Inhalts |
| `media.network` | N | Zeichenfolge | `sessionStart` | Der Name des Netzwerks/Senders |
| `media.showType` | N | Zeichenfolge | `sessionStart` | Der Inhaltstyp, angegeben als Integer-Wert zwischen 0 und 3: <ul> <li>0 - Vollständige Folge </li> <li>1 - Vorschau </li> <li>2 - Clip </li> <li>3 - Sonstiges </li> </ul> |
| `media.adLoad` | N | Zeichenfolge | `sessionStart` | Die Art der geladenen Anzeige |
| `media.pass.mvpd` | N | Zeichenfolge | `sessionStart` | Der von der Adobe-Authentifizierung bereitgestellte MVPD |
| `media.pass.auth` | N | Zeichenfolge | `sessionStart` | Zeigt an, dass der Anwender durch die Adobe-Authentifizierung autorisiert wurde (dieser Parameter kann nur true lauten, wenn er festgelegt wurde). |
| `media.dayPart` | N | Zeichenfolge | `sessionStart` | Die Tageszeit, zu der der Inhalt übertragen wurde |
| `media.feed` | N | Zeichenfolge | `sessionStart` | Die Art des Feeds, z. B. „West-HD“ |

## Anzeigedaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | Zeichenfolge | `adBreakStart` | Der Anzeigename der Werbeunterbrechung |
| `media.ad.podIndex` | J | Ganzzahl | `adBreakStart` | Der Index der Anzeigen-Pods im Video |
| `media.ad.podSecond` | J | Anzahl | `adBreakStart` | Die Sekunde, in der der Pod gestartet wurde |
| `media.ad.podPosition` | J | Ganzzahl | `adStart` | Der Index der Anzeige innerhalb der Werbegruppe (beginnend bei 1) |
| `media.ad.name` | N | Zeichenfolge | `adStart` | Der Anzeigename der Werbeanzeige |
| `media.ad.id` | J | Zeichenfolge | `adStart` | Der Name der Werbeanzeige |
| `media.ad.length` | J | Anzahl | `adStart` | Die Länge der Videoanzeige in Sekunden |
| `media.ad.playerName` | J | Zeichenfolge | `adStart` | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist |

## Standardmäßige Anzeigenmetadaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | Zeichenfolge | `adStart` | Das Unternehmen oder die Marke des Produkts, das in der Anzeige vorgestellt wird |
| `media.ad.campaignId` | N | Zeichenfolge | `adStart` | Die ID der Anzeigenkampagne |
| `media.ad.creativeId` | N | Zeichenfolge | `adStart` | Die ID der Werbeanzeige |
| `media.ad.siteId` | N | Zeichenfolge | `adStart` | Die ID der Anzeigen-Site |
| `media.ad.creativeURL` | N | Zeichenfolge | `adStart` | Die URL der Werbeanzeige |
| `media.ad.placementId` | N | Zeichenfolge | `adStart` | Die Platzierungs-ID der Anzeige |

## Kapiteldaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | J | Ganzzahl | `chapterStart` | Identifiziert die Position des Kapitels im Inhalt |
| `media.chapter.offset` | J | Anzahl | `chapterStart` | Die Sekunde, in der die Wiedergabe des Kapitels beginnt |
| `media.chapter.length` | J | Anzahl | `chapterStart` | Die Länge des Kapitels in Sekunden |
| `media.chapter.friendlyName` | N | Zeichenfolge | `chapterStart` | Der Anzeigename des Kapitels |

## Qualitätsdaten

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Ganzzahl | Eines | Die durchschnittliche Bitrate (in Bit/s). Die durchschnittliche Bitrate wird als gewichteter Durchschnitt aller Bitratenwerte im Zusammenhang mit der Wiedergabedauer berechnet, die während einer Wiedergabesitzung aufgetreten sind. |
| `media.qoe.droppedFrames` | N | Ganzzahl | Eines | Die Anzahl der Dropped Frames im Stream |
| `media.qoe.framesPerSecond` | N | Ganzzahl | Eines | Die Anzahl der Frames pro Sekunde |
| `media.qoe.timeToStart` | N | Ganzzahl | Eines | Die Dauer (in Millisekunden) zwischen der Aktivierung der Wiedergabetaste durch den Benutzer und dem Laden und Abspielen des Inhalts |

## Parameter des California Consumer Privacy Act (CCPA) {#ccpa-params}

| Anforderungsschlüssel  | erforderlich | Anfragetyp-Schlüssel | Eingerichtet auf... |  Beschreibung  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | boolean | `sessionStart` | Auf „true“ (wahr) setzen, wenn der Endbenutzer die Freigabe seiner Daten für Adobe Analytics und andere Experience Cloud-Lösungen (z. B. Audience Manager) abgelehnt hat. |
| `analytics.optOutShare` | N | boolean | `sessionStart` | Auf „true“ (wahr) setzen, wenn der Endbenutzer die Verknüpfung seiner Daten (z. B. mit anderen Adobe Analytics-Clients) abgelehnt hat. |

## Zusätzliche Details {#additional-details}

### visitor.marketingCloudUserId

Übergeben Sie die Experience Cloud-Benutzer-ID (auch als `MID` oder `MCID` bezeichnet) im `sessionStart`-Aufruf, indem Sie sie mit folgendem Schlüssel in der `params`-Map angeben: **visitor.marketingCloudUserId**. Diese Funktion ist hilfreich, wenn Sie schon andere Experience Cloud-Produkte integriert haben und bereits über eine MCID verfügen.

>[!NOTE]
>
>Media Analytics (MA) ist in das Portfolio von Experience Cloud-Anwendungen (Adobe Analytics, Audience Manager, Target usw.) integriert. Sie benötigen eine Experience Cloud ID, um auf diese Anwendungen zuzugreifen. _In den meisten Szenarien sollten Sie die ECID verwenden, um Benutzer zu identifizieren._

### appInstallationId

* **Wenn Sie den `appInstallationId`-Wert *nicht* übergeben:** Das MA-Backend generiert keine MCID mehr, sondern überlässt diese Aufgabe Adobe Analytics. Adobe empfiehlt, entweder eine MCID (sofern verfügbar) oder eine `appInstallationId` zu senden (neben der erforderlichen `marketingCloudOrgId`), damit die Mediensammlungs-API die MCID generiert und bei allen Aufrufen sendet.

* **Wenn Sie *den*`appInstallationId`-Wertübergeben:** Die MCID *kann* vom MA-Backend generiert werden, wenn Sie Werte für die Parameter `appInstallationId` und `marketingCloudOrgId` (erforderlich) übergeben.  Wenn Sie `appInstallationId` nicht selbst übergeben, muss der Wert clientseitig persistent sein. Er muss außerdem eindeutig für die Anwendung auf dem Gerät sein und beibehalten werden, bis die Anwendung neu installiert wird.

>[!NOTE]
>
>`appInstallationId` identifiziert die Anwendung *und das Gerät* eindeutig. Sie muss für jede Anwendung auf jedem Gerät eindeutig sein. Zwei Anwender, die dieselbe Version der Anwendung auf verschiedenen Geräten verwenden, müssen also eine unterschiedliche (eindeutige) `appInstallationId` senden.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Dieser Parameter ist nicht nur für die MCID-Generierung erforderlich, sondern wird auch als Wert für die Herausgeber-ID verwendet (basierend auf der Media Analytics den [Abgleich von Verknüpfungsregeln durchführt](/help/use-cases/federated-analytics.md)).

### Analytics-Legacy-Anwender-ID (aid) und deklarierte Anwender-IDs (customerIDs)

* **analytics.aid:**

   Der Wert dieses Schlüssels muss eine Zeichenfolge sein, die die veraltete Analytics-Benutzer-ID darstellt
* **visitor.customerIDs:**

   Der Wert dieses Schlüssels muss ein Objekt im folgenden Format sein:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

Beachten Sie, dass der Wert `visitor.customerIDs` über mehrere Objekte im angegebenen Format verfügen kann.

### visitor.aamLocationHint

Dieser Parameter gibt an, welcher AAM-Edge (Adobe Audience Manager) angesteuert wird, wenn Adobe Analytics die Kundendaten an Audience Manager sendet. Wenn kein Wert eingegeben wird, ist der Wert null. Das ist insbesondere dann wichtig, wenn Endanwender ihre Geräte an geografisch weit entfernten Standorten verwenden (z. B. US-Ost- und -Westküste, Europa, Asien). Andernfalls werden die Benutzerdaten über mehrere AAM-Edges verteilt.

### media.resume

Wenn die Anwendung feststellt, dass eine Sitzung geschlossen und später wiederaufgenommen wurde – z. B. weil der Anwender das Video verlassen hat, aber zu einem späteren Zeitpunkt zurückgekehrt ist und der Player die Wiedergabe von der vorherigen Position fortgesetzt hat –, können Sie einen optionalen booleschen **media.resume**-Parameter im params-Bereich des `sessionStart`-Aufrufs festlegen.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->

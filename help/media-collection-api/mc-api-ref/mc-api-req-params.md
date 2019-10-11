---
seo-title: Anfrageparameter
title: Anfrageparameter
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 5fc38098bcd497f3305f76ae2b23757b5f81ac69

---


# Anfrageparameter{#request-parameters}

## Analytics-Daten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | Die URL Ihres Adobe Analytics-Servers |
| `analytics.reportSuite` | Y | `sessionStart` | Die ID, die Ihre Analytics-Reporting-Daten identifiziert |
| `analytics.enableSSL` | N | `sessionStart` | True oder False für die SSL-Aktivierung |
| `analytics.visitorId` | N | `sessionStart` | Die Adobe-Besucher-ID ist eine benutzerdefinierte ID, die Sie in mehreren Adobe-Anwendungen verwenden können. Heartbeat `visitorId` entspricht Analytics `VID.` |

## Besucherdaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Die Experience Cloud-Organisations-ID, die Ihre Organisation innerhalb der Adobe Experience Cloud-Umgebung identifiziert |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Dies ist die Experience Cloud-Benutzer-ID (ECID). In den meisten Fällen ist dies die ID, die Sie zur Identifizierung eines Benutzers verwenden sollten. Der Heartbeat `marketingCloudUserId` entspricht dem `MID` in Adobe Analytics. Dieser Parameter ist zwar technisch nicht erforderlich, aber für den Zugriff auf die Apps der Experience Cloud-Familie erforderlich. |
| `visitor.aamLocationHint` | N | `sessionStart` | Stellt Adobe Audience Manager-Edge-Daten bereit |
| `appInstallationId` | N | `sessionStart` | Die appInstallationId identifiziert Anwendung und Gerät eindeutig. |

## Inhaltsdaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Eindeutige Kennung für den Inhalt |
| `media.name` | N | `sessionStart` | Lesbarer Name für den Inhalt |
| `media.length` | Y | `sessionStart` | Inhaltsdauer (in Sekunden) |
| `media.contentType` | Y | `sessionStart` | Format des Streams (hierbei kann es sich um eine beliebige Zeichenfolge handeln, empfohlen werden jedoch Werte wie „Live“, „VOD“ oder „Linear“) |
| `media.playerName` | Y | `sessionStart` | Der Name des Players, der für das Rendering des Inhalts verantwortlich ist |
| `media.channel` | Y | `sessionStart` | Der Verbreitungskanal für den Inhalt. Hierbei kann es sich um den Namen einer App, einer Website oder eines anderen Assets handeln. |
| `media.resume` | N | `sessionStart` | Gibt an, ob ein Benutzer eine vorherige Sitzung wiederaufnimmt (statt eine neue Sitzung zu starten) |
| `media.sdkVersion` | N | `sessionStart` | Die vom Player verwendete SDK-Version |

## Standardmäßige Inhaltsmetadaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | Der Name des Programms oder der Serie |
| `media.season` | N | `sessionStart` | Die Staffelnummer der Sendung oder Serie |
| `media.episode` | N | `sessionStart` | Die Folge der Sendung oder Serie |
| `media.assetId` | N | `sessionStart` | Die eindeutige ID für den Inhalt des Video-Assets, z. B. die Kennung einer Serienfolge, eines Film-Assets oder eines Live-Events. In der Regel werden diese IDs von Metadaten-Anbietern wie EIDR, TMS/Gracenote oder Rovi abgerufen. Diese IDs können auch von anderen speziellen oder internen Systemen stammen. |
| `media.genre` | N | `sessionStart` | Die Art des Inhalts nach Definition des Inhaltserstellers |
| `media.firstAirDate` | N | `sessionStart` | Das Datum der Erstausstrahlung des Inhalts im Fernsehen |
| `media.firstDigitalDate` | N | `sessionStart` | Das Datum der Erstausstrahlung des Inhalts auf einer digitalen Plattform |
| `media.rating` | N | `sessionStart` | Die Alterseinstufung nach der Definition von TV Parental Guidelines |
| `media.originator` | N | `sessionStart` | Der Ersteller des Inhalts |
| `media.network` | N | `sessionStart` | Der Name des Netzwerks/Senders |
| `media.showType` | N | `sessionStart` | Die Art des Inhalts, angegeben als Integer-Wert zwischen 0 und 3: <ul> <li>0: Vollständige Folge </li> <li>1: Vorschau </li> <li>2: Clip </li> <li>3: Sonstiges </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Die Art der geladenen Anzeige |
| `media.pass.mvpd` | N | `sessionStart` | Der von der Adobe-Authentifizierung bereitgestellte MVPD |
| `media.pass.auth` | N | `sessionStart` | Zeigt an, dass der Anwender durch die Adobe-Authentifizierung autorisiert wurde (dieser Parameter kann nur true lauten, wenn er festgelegt wurde). |
| `media.dayPart` | N | `sessionStart` | Die Tageszeit, zu der der Inhalt übertragen wurde |
| `media.feed` | N | `sessionStart` | Die Art des Feeds, z. B. „West-HD“ |

## Anzeigedaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Der Anzeigename der Werbeunterbrechung |
| `media.ad.podIndex` | Y | `adBreakStart` | Der Index der Anzeigen-Pods im Video |
| `media.ad.podSecond` | Y | `adBreakStart` | Die Sekunde, in der der Pod gestartet wurde |
| `media.ad.podPosition` | Y | `adStart` | Der Index der Anzeige innerhalb der Werbegruppe (beginnend bei 1) |
| `media.ad.name` | N | `adStart` | Der Anzeigename der Werbeanzeige |
| `media.ad.id` | Y | `adStart` | Der Name der Werbeanzeige |
| `media.ad.length` | Y | `adStart` | Die Länge der Videoanzeige in Sekunden |
| `media.ad.playerName` | Y | `adStart` | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist |

## Standardmäßige Anzeigenmetadaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Das Unternehmen oder die Marke des Produkts, das in der Anzeige vorgestellt wird |
| `media.ad.campaignId` | N | `adStart` | Die ID der Anzeigenkampagne |
| `media.ad.creativeId` | N | `adStart` | Die ID der Werbeanzeige |
| `media.ad.siteId` | N | `adStart` | Die ID der Anzeigen-Site |
| `media.ad.creativeURL` | N | `adStart` | Die URL der Werbeanzeige |
| `media.ad.placementId` | N | `adStart` | Die Platzierungs-ID der Anzeige |

## Kapiteldaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifiziert die Position des Kapitels im Inhalt |
| `media.chapter.offset` | Y | `chapterStart` | Die Sekunde, in der die Wiedergabe des Kapitels beginnt |
| `media.chapter.length` | Y | `chapterStart` | Die Länge des Kapitels in Sekunden |
| `media.chapter.friendlyName` | N | `chapterStart` | Der Anzeigename des Kapitels |

## Qualitätsdaten

| Anforderungsschlüssel | Erforderlich | Festgelegt in |  Beschreibung  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Alle | Die Bitrate des Streams |
| `media.qoe.droppedFrames` | N | Alle | Die Anzahl der Dropped Frames im Stream |
| `media.qoe.framesPerSecond` | N | Alle | Die Anzahl der Frames pro Sekunde |
| `media.qoe.timeToStart` | N | Alle | Die Zeit (in Millisekunden), die zwischen dem Start des Videos durch den Anwender und der tatsächlichen Wiedergabe des Inhalts vergeht |

## Zusätzliche Details {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. Diese Funktion ist hilfreich, wenn Sie schon andere Experience Cloud-Produkte integriert haben und bereits über eine MCID verfügen.

>[!NOTE]
>
>Media Analytics (MA) ist in die Apps der Experience Cloud-Familie (Adobe Analytics, Audience Manager, Target usw.) integriert. Sie benötigen eine Experience Cloud ID, um auf diese Anwendungen zuzugreifen. _Mit der ECID können Sie Benutzer in den meisten Szenarien identifizieren._

### appInstallationId

* **Wenn Sie *keinen*`appInstallationId`Wert übergeben -** Das MA-Back-End generiert keine MCID mehr, sondern setzt hierfür Adobe Analytics ein. Adobe empfiehlt, entweder eine MCID (sofern verfügbar) oder eine `appInstallationId` zu senden (neben der erforderlichen `marketingCloudOrgId`), damit die Mediensammlungs-API die MCID generiert und bei allen Aufrufen sendet.

* **Wenn Sie *den*Wert -`appInstallationId`Die MCID** kann vom MA-Back-End generiert werden *, wenn Sie Werte für* und die (erforderlichen) `appInstallationId``marketingCloudOrgId` Parameter übergeben. Wenn Sie `appInstallationId` nicht selbst übergeben, muss der Wert clientseitig persistent sein. Er muss außerdem eindeutig für die Anwendung auf dem Gerät sein und beibehalten werden, bis die Anwendung neu installiert wird.

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. Sie muss für jede Anwendung auf jedem Gerät eindeutig sein. Zwei Anwender, die dieselbe Version der Anwendung auf verschiedenen Geräten verwenden, müssen also eine unterschiedliche (eindeutige) `appInstallationId` senden.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](/help/federated-analytics.md))

### Analytics-Legacy-Anwender-ID (aid) und deklarierte Anwender-IDs (customerIDs)

* **analytics.aid:**

   Der Wert dieses Schlüssels muss eine Zeichenfolge sein, die die Legacy-Benutzer-ID von Analytics darstellt.
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

Dieser Parameter gibt an, welcher Adobe Audience Manager (AAM) Edge betroffen sein würde, wenn Adobe Analytics die Kundendaten an Audience Manager sendet. Wenn Sie diesen Parameter nicht übergeben, wird er von Adobe fest auf 1 codiert. Das ist insbesondere dann wichtig, wenn Endanwender ihre Geräte an geografisch weit entfernten Standorten verwenden (z. B. US-Ost- und -Westküste, Europa, Asien). Andernfalls werden die Daten auf verschiedene AAM-Edges aufgeteilt.

### media.resume

Wenn die Anwendung feststellt, dass eine Sitzung geschlossen und später wiederaufgenommen wurde – z. B. weil der Anwender das Video verlassen hat, aber zu einem späteren Zeitpunkt zurückgekehrt ist und der Player die Wiedergabe von der vorherigen Position fortgesetzt hat –, können Sie einen optionalen booleschen **media.resume**-Parameter im params-Bereich des `sessionStart`-Aufrufs festlegen.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->

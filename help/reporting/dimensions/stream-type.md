---
title: Stream-Typ
description: Erfasst, ob es sich bei jeder Mediensitzung um Audio- oder Videoinhalte handelte.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%
---

# Stream-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Stream-Typ**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/stream-type.md) unter „Stream-Typ“*

>[!ENDSHADEBOX]

Die Dimension **Stream-**) erfasst, ob es sich bei jeder Mediensitzung um Audio- oder Videoinhalte handelte. Sie ist in Adobe Analytics verfügbar, sobald [Media Core aktiviert](/help/reporting/setup/analytics-reporting.md) für die Report Suite und in Customer Journey Analytics für jeden Datensatz, der Streaming-Mediendaten enthält.

## So wird diese Dimension ausgefüllt

Der Stream-Typ wird vom Player beim Sitzungsstart festgelegt und an den Sitzungsabschlussaufruf weitergeleitet. Er wird weder berechnet noch abgeleitet. Der angezeigte Wert entspricht exakt dem Wert, der während der Erfassung gesendet wurde.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.streamType`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>Wenn der Stream-Typ nicht festgelegt ist, wird die Dimension für diese Sitzung nicht ausgefüllt. Diese Sitzungen sind von den integrierten Segmenten Nur-Audio und Nur-Video ausgeschlossen und das Segment Alle Streaming-Medien wird unterzählt, wenn es in Verbindung mit Aufschlüsselungen des Stream-Typs verwendet wird.

## Dimensionselemente

| Wert | Beschreibung |
| --- | --- |
| `video` | Die Sitzung bestand aus Videoinhalten. |
| `audio` | Die Sitzung bestand aus Audioinhalten wie einem Podcast, Hörbuch oder Musikstream. |

Benutzerdefinierte Werte werden von den Sammlungs-APIs technisch akzeptiert, werden jedoch nicht empfohlen. Sie stimmen nicht mit den unten beschriebenen integrierten Segmenten überein und können zu inkonsistenten Berichten über Implementierungen hinweg führen.

## Empfohlene Segmente

Der Stream-Typ ist die Grundlage für die in Adobe Analytics integrierten Segmente [!UICONTROL Medien-]). Verwenden Sie diese Segmente, um jeden Streaming-Medienbericht auf einen bestimmten Inhaltstyp zu beschränken:

| Segment | Regel |
| --- | --- |
| [!UICONTROL Alle Streaming-Medien] | Content (ID) exists |
| [!UICONTROL Nur Audio] | Content (ID) exists UND Stream Type = `audio` |
| [!UICONTROL Nur Video] | Inhalt (ID) existiert UND Stream-Typ != `audio` |

>[!TIP]
>
>Das [!UICONTROL Nur Video]-Segment verwendet eine `!=` Regel anstelle von `= video`, um Sitzungen korrekt zu erfassen, bei denen der Stream-Typ möglicherweise auf einen benutzerdefinierten Wert festgelegt wurde, der nicht `audio` ist.

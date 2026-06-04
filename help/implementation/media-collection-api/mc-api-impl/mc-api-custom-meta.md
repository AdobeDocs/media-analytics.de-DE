---
title: Unterstützung benutzerspezifischer Metadaten
description: Erfahren Sie, wie Sie benutzerdefinierte Schlüssel-Wert-Paare für die Ereignisse sessionStart, chapterStart und adStart bereitstellen.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# Unterstützung benutzerspezifischer Metadaten{#custom-metadata-support}

Mit der Mediensammlungs-API können Sie benutzerdefinierte Schlüssel-Wert-Paare zusammen mit Standardparametern in `sessionStart`-, `adStart`- und `chapterStart` senden. Benutzerdefinierte Metadaten werden an **Adobe Analytics** weitergeleitet, wobei die entsprechenden Medienereignisse geschlossen werden.

Um diese Daten in Analysis Workspace verfügbar zu machen, müssen Kunden benutzerdefinierte eVars definieren und Verarbeitungsregeln konfigurieren, um sie entsprechend ihrem Anwendungsfall auszufüllen. Nach der Zuordnung zu eVars oder Props werden die Daten auch in Adobe Experience Platform über die entsprechenden eVar-Pfade verfügbar, sofern der [Analytics-Quell-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) konfiguriert ist.

Informationen zu XDM-basierten Implementierungen mit Experience Edge finden Sie unter [Unterstützung benutzerdefinierter Metadaten - XDM-Format](/help/implementation/edge/custom-metadata.md).

## Überblick

Benutzerdefinierte Metadaten werden im Anfragetext als `customMetadata` neben dem `params` positioniert. Sie gilt für drei Ereignistypen:

| Ereignis | Metadaten gelten für |
|-------|-------------------|
| `sessionStart` | Hauptinhalt (gesamte Sitzung) |
| `adStart` | Individuelle Werbung |
| `chapterStart` | Kapitel oder Segment des Inhalts |

## Struktur

Benutzerdefinierte Metadaten sind ein flaches **Objekt** (Schlüssel-Wert-Paare) auf Ereignisebene neben dem `params` Schlüssel:

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### Obligatorische Parameter nach Ereignistyp

| Ereignis | Erforderliche `params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### Wichtige Benennungsanforderungen

* Verwenden Sie das `media.`-Präfix nicht in benutzerdefinierten Metadatenschlüsseln. Es werden Standard-Medienfeldern zugeordnet und können diese in Analytics-Berichten überschreiben
* Das `a.`-Präfix ist für Adobe-Standardmetadaten reserviert und darf nicht verwendet werden

## Benutzerdefinierte Metadaten für Hauptinhalte

Mit `sessionStart` gesendet. Gilt für die verfolgten primären Medien und bleibt für alle Anzeigen- und Kapitelaufrufe verfügbar. Alle hier definierten benutzerdefinierten Metadaten werden beim entsprechenden Schließen-Aufruf automatisch vom Medien-Backend zusammengeführt. Er wird zusammen mit allen spezifischen benutzerdefinierten Metadaten eingefügt, die für Anzeigen und Kapitel definiert sind.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## Hinzufügen benutzerdefinierter Metadaten

Mit `adStart` gesendet. Spezifisch für jede einzelne Anzeige. Die benutzerdefinierten Metadaten aus `sessionStart` werden auch automatisch vom Medien-Backend beim Aufruf zum Schließen der Anzeige zusammen mit allen hier definierten anzeigenspezifischen benutzerdefinierten Metadaten zusammengeführt.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## Benutzerdefinierte Kapitel-Metadaten

Mit `chapterStart` gesendet. Spezifisch für jedes Inhaltskapitel oder Segment. Die benutzerdefinierten Metadaten aus `sessionStart` werden beim Kapitelabschlussaufruf auch automatisch vom Medien-Backend zusammen mit den hier definierten kapitelspezifischen benutzerdefinierten Metadaten zusammengeführt.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## Verhalten

* Alle benutzerdefinierten Metadatenwerte müssen &quot;**&quot;**. Konvertieren Sie Zahlen und boolesche Werte vor dem Versand.
* Benutzerdefinierte Metadaten werden in Analytics mit einem `c.` Präfix angezeigt (z. B. `contentCategory` → `c.contentCategory`)
* Zuordnen benutzerdefinierter Metadaten zu eVars, Props oder Kontextdatenvariablen über Analytics-Verarbeitungsregeln
* `sessionStart` Metadaten bleiben für die gesamte Sitzung erhalten. Für Aktualisierungen ist eine neue Sitzung erforderlich
* Jedes `adStart`- und `chapterStart`-Ereignis kann unterschiedliche benutzerdefinierte Metadaten enthalten

## Verwandte Dokumentation

* [Unterstützung benutzerdefinierter Metadaten - XDM-Format](/help/implementation/edge/custom-metadata.md) - Senden benutzerdefinierter Metadaten über Experience Edge sowohl an Analytics als auch an AEP
* [Adobe Analytics-Quell-Connector für Report Suite-Daten](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) — Importieren von Analytics-Daten in Adobe Experience Platform

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->

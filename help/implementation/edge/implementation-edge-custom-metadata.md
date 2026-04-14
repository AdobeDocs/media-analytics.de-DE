---
title: Unterstützung benutzerdefinierter Metadaten - XDM-Format
description: Erfahren Sie, wie Sie benutzerdefinierte Metadaten mit Medien-Tracking-Ereignissen im XDM-Format von Experience Edge senden.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: da2fe856a32f9056752b9e2c2e339d43be20372a
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---


# Unterstützung benutzerdefinierter Metadaten - XDM-Format

Mit der Experience Edge-API können Sie benutzerdefinierte Medienmetadaten zusammen mit standardmäßigen XDM-Feldern in `sessionStart`-, `adStart`- und `chapterStart`-API-Ereignissen senden. Benutzerdefinierte Medienmetadaten, die über das XDM-Format gesendet werden, können sowohl an **Adobe Analytics** als auch an **Adobe Experience Platform weitergeleitet**.

Informationen zu Implementierungen der Mediensammlungs-API finden Sie unter [Unterstützung benutzerdefinierter Metadaten](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md).

## Überblick

Benutzerdefinierte Medien-Metadaten können an zwei Stellen innerhalb einer Experience Edge-Anfrage gesendet werden, die jeweils ein unterschiedliches Routing-Verhalten aufweisen:

| Standort | An Adobe Analytics senden | An Adobe Experience Platform senden | Anwendungsfall |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅ Ja | ✅ Ja | In beiden Systemen erforderliche Geschäftsdaten |
| `_data` | ✅ Ja | ❌ | Analytics-spezifische Flags oder Verarbeitungshinweise |

Benutzerdefinierte Metadaten gelten für drei Ereignistypen:

| Ereignis | Metadaten gelten für |
|-------|-------------------|
| `sessionStart` | Hauptinhalt (gesamte Sitzung) |
| `adStart` | Individuelle Werbung |
| `chapterStart` | Kapitel oder Segment des Inhalts |

## Struktur

### `xdm.mediaCollection.customMetadata` (Analytics und AEP)

Benutzerdefinierte Metadaten sind ein **Array von Name/Wert-Objekten** innerhalb des `mediaCollection`:

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

&lt;InlineAlert variant="warning" slots="text" />

`customMetadata` muss ein **Array** innerhalb von `mediaCollection` sein, nicht auf `xdm` Stammebene.

**Falsch:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**Richtig:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` (nur Analytics)

Das `_data`-Objekt ist ein spezielles Experience Edge-Konstrukt, das Daten ausschließlich an Adobe Analytics sendet und AEP-Datensätze umgeht. Benutzerdefinierte Metadaten müssen unter `__adobe.analytics.contextData` platziert werden.

Im Gegensatz zu `xdm.mediaCollection.customMetadata`, das ein **Array von Name-Wert-** verwendet, verwendet die `_data`-Zuordnung ein flaches **Schlüssel-Wert-** direkt unter `contextData`:

| Ansatz | Struktur | Ziel |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | Array von `{"name": "...", "value": "..."}` Objekten | Analytics und AEP |
| `_data.__adobe.analytics.contextData` | Flacher Schlüssel-Wert-`{"key": "value"}` | Nur Analytics |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### Benennungskonventionen

- **XDM-Format** Präfix mit Mandanten-Namespace unter Verwendung eines Unterstrichs. Sie können auch Strukturen in Ihrer benutzerdefinierten Feldergruppe des Mandanten erstellen, z. B. `_<tenant>.<struct_name>.<field_name>`.
- **`_data`:** Felder werden unter `_data.__adobe.analytics.contextData` platziert. Für den Feldnamen ist kein Unterstrichpräfix erforderlich (z. B. `debugFlag`)

## Benutzerdefinierte Metadaten für Hauptinhalte

Mit `sessionStart` gesendet. Gilt für die verfolgten primären Medien und bleibt für alle Anzeigen- und Kapitelaufrufe verfügbar. Alle hier definierten benutzerdefinierten Metadaten werden beim entsprechenden Schließen-Aufruf automatisch vom Medien-Backend zusammengeführt. Er wird zusammen mit allen spezifischen benutzerdefinierten Metadaten eingefügt, die für Anzeigen und Kapitel definiert sind.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Anfrage

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## Hinzufügen benutzerdefinierter Metadaten

Mit `adStart` gesendet. Spezifisch für jede einzelne Anzeige. Die benutzerdefinierten Metadaten aus `sessionStart` werden auch automatisch vom Medien-Backend beim Aufruf zum Schließen der Anzeige zusammen mit allen hier definierten anzeigenspezifischen benutzerdefinierten Metadaten zusammengeführt.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Anfrage

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## Benutzerdefinierte Kapitel-Metadaten

Mit `chapterStart` gesendet. Spezifisch für jedes Inhaltskapitel oder Segment. Die benutzerdefinierten Metadaten aus `sessionStart` werden beim Kapitelabschlussaufruf auch automatisch vom Medien-Backend zusammen mit den hier definierten kapitelspezifischen benutzerdefinierten Metadaten zusammengeführt.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Anfrage

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## Verwenden des `_data`-Objekts (nur Analytics-Metadaten)

Verwenden Sie das `_data`-Objekt, wenn Sie Metadaten in Adobe Analytics benötigen **die nicht** in AEP-Datensätzen gespeichert werden sollen, z. B. temporäre Flags, Debugging-Variablen oder Analytics-spezifische Verarbeitungshinweise.

&lt;InlineAlert variant="warning" slots="text" />

Daten, die über `_data` gesendet werden, werden nicht in Adobe Experience Platform gespeichert und sind nicht für Real-Time CDP, Journey Orchestration oder andere AEP-Services verfügbar.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Anfrage

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

In diesem Beispiel:
- `_mycompany.league` → an Analytics und AEP gesendet
- `debugMode` und `testFlag` (unter `_data.__adobe.analytics.contextData`) → nur an Analytics gesendet


## Speicherort nachgelagerter Daten

&lt;InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata` ist der **eingehende API-Pfad** der zum Senden benutzerdefinierter Metadaten mit Ereignissen verwendet wird. Nach der Verarbeitung werden die Daten als Kontextdatenvariablen an Adobe Analytics weitergeleitet und in Adobe Experience Platform unter `mediaReporting.customMetadata` und als reduzierte Felder der obersten Ebene gespeichert.

**Adobe Analytics:**
- Nach der Verarbeitung werden benutzerdefinierte Metadaten als Kontextdatenvariablen an Adobe Analytics weitergeleitet. Das `_tenant` Präfix wird automatisch entfernt, sodass Verarbeitungsregeln nur auf den Feldpfad nach der `_tenant` verweisen (z. B. `_mycompany.contentCategory` wird `contentCategory`)
- Über `_data` gesendete Daten werden ebenfalls an Adobe Analytics weitergeleitet und stehen über Verarbeitungsregeln zur Verfügung
- Verwenden Sie Verarbeitungsregeln, um Kontextdatenvariablen eVars, Props oder anderen Analytics-Variablen zuzuordnen. Weitere [&#x200B; finden Sie unter „Datenvariablenzuordnung für die Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping)Edge Network&quot;.

**Adobe Experience Platform:**
- Benutzerdefinierte Metadatenfelder müssen als benutzerdefinierte Felder in Ihrem XDM-Schema definiert werden (z. B. `_mycompany`) und können in AEP als reduzierte Felder gespeichert und abgefragt werden

  ![Benutzerdefinierte Felddefinition im XDM-Schema](assets/custom_metadata.png)
- Für Berichte und Abfragen sind benutzerdefinierte Metadaten unter `mediaReporting.customMetadata` sowie als reduzierte Felder der obersten Ebene verfügbar. Verwenden Sie je nachdem, was für Ihren Anwendungsfall am besten geeignet ist.
- Abrufbar für Segmentierung, Journey Orchestration- und Real-Time CDP-Aktivierung

## Verhalten

- Alle benutzerdefinierten Metadatenwerte müssen &quot;**&quot;**. Konvertieren Sie Zahlen und boolesche Werte vor dem Versand.
- `sessionStart` Metadaten bleiben für die gesamte Sitzung erhalten. Für Aktualisierungen ist eine neue Sitzung erforderlich
- Jedes `adStart`- und `chapterStart`-Ereignis kann unterschiedliche benutzerdefinierte Metadaten enthalten
- Standard-XDM-Felder (`sessionDetails`, `advertisingDetails`, `chapterDetails`) werden gegenüber benutzerdefinierten Metadaten bevorzugt, wenn ein Standardfeld vorhanden ist


## Verwandte Dokumentation

- [Unterstützung benutzerdefinierter Metadaten](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md). — MC API (JSON-Format)
- [Datentyp „Media Collection Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) — XDM-Schemareferenz
- [Datenvariablenzuordnung für die Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) — Analytics-Kontextdatenzuordnung für XDM-Felder
<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->

---
title: Hochladen von Zeitplandaten zur Verfolgung von Live-Inhalten
description: Erfahren Sie, wie Sie Zeitplandaten hochladen, um Live-Inhalte zu verfolgen.
feature: Streaming Media
role: User, Admin, Data Engineer
hide: true
hidefromtoc: true
exl-id: 875c4513-ea4e-4c5f-bfc1-34ea175007ca
source-git-commit: b947a1d64c7fa58e784712397b0167d4186d00c3
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 2%

---

# Hochladen von Zeitplandaten zur Verfolgung von Live-Inhalten

Sie können Daten vergangener Live-Streaming-Medieninhalte planmäßig hochladen, um die Zuschauerzahlen von Live-Inhalten einfacher und genauer zu verfolgen. Sie können die Zuschauerzahlen für einzelne Programme und sogar bestimmte Themen oder Programmsegmente verfolgen.

Im Folgenden finden Sie Beispiele für Live-Inhalte, die mit dem Upload von Zeitplandaten unterstützt werden:

* FAST-Plattformen (Free Ad Supported TV)

* Lokale Datenströme

* Live-Sportübertragungen

* Nachrichten oder aktuelle Programme

## Funktionen

Bei Verwendung der Funktion zum Planen von Daten-Uploads vergangener Live-Streaming-Medieninhalte stehen verschiedene Funktionen zur Verfügung. In diesem Abschnitt werden einige der Schlüsselfunktionen beschrieben, die bei der Analyse der Programmleistung helfen.

Diese Funktionen sind unabhängig davon verfügbar, wie Sie die Erfassung von Streaming-Medien implementiert haben.

* **Programmzeitpläne genau verfolgen**: Identifizieren Sie die Start- und Endzeiten jedes einzelnen Programms im Live-Stream für den Zeitraum, den Sie analysieren möchten. Bei genauen Start- und Endzeiten wird die genaue Laufzeit genau wiedergegeben und kann für jede Viewer-Sitzung analysiert werden.

  So sind beispielsweise genaue Anfangs- und Endzeiten für ein Live-Sportereignis nicht immer bekannt, bis das Ereignis vorbei ist. Planen Sie Daten-Uploads, um genaue Berichte zu erhalten, indem Sie die Start- und Endzeiten nach Abschluss des Programms aktualisieren.

* **Verfolgen einzelner Themen oder Programmsegmente**: Erstellen Sie neue zeitbasierte Dimensionen für bestimmte Themen oder Programmsegmente (Zeitfenster) innerhalb eines bestimmten Programms. Diese zeitbasierten Dimensionen ermöglichen es Ihnen, die Zuschauerzahlen eines Programms auf einer spezifischeren Ebene zu analysieren und so Einblicke zu gewinnen, welche Themen oder Programmsegmente am besten angesprochen wurden.

  Wenn Sie beispielsweise ein Live-Sportereignis analysieren, z. B. ein Fußballspiel, können Sie separate Dimensionen für die erste Hälfte, die erste Halbzeit und die zweite Halbzeit erstellen. Das derartige Tracking bestimmter Themen oder Segmente innerhalb eines Programms ermöglicht eine detailliertere Aufschlüsselung des Viewer-Verhaltens.

* **Erstellen von Journey in Journey Optimizer**: Verfolgen Sie, welche Programme eine Person in einer bestimmten Sitzung angezeigt hat (oder sogar welche Themen oder Programmsegmente die Person angesehen hat), und verwenden Sie diese Daten in Adobe Journey Optimizer, um Benutzer-Journey für Kunden zu erstellen, die ein bestimmtes Programm gesehen haben oder Interesse an einem bestimmten Thema gezeigt haben.

## Funktionsweise von Zeitplandaten für Streaming-Medien

Die Funktion zum Planen von Daten für Streaming-Medien funktioniert wie folgt:

1. liest aus dem Programmzeitplan-Datensatz nach Programmzeitplänen-Datensätzen und filtert nach dem Datum des Zeitplans.

   Funktioniert nur für Programme, die zwischen 24 und 48 Stunden in der Vergangenheit aufgetreten sind.

2. Liest die Mediennutzungsereignisse aus dem Mediendatensatz und filtert nach Datum und XDM-Pfad in den Programmplaneinträgen.

3. Für jedes Medienabschlussereignis wird dieselbe Anzahl von Medienzeitplan-Startereignissen generiert, wie es Shows gab, die sich mit der Mediensitzung überschnitten.

   Jedes Medienzeitplan-Startereignis enthält den Namen und die Länge des Zeitplans.

   Außerdem enthält eine neue Zeitmetrik namens **scheduleTimePlayed** die Anzahl der Sekunden, die die Mediensitzung mit dem geplanten Programm überschnitten hat. Der Zeitstempel des geplanten Startereignisses ist der Zeitstempel des Starts der Sendung.

4. Schreibt die neuen geplanten Startereignisse in den AEP-Mediensatz.

## Voraussetzungen

Um Daten vergangener Live-Inhalte hochzuladen, muss Ihre Streaming Media-Umgebung die folgenden Voraussetzungen erfüllen:

* Die Streaming-Mediensammlung muss für das Tracking des Inhalts aktiviert sein, für den Sie Zeitplandaten hochladen möchten, wie in [Tracking-Übersicht](/help/use-cases/track-av-playback/track-core-overview.md) beschrieben<!--specifics??? -->

* Verwenden der Streaming Media Collection mit Customer Journey Analytics. Das Hochladen von Zeitplandaten ist in Adobe Analytics nicht verfügbar.

## Erstellen eines Programmzeitplan-Datensatzes in AEP

Bevor Sie Zeitplaninformationen per Push übertragen können, müssen Sie einen Programmplanungs-Datensatz in Experience Platform erstellen:

1. Erstellen Sie ein Schema basierend auf der XDM **Klasse „Geplantes**-Programm für Media Analytics“.

   ![Schema des Programmplans für Media Analytics](assets/media_schedule_finish_schema_creation.png)

   Dies ist die XDM-Definition der Klasse „Geplantes Programm für Media Analytics“.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Erstellen Sie einen Datensatz basierend auf dem von Ihnen erstellten Schema.

1. Fahren Sie mit dem folgenden Abschnitt fort: [Informationen zum Push-Zeitplan](#push-schedule-information).

## Informationen zum Push-Zeitplan

Nachdem Sie [Programmzeitplan-Datensatz erstellen](#create-a-program-schedule-dataset-in-aep) können Sie Zeitplaninformationen per Push übertragen:

1. Erstellen Sie eine JSON-Datei mit den Zeitplaninformationen.

   Die JSON-Datei muss ein Array von Zeitplanprogrammobjekten gemäß dem XDM-Schema enthalten.

1. Laden Sie die JSON-Datei hoch:

   >[!NOTE]
   >
   >Die cURL-Beispiele in diesem Abschnitt verwenden die folgenden Variablen:
   >
   >* Für die Authentifizierung mit Adobe Developer:
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* Organisations-ID: CUSTOMER_ORG_ID
   >* Datensatz-ID des im Setup erstellten Datensatzes: DATASET_ID
   >* Batch-ID, die in der ersten beim Datei-Upload verwendeten Anfrage erstellt wurde: BATCH_ID
   >* Der Name der Datei, die zum Pushen von Datensätzen verwendet wird: FILE_NAME

   1. Erstellen Sie einen neuen Batch und rufen Sie dann die Batch-ID aus der Antwort ab.

      Betrachten Sie das folgende Beispiel der Verwendung von cURL zum Erstellen eines neuen AEP-Batches:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Pushen Sie die JSON-Datei, die die Programmplanungs-Datensätze enthält, unter Verwendung der Batch-ID.

      Verwenden Sie zum Übertragen von Zeitplandaten die Batch-APIs von AEP, wie unter [Übersicht über die Batch-Aufnahme-API](https://experienceleague.adobe.com/de/docs/experience-platform/ingestion/batch/overview) beschrieben.

      Betrachten wir das folgende Beispiel für die Verwendung von cURL zum Pushen einer Datei mit den Zeitplandatensätzen:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Füllen Sie den Batch aus.

      Betrachten Sie das folgende Beispiel der Verwendung von cURL, um den Batch abzuschließen:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Fahren Sie mit dem folgenden Abschnitt fort: [&#x200B; eines Support-Tickets bei der Adobe-Kundenunterstützung](#log-a-support-ticket-with-adobe-customer-care).

## Erstellen Sie ein Support-Ticket bei der Adobe-Kundenunterstützung

Erstellen Sie ein Support-Ticket bei der Adobe-Kundenunterstützung mit den folgenden Informationen:

* **Mediendatensatz**: Geben Sie die Datensatz-ID des Datensatzes an, aus dem die Mediensitzungsdaten gelesen werden.

* **Zeitplan-Datensatz**: Geben Sie die Datensatz-ID des Datensatzes an, an den die Zeitplaneinträge gesendet werden.

* **Ausgabemedien-**: Geben Sie die Datensatz-ID des Datensatzes an, in dem die Startereignisse des Zeitplans gespeichert werden.

  Diese Datensatz-ID kann dieselbe Datensatz-ID sein wie der für den Medien-Datensatz. Wenn es sich um eine andere Datensatz-ID handelt, sollte es dennoch dasselbe XDM-Schema wie der Medien-Datensatz haben.

* **Organisations-ID**: Geben Sie Ihre Organisations-ID an.

## Beispiel einer JSON-Datei mit Zeitplan und zwei Datensätzen

Das folgende Beispiel zeigt eine Datei mit der Zeitplandatei JSON mit zwei Datensätzen. Jede JSON-Datei sollte alle geplanten Programme für einen Tag enthalten.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Grundlegendes zu den Feldern für Planprogramme im Beispiel

1. **mediaProgramDetails**: Muss die zum Erstellen des geplanten Startereignisses mindestens erforderlichen Informationen enthalten:
   * **startTimestamp**: Der Zeitpunkt, zu dem die Sendung begonnen hat.
   * **name**: Der Anzeigename der Sendung.
   * **length**: Die Anzahl der Sekunden, die die Sendung dauerte.

     >[!IMPORTANT]
     >
     >Wenn Sie mehrere Datenanfragen für den Zeitplan haben, können diese sich nicht überschneiden.

1. **scheduleDate**: Das Datum, an dem die Sendung gesendet wurde. Das Format sollte JJJJ-MM-TT sein. Er wird verwendet, um den Zeitplan-Datensatz zu filtern und alle Zeitpläne abzurufen, für die Adobe einen Zeitplan erstellt.
1. **scheduleFilter**: Wird zum Filtern aller Ereignisse für das Schließen von Mediensitzungen verwendet.
   * **filterPath**: Ein XDM-Pfad zu dem Feld, das zum Filtern verwendet wird.
   * **filterValue**: Der zum Filtern verwendete Wert.
1. **customMetadata**: Benutzerdefinierte Metadaten, die Sie dem Zeitplan hinzufügen möchten, beginnen Ereignisse. Diese Metadaten werden verwendet, um die benutzerdefinierten Metadaten zu überschreiben, die in den Ereignissen zum Schließen der Sitzung vorhanden sind.
1. **defaultMetadata**: Eine bestimmte Liste von Dimensionen, die die Standardmetadaten hinzufügen oder überschreiben können, die bei Medienschließungsaufrufen vorhanden sind.

   Im Folgenden finden Sie einige Beispiele für Dimensionen, die Sie in Customer Journey Analytics erstellen und über die Sie dann Berichte erstellen können:

   * **[&quot;_Episodenname_&quot;](https://experienceleague.adobe.com/de/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: Diese Dimension könnte Ihnen dabei helfen zu erfahren, welche Episoden in einer bestimmten Serie am besten funktionieren.

   * **[Asset-ID](https://experienceleague.adobe.com/de/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Fahren Sie mit [Analysieren von Daten in Customer Journey Analytics](#analyze-data-in-customer-journey-analytics) fort.

## Analysieren von Daten in Customer Journey Analytics

Innerhalb eines Tages nach dem Hochladen Ihrer Datendatei, wie in [Anfordern und Hochladen der Zeitplandatendatei](#request-and-upload-the-schedule-data-file) beschrieben, können Ihre Daten in Customer Journey Analytics gemeldet werden.

So erstellen Sie einen Bericht zu Ihren früheren Live-Streaming-Mediendaten in Customer Journey Analytics:

1. Erstellen Sie ein neues Projekt oder öffnen Sie ein vorhandenes.

1. Erstellen Sie das Projekt, indem Sie alle Tabellen oder Visualisierungen erstellen, die Sie für die Analyse Ihrer früheren Live-Streaming-Mediendaten benötigen.

   Verwenden Sie beim Erstellen des Projekts die Informationen, die Sie in die Datendatei für den Zeitplan aufgenommen und an die Adobe-Kundenunterstützung gesendet haben. Dazu gehören der übereinstimmende Schlüssel, Dimensionen und alle zusätzlichen Metadaten. Weitere Informationen finden Sie unter [Plandatendatei anfordern und hochladen](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->

---
title: Abrufen der JSON-Berichtsdaten zur mit Medienwiedergabe verbrachten Zeit mit Analytics 2.0-APIs
description: Hier erfahren Sie, wie Sie mit den Analytics 2.0-APIs Daten zu der mit Medienwiedergabe verbrachten Zeit abrufen können. Beispielanfrage und -antwort anzeigen.
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: 65e5b67a-26fc-433e-b99b-0ebbc24428ac
source-git-commit: 67f1fa8194fa58b2c513e3136d2bc7880f9cb06b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Abrufen der JSON-Berichtsdaten zur mit Medienwiedergabe verbrachten Zeit mit Analytics 2.0-APIs{#get-media-playback-time-spent-json-report-data}

Sie können Berichtsdaten zur Besuchszeit für Medienwiedergabe mit den [_*Analytics 2.0-APIs*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html) abrufen.

1. Filtern Sie die Daten mit einem beliebigen Segment, das auf der Benutzeroberfläche basiert. Um nach einer bestimmten Inhalts-ID zu filtern, erstellen Sie ein neues Segment.
1. Stellen Sie die `elements` -> `id` im Anfragetext auf `metrics/playback_time_spent_seconds` oder `metrics/playback_time_spent_minutes` ein, je nachdem, ob Sie die Ausgabe in Sekunden oder Minuten erhalten möchten.
1. Fordern Sie eine ausreichende Datenmenge an.

   * In dem von Ihnen im Bericht angegebenen Datenbereich werden die Daten aller gleichzeitigen Betrachter _zum Zeitpunkt des Endes der Videositzung erfasst._
Es gilt, Sitzungen zu berücksichtigen, die an einem Tag beginnen und nach Mitternacht enden, also am nächsten Tag.

   * Geben Sie bei Ihrer Anfrage für den vorgesehenen Zeitraum einen weiteren Tag für die Daten an, nutzen Sie aber in Ihrer Analyse _*nur die vorgesehenen Daten.*_

Die Beispielanforderung für einen Datentag würde wie im folgenden Beispiel aussehen. Die Anfrage wird für zwei aufeinander folgende Tagen durchgeführt, für den Bericht wird jedoch nur der erste Tag verwendet.

## Beispielanforderung

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2021-09-02T00:00/2021-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/playback_time_spent_minutes"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## Beispielantwort

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2021-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2021-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2021-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2021-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the Media Playback Time Spent report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The Media Playback Time Spent report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->

---
seo-title: Neuen Debug-Bericht erstellen
title: Neuen Debug-Bericht erstellen
uuid: 438 fde 3 d -98 f 9-46 d 1-9672-75 d 204361568
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Neuen Debugging-Bericht erstellen{#create-a-new-debug-report}

So erstellen Sie einen neuen Debug-Bericht:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Geben Sie in die Felder folgende Informationen ein:

   * **Berichtsname**: Geben Sie den Player-Namen und das Datum ein, damit Sie den Player während der Zertifizierung einfach verfolgen können und Marken und Plattform voneinander trennen können.
   * **Adobe Analytics**

      * [!UICONTROL Benutzername] und [!UICONTROL Gemeinsamer geheimer Schlüssel]: Diese Felder sind optional, Sie können Ihre Webservice-API-Anmeldedaten jedoch zu Adobe Debug hinzufügen, um die Variablennamen und -einstellungen für die Report Suite anzuzeigen.

         Ihnen stehen folgende Zugriffsmöglichkeiten zur Verfügung:

         * [!UICONTROL Analytics &gt; Admin &gt; Unternehmenseinstellungen &gt; Webdienste]
         * [!UICONTROL Analytics &gt; Admin &gt; Anwenderverwaltung &gt; Anwender &gt; Individuelle Anwendereinstellungen] Um Webservice-API-Anmeldedaten für einen neuen Anwender zu erstellen, fügen Sie den Anwender unter [!UICONTROL Anwenderverwaltung] zur Anwendergruppe **Zugriff auf Webdienste** hinzu.
      * [!UICONTROL Standardendpunkt] : Die Daten in diesem Feld werden von Adobe bereitgestellt und können nicht geändert werden.
      * [!UICONTROL Extra Endpoint] - Hinzufügen `CNAMES`, wenn Sie sie verwenden, für Tracking-Server wie `metrics.companyname.com`
   * **Media Heartbeats**

      * [!UICONTROL Standardendpunkt] : Die Daten in diesem Feld werden von Adobe bereitgestellt und können nicht geändert werden.
      * [!UICONTROL Zusätzlicher Endpunkt] - Wenn `CNAMES`Sie sie verwenden, für Ihren Tracking-Server, z. `metrics.companyname.com`B.




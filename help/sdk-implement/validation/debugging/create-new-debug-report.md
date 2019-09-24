---
seo-title: Neuen Debug-Bericht erstellen
title: Neuen Debug-Bericht erstellen
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

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
      * [!UICONTROL Standardendpunkt] - Die Daten in diesem Feld werden von Adobe bereitgestellt und können nicht geändert werden.
      * [!UICONTROL Extra-Endpunkt] - Fügen Sie `CNAMES`, falls Sie sie verwenden, für Tracking-Server wie `metrics.companyname.com`
   * **Video Heartbeats (Medienanalyse)**

      * [!UICONTROL Standardendpunkt] - Die Daten in diesem Feld werden von Adobe bereitgestellt und können nicht geändert werden.
      * [!UICONTROL Extra-Endpunkt] - Fügen Sie `CNAMES`bei Verwendung für Ihren Tracking-Server, z. B. `metrics.companyname.com`hinzu.




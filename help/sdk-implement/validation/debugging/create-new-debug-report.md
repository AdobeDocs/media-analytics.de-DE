---
title: Neuen Debug-Bericht erstellen
description: Erfahren Sie, wie Sie einen neuen Debug-Bericht erstellen.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 96%

---

# Neuen Debug-Bericht erstellen{#create-a-new-debug-report}

So erstellen Sie einen neuen Debug-Bericht:

1. Wählen Sie unter [!UICONTROL Neuen Debug-Bericht erstellen] Folgendes aus:

   ![](assets/create-new-debug-report.png)

1. Geben Sie in die Felder folgende Informationen ein:

   * **Berichtsname**: Geben Sie den Player-Namen und das Datum ein, damit Sie den Player während der Zertifizierung einfach verfolgen können und Marken und Plattform voneinander trennen können.
   * **Adobe Analytics**

      * [!UICONTROL Benutzername] und [!UICONTROL Gemeinsamer geheimer Schlüssel]: Diese Felder sind optional, Sie können Ihre Webservice-API-Anmeldedaten jedoch zu Adobe Debug hinzufügen, um die Variablennamen und -einstellungen für die Report Suite anzuzeigen.

         Ihnen stehen folgende Zugriffsmöglichkeiten zur Verfügung:

         * [!UICONTROL Analytics > Admin > Unternehmenseinstellungen > Webdienste]
         * [!UICONTROL Analytics > Admin > Anwenderverwaltung > Anwender > Individuelle Anwendereinstellungen] Um Webservice-API-Anmeldedaten für einen neuen Benutzer zu erstellen, fügen Sie den Benutzer unter [!UICONTROL Anwenderverwaltung] zur Benutzergruppe **Zugriff auf Webdienste** hinzu.
      * [!UICONTROL Standardendpunkt]: Die Daten in diesem Feld werden von Adobe angegeben und können nicht geändert werden.
      * [!UICONTROL Zusätzlicher Endpunkt]: Fügen Sie `CNAMES` (sofern Sie diese verwenden) für Tracking-Server wie `metrics.companyname.com` hinzu.
   * **Video-Heartbeats (Media Analytics)**

      * [!UICONTROL Standardendpunkt]: Die Daten in diesem Feld werden von Adobe angegeben und können nicht geändert werden.
      * [!UICONTROL Zusätzlicher Endpunkt:] Fügen Sie `CNAMES` (sofern Sie diese verwenden) für Ihren Tracking-Server wie `metrics.companyname.com` hinzu.

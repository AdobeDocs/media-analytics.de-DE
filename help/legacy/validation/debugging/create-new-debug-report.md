---
title: Neuen Debug-Bericht erstellen
description: Erfahren Sie, wie Sie einen neuen Debug-Report erstellen.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# Neuen Debug-Bericht erstellen{#create-a-new-debug-report}

So erstellen Sie einen neuen Debug-Bericht:

1. Wählen Sie unter [!UICONTROL Neuen Debug-Bericht erstellen] Folgendes aus:

   ![](assets/create-new-debug-report.png)

1. Füllen Sie die Felder mit den folgenden Informationen aus:

   * **Benennen des Berichts** - Geben Sie den Player-Namen und das Datum ein, damit Sie den Player während der Zertifizierung einfach verfolgen und Marken und Plattformen getrennt halten können.
   * **Adobe Analytics**

      * [!UICONTROL Benutzername] und [!UICONTROL Gemeinsamer geheimer Schlüssel] - Diese Felder sind optional. Sie können jedoch Ihre Web-Services-API-Anmeldeinformationen zu Adobe Debug hinzufügen, um die Variablennamen und Variableneinstellungen für die Report Suite anzuzeigen.

        Sie können auf eine der folgenden Arten zugreifen:

         * [!UICONTROL Analytics > Admin > Unternehmenseinstellungen > Web-Services]
         * [!UICONTROL Analytics > Admin > User Management > Benutzer > Individuelle Benutzereinstellungen] Um Anmeldedaten für eine Web-Services-API für einen neuen Benutzer zu erstellen, fügen Sie den Benutzer in [!UICONTROL User Management] der Benutzergruppe **Web Service Access** hinzu.

      * [!UICONTROL Standardendpunkt]: Die Daten in diesem Feld werden von Adobe angegeben und können nicht geändert werden.
      * [!UICONTROL Zusätzlicher Endpunkt]: Fügen Sie `CNAMES` (sofern Sie diese verwenden) für Tracking-Server wie `metrics.companyname.com` hinzu.

   * **Video-Heartbeats (Media Analytics)**

      * [!UICONTROL Standardendpunkt]: Die Daten in diesem Feld werden von Adobe angegeben und können nicht geändert werden.
      * [!UICONTROL Zusätzlicher Endpunkt:] Fügen Sie `CNAMES` (sofern Sie diese verwenden) für Ihren Tracking-Server wie `metrics.companyname.com` hinzu.

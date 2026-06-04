---
title: Anwendungsversion
description: Gibt die Version der Media Player-Anwendung an, die für jede Streaming-Sitzung verwendet wird.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# Anwendungsversion

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **App-Version**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/app-version.md) unter „App-Version“*

>[!ENDSHADEBOX]

Die Dimension **App-Version** zeigt die Versionszeichenfolge der bei der SDK-Initialisierung konfigurierten Media Player-Anwendung an. Ermitteln Sie damit, welche Player-Versionen aktiv verwendet werden, korrelieren Sie Qualitäts- oder Verhaltensänderungen mit bestimmten Versionen und priorisieren Sie die Unterstützung für häufig verwendete Versionen.

>[!NOTE]
>
>Diese Dimension erfasst die Version Ihrer **Media Player-Anwendung** und nicht die SDK-Bibliothek von Adobe. Adobes eigene SDK-Bibliotheksversion wird automatisch als separates internes Feld erfasst.

## So wird diese Dimension ausgefüllt

Die Anwendungsversion wird bei der Initialisierung von SDK einmal festgelegt und automatisch in jede Anfrage zum Sitzungsstart aufgenommen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird bei Verwendung von Edge-Implementierungen automatisch über die XDM-Feldzuordnung erfasst. Bei Implementierungen, die nur die Analytics betreffen, ordnen Sie `media.sdkVersion` mithilfe einer [Verarbeitungsregel“ einer benutzerdefinierten eVar &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | Keine spezielle Daten-Feed-Spalte. Bei Implementierungen, die nur die Analytics betreffen, verwenden Sie die Daten-Feed-Spalte der benutzerdefinierten eVar, die über die Verarbeitungsregel konfiguriert wurde. |
| Audience Manager | `c_contextdata.media.sdkVersion` (Nur Analytics-Implementierungen) |

## Dimensionselemente

Jedes Element ist die literale Versionszeichenfolge, die bei der Initialisierung von SDK konfiguriert wird. Verwenden Sie ein konsistentes Versionierungsschema für Ihre Implementierungen, damit Versionszeichenfolgen in Berichten vorhersehbar verwendet werden können.

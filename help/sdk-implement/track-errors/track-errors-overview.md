---
seo-title: Überblick
title: Überblick
uuid: d 71429 e 6-ef 8 b -4 ea 2-8491-ff 3 cdbf 4357 f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Überblick{#overview}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Fehlerverfolgung implementieren

1. Verfolgen Sie Medienplayer-Fehler.

   Rufen Sie bei Fehlerereignissen `trackError` mit den Fehlerinformationen auf.

>[!NOTE]
>
>Die Verfolgung von Fehlern im Medienplayer stoppt die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.


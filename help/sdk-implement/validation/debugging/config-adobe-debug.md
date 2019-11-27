---
title: Adobe Debug konfigurieren
description: Hier wird beschrieben, wie Sie Adobe Debug konfigurieren, um Fehler in Media SDK-Implementierungen beheben zu können.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Adobe Debug konfigurieren {#configure-adobe-debug}

## Zugriff auf Adobe Debug {#accessing-adobe-debug}

So greifen Sie auf Adobe Debug zu:

1. Gehen Sie zu [Experience Cloud](https://www.marketing.adobe.com) und erstellen Sie einen neuen Adobe Experience Cloud-Benutzer.

   >[!TIP]
   >
   >Diese Anmeldedaten nicht mit dem Benutzernamen/Passwort überein, mit dem Sie sich bei Adobe Analytics anmelden.

1. Nachdem Sie ein Experience Cloud-Konto eingerichtet haben, wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf Adobe Debug anzufordern.
1. Nachdem der Zugriff gewährt wurde, gehen Sie zu [https://debug.adobe.com](https://debug.adobe.com) und melden Sie sich mit den Anmeldedaten für Experience Cloud an.

   ![](assets/adobe-debug-login.png)

   Das Tool unterstützt folgende Browser:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 9 bis 11

Empfohlen werden die neuesten Versionen von Chrome und Firefox.

## Debug-Proxy {#debug-proxy}

Herunterladen und Konfigurieren des Debug-Proxy:

1. Laden Sie die Debug-Proxy-App unter [App-Downloads](https://debug.adobe.com/#/downloads) herunter.

   Folgende Betriebssysteme werden unterstützt:
   * OS X 10.7 64 Bit (oder höher)
   * Windows 7.1 64 Bit (oder höher)
   ![](assets/debug-proxy-app.png)

1. Der Debug-Proxy-Server wird auf der lokalen Maschine an Port 33284 ausgeführt und als System-Proxy festgelegt.

   Sie müssen möglicherweise je nach Betriebssystem und Browser Ihre Browsereinstellungen anpassen.

## SSL-Zertifikat für Desktops oder Apps herunterladen und installieren {#download-and-install-sSL-desktop}

Wenn Sie Adobe Debug zum ersten Mal ausführen, wird ein eindeutiges SSL-Zertifikat generiert. Wenn Sie HTTPS-Traffic auf Desktops und/oder in Apps unterstützen, müssen Sie unser SSL-Zertifikat herunterladen und installieren.

Laden Sie das SSL-Zertifikat herunter und installieren Sie es:

1. Nachdem Adobe Debug installiert und gestartet wurde, gehen Sie zu [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) und laden Sie das Zertifikat herunter.
1. Importieren Sie das Zertifikat

   **Mac OS**
   1. Doppelklicken Sie auf das CA-Stammzertifikat, um es im Schlüsselbund zu öffnen.
   1. Das CA-Stammzertifikat wird unter „Anmeldung“ angezeigt.
   1. Verschieben Sie das CA-Stammzertifikat per Drag-and-drop zu „System“.
   1. Sie müssen das Zertifikat zu „System“ kopieren, um zu gewährleisten, dass alle Anwender und lokalen Systemprozesse ihm vertrauen.
   1. Öffnen Sie das CA-Stammzertifikat, erweitern Sie „Vertrauen“, wählen Sie „Immer vertrauen“ aus und speichern Sie Ihre Änderungen.
   **Windows**
   1. Führen Sie eine der folgenden Aktionen durch:

      * [Hinzufügen von Zertifikaten zum Truststore vertrauenswürdiger Stammzertifizierungsstellen für einen lokalen Computer](https://technet.microsoft.com/de-de/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Führen Sie für Firefox die Schritte unter [Installation des Stammzertifikats in Mozilla Firefox aus.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Möglicherweise müssen Sie Firefox beenden und erneut öffnen, um die Änderung zu sehen.
    
    **iOS-Geräte**
    1. Legen Sie auf Ihrem iOS-Gerät Adobe Debug als HTTP-Proxy fest, indem Sie auf **[!UICONTROL Einstellungen]** **&gt;** **[!UICONTROL WLAN-Einstellungen]** klicken.
    
    1. Gehen Sie in Safari zu [Debuggen.](https://proxy.debug.adobe.com/ssl)
    
    Safari fordert Sie zur Installation des SSL-Zertifikats auf.

## SSL-Zertifikat auf Ihrem Mobilgerät installieren {#install-sSL-for-mobile-device}

Wenn die HTTPS-Aufrufe in Adobe Debug fehlen, müssen Sie das SSL-Zertifikat für Adobe Debug auf dem Mobilgerät installieren.

### iOS

So installieren Sie das SSL-Zertifikat auf einem iOS-Gerät:

1. Deaktivieren Sie auf Ihrem Laptop den Debug-Proxy und öffnen Sie [Adobe Debug.](https://debug.adobe.com)
1. Führen Sie auf Ihrem iOS-Gerät folgende Schritte durch:
   1. Versetzen Sie das Gerät in den Flugmodus.
   1. Wählen Sie dasselbe WLAN-Signal aus, das auch von Ihrem Laptop verwendet wird.
   1. Legen Sie auf Ihrem Laptop manuell die in der Debug-Proxy-App angezeigte IP und den Port fest.
   1. Öffnen Sie ein Apple Safari-Browser-Fenster.
   1. Gehen Sie zu [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Laden Sie das SSL-Zertifikat herunter und installieren Sie es.

1. Starten Sie auf Ihrem Laptop eine Adobe Debug-Sitzung.
1. Beginnen Sie mit den Tests auf Ihrem iOS-Gerät.

### Android

So installieren Sie das SSL-Zertifikat auf einem Android-Gerät:

1. Deaktivieren Sie auf Ihrem Laptop den Debug-Proxy und öffnen Sie [Adobe Debug.](https://debug.adobe.com)
1. Führen Sie auf Ihrem Android-Gerät folgende Schritte durch:
   1. Versetzen Sie das Gerät in den Flugmodus.
   1. Wählen Sie dasselbe WLAN-Signal aus, das auch von Ihrem Laptop verwendet wird.
   1. Legen Sie auf Ihrem Laptop manuell die in der Debug-Proxy-App angezeigte IP und den Port fest.
   1. Öffnen Sie ein Browser-Fenster.
   1. Gehen Sie zu [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Laden Sie das SSL-Zertifikat herunter und installieren Sie es.

1. Starten Sie auf Ihrem Laptop eine Adobe Debug-Sitzung.
1. Beginnen Sie mit den Tests auf Ihrem Android-Gerät.


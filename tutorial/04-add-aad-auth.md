---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822830"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen. Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten. In diesem Schritt werden Sie die Bibliothek der [Microsoft-Authentifizierungsbibliothek](https://github.com/AzureAD/microsoft-authentication-library-for-js) in die Anwendung integrieren.

1. Erstellen Sie eine neue Datei im Stammverzeichnis namens **config.js** , und fügen Sie den folgenden Code hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    Ersetzen Sie `YOUR_APP_ID_HERE` durch die Anwendungs-ID aus dem Anwendungs Registrierungs Portal.

    > [!IMPORTANT]
    > Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es nun ein guter Zeitpunkt, die **config.js** Datei aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.

1. Öffnen Sie **auth.js** , und fügen Sie den folgenden Code am Anfang der Datei hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a>Implementieren der Anmeldung

In diesem Abschnitt implementieren Sie die `signIn` Funktionen und `signOut` .

1. Ersetzen Sie die vorhandene `signIn`-Funktion durch Folgendes.

    ```javascript
    async function signIn() {
      // Login
      try {
        // Use MSAL to login
        const authResult = await msalClient.loginPopup(msalRequest);
        console.log('id_token acquired at: ' + new Date().toString());
        // Save the account username, needed for token acquisition
        sessionStorage.setItem('msalAccount', authResult.account.username);
        // TEMPORARY
        updatePage(Views.error, {
          message: 'Login successful',
          debug: `Token: ${authResult.accessToken}`
        });
      } catch (error) {
        console.log(error);
        updatePage(Views.error, {
          message: 'Error logging in',
          debug: error
        });
      }
    }
    ```

    In diesem temporären Code wird das Zugriffstoken nach einer erfolgreichen Anmeldung angezeigt.

1. Ersetzen Sie die vorhandene `signOut`-Funktion durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. Speichern Sie die Änderungen, und aktualisieren Sie die Seite. Nachdem Sie sich angemeldet haben, sollte ein Fehler Feld angezeigt werden, in dem das Zugriffstoken angezeigt wird.

## <a name="get-the-users-profile"></a>Abrufen des Benutzerprofils

In diesem Abschnitt verbessern Sie die `signIn` Funktion, um das Zugriffstoken zum Abrufen des Benutzerprofils aus Microsoft Graph zu verwenden.

1. Fügen Sie die folgende Funktion in **auth.js** hinzu, um das Zugriffstoken des Benutzers abzurufen.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. Erstellen Sie eine neue Datei im Stamm des Projekts mit dem Namen **graph.js** , und fügen Sie den folgenden Code hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    Mit diesem Code wird ein Autorisierungsanbieter erstellt, der die `getToken` Methode in **auth.js** umschließt und den Graph-Client mit diesem Anbieter initialisiert.

1. Fügen Sie die folgende Funktion in **graph.js** hinzu, um das Profil des Benutzers abzurufen.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. Ersetzen Sie die vorhandene `signIn`-Funktion durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. Speichern Sie die Änderungen, und aktualisieren Sie die Seite. Nachdem Sie sich angemeldet haben, sollten Sie wieder auf die Startseite zurückkehren, die Benutzeroberfläche sollte jedoch geändert werden, um anzugeben, dass Sie angemeldet sind.

    ![Screenshot der Startseite nach dem Anmelden](./images/user-signed-in.png)

1. Klicken Sie in der oberen rechten Ecke auf den Avatar des Benutzers, um auf den **Abmelde** Link zuzugreifen. Durch Klicken auf **Abmelden** wird die Sitzung zurückgesetzt, und Sie kehren zur Startseite zurück.

    ![Screenshot des Dropdownmenüs mit dem Link zum Abmelden](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a>Speichern und Aktualisieren von Token

Zu diesem Zeitpunkt verfügt Ihre Anwendung über ein Zugriffstoken, das in der `Authorization` Kopfzeile von API-aufrufen gesendet wird. Dies ist das Token, das es der App ermöglicht, im Namen des Benutzers auf Microsoft Graph zuzugreifen.

Dieses Token ist jedoch nur kurzzeitig verfügbar. Das Token läuft eine Stunde nach seiner Ausgabe ab. An dieser Stelle kommt das Aktualisierungstoken ins Spiel. Anhand des Aktualisierungstoken ist die App in der Lage, ein neues Zugriffstoken anzufordern, ohne dass der Benutzer sich erneut anmelden muss.

Da die APP die MSAL-Bibliothek verwendet, müssen Sie keine Token-Speicher-oder Aktualisierungslogik implementieren. MSAL speichert das Token in der Browsersitzung zwischen. Die `acquireTokenSilent` Methode überprüft zuerst das zwischengespeicherte Token, und wenn es nicht abgelaufen ist, wird es zurückgegeben. Wenn er abgelaufen ist, wird das zwischengespeicherte Aktualisierungstoken verwendet, um ein neues zu erhalten. Das Graph-Clientobjekt Ruft die `getToken` Methode in **auth.js** bei jeder Anforderung auf und stellt sicher, dass Sie über einen aktuellen Token verfügt.

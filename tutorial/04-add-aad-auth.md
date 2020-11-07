---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822830"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="19e93-101">In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="19e93-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="19e93-102">Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="19e93-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="19e93-103">In diesem Schritt werden Sie die Bibliothek der [Microsoft-Authentifizierungsbibliothek](https://github.com/AzureAD/microsoft-authentication-library-for-js) in die Anwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="19e93-103">In this step you will integrate the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-js) library into the application.</span></span>

1. <span data-ttu-id="19e93-104">Erstellen Sie eine neue Datei im Stammverzeichnis namens **config.js** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="19e93-104">Create a new file in the root directory named **config.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    <span data-ttu-id="19e93-105">Ersetzen Sie `YOUR_APP_ID_HERE` durch die Anwendungs-ID aus dem Anwendungs Registrierungs Portal.</span><span class="sxs-lookup"><span data-stu-id="19e93-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="19e93-106">Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es nun ein guter Zeitpunkt, die **config.js** Datei aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="19e93-106">If you're using source control such as git, now would be a good time to exclude the **config.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="19e93-107">Öffnen Sie **auth.js** , und fügen Sie den folgenden Code am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="19e93-107">Open **auth.js** and add the following code to the beginning of the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a><span data-ttu-id="19e93-108">Implementieren der Anmeldung</span><span class="sxs-lookup"><span data-stu-id="19e93-108">Implement sign-in</span></span>

<span data-ttu-id="19e93-109">In diesem Abschnitt implementieren Sie die `signIn` Funktionen und `signOut` .</span><span class="sxs-lookup"><span data-stu-id="19e93-109">In this section you'll implement the `signIn` and `signOut` functions.</span></span>

1. <span data-ttu-id="19e93-110">Ersetzen Sie die vorhandene `signIn`-Funktion durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="19e93-110">Replace the existing `signIn` function with the following.</span></span>

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

    <span data-ttu-id="19e93-111">In diesem temporären Code wird das Zugriffstoken nach einer erfolgreichen Anmeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="19e93-111">This temporary code will display the access token after a successful login.</span></span>

1. <span data-ttu-id="19e93-112">Ersetzen Sie die vorhandene `signOut`-Funktion durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="19e93-112">Replace the existing `signOut` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. <span data-ttu-id="19e93-113">Speichern Sie die Änderungen, und aktualisieren Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="19e93-113">Save your changes and refresh the page.</span></span> <span data-ttu-id="19e93-114">Nachdem Sie sich angemeldet haben, sollte ein Fehler Feld angezeigt werden, in dem das Zugriffstoken angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="19e93-114">After you sign in, you should see an error box that shows the access token.</span></span>

## <a name="get-the-users-profile"></a><span data-ttu-id="19e93-115">Abrufen des Benutzerprofils</span><span class="sxs-lookup"><span data-stu-id="19e93-115">Get the user's profile</span></span>

<span data-ttu-id="19e93-116">In diesem Abschnitt verbessern Sie die `signIn` Funktion, um das Zugriffstoken zum Abrufen des Benutzerprofils aus Microsoft Graph zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="19e93-116">In this section you'll improve the `signIn` function to use the access token to get the user's profile from Microsoft Graph.</span></span>

1. <span data-ttu-id="19e93-117">Fügen Sie die folgende Funktion in **auth.js** hinzu, um das Zugriffstoken des Benutzers abzurufen.</span><span class="sxs-lookup"><span data-stu-id="19e93-117">Add the following function in **auth.js** to retrieve the user's access token.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. <span data-ttu-id="19e93-118">Erstellen Sie eine neue Datei im Stamm des Projekts mit dem Namen **graph.js** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="19e93-118">Create a new file in the root of the project named **graph.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    <span data-ttu-id="19e93-119">Mit diesem Code wird ein Autorisierungsanbieter erstellt, der die `getToken` Methode in **auth.js** umschließt und den Graph-Client mit diesem Anbieter initialisiert.</span><span class="sxs-lookup"><span data-stu-id="19e93-119">This code creates an authorization provider that wraps the `getToken` method in **auth.js** , and initializes the Graph client with this provider.</span></span>

1. <span data-ttu-id="19e93-120">Fügen Sie die folgende Funktion in **graph.js** hinzu, um das Profil des Benutzers abzurufen.</span><span class="sxs-lookup"><span data-stu-id="19e93-120">Add the following function in **graph.js** to get the user's profile.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. <span data-ttu-id="19e93-121">Ersetzen Sie die vorhandene `signIn`-Funktion durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="19e93-121">Replace the existing `signIn` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. <span data-ttu-id="19e93-122">Speichern Sie die Änderungen, und aktualisieren Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="19e93-122">Save your changes and refresh the page.</span></span> <span data-ttu-id="19e93-123">Nachdem Sie sich angemeldet haben, sollten Sie wieder auf die Startseite zurückkehren, die Benutzeroberfläche sollte jedoch geändert werden, um anzugeben, dass Sie angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="19e93-123">After you sign in, you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

    ![Screenshot der Startseite nach dem Anmelden](./images/user-signed-in.png)

1. <span data-ttu-id="19e93-125">Klicken Sie in der oberen rechten Ecke auf den Avatar des Benutzers, um auf den **Abmelde** Link zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="19e93-125">Click the user avatar in the top right corner to access the **Sign out** link.</span></span> <span data-ttu-id="19e93-126">Durch Klicken auf **Abmelden** wird die Sitzung zurückgesetzt, und Sie kehren zur Startseite zurück.</span><span class="sxs-lookup"><span data-stu-id="19e93-126">Clicking **Sign out** resets the session and returns you to the home page.</span></span>

    ![Screenshot des Dropdownmenüs mit dem Link zum Abmelden](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="19e93-128">Speichern und Aktualisieren von Token</span><span class="sxs-lookup"><span data-stu-id="19e93-128">Storing and refreshing tokens</span></span>

<span data-ttu-id="19e93-129">Zu diesem Zeitpunkt verfügt Ihre Anwendung über ein Zugriffstoken, das in der `Authorization` Kopfzeile von API-aufrufen gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="19e93-129">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="19e93-130">Dies ist das Token, das es der App ermöglicht, im Namen des Benutzers auf Microsoft Graph zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="19e93-130">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="19e93-131">Dieses Token ist jedoch nur kurzzeitig verfügbar.</span><span class="sxs-lookup"><span data-stu-id="19e93-131">However, this token is short-lived.</span></span> <span data-ttu-id="19e93-132">Das Token läuft eine Stunde nach seiner Ausgabe ab.</span><span class="sxs-lookup"><span data-stu-id="19e93-132">The token expires an hour after it is issued.</span></span> <span data-ttu-id="19e93-133">An dieser Stelle kommt das Aktualisierungstoken ins Spiel.</span><span class="sxs-lookup"><span data-stu-id="19e93-133">This is where the refresh token becomes useful.</span></span> <span data-ttu-id="19e93-134">Anhand des Aktualisierungstoken ist die App in der Lage, ein neues Zugriffstoken anzufordern, ohne dass der Benutzer sich erneut anmelden muss.</span><span class="sxs-lookup"><span data-stu-id="19e93-134">The refresh token allows the app to request a new access token without requiring the user to sign in again.</span></span>

<span data-ttu-id="19e93-135">Da die APP die MSAL-Bibliothek verwendet, müssen Sie keine Token-Speicher-oder Aktualisierungslogik implementieren.</span><span class="sxs-lookup"><span data-stu-id="19e93-135">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="19e93-136">MSAL speichert das Token in der Browsersitzung zwischen.</span><span class="sxs-lookup"><span data-stu-id="19e93-136">MSAL caches the token in the browser session.</span></span> <span data-ttu-id="19e93-137">Die `acquireTokenSilent` Methode überprüft zuerst das zwischengespeicherte Token, und wenn es nicht abgelaufen ist, wird es zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="19e93-137">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="19e93-138">Wenn er abgelaufen ist, wird das zwischengespeicherte Aktualisierungstoken verwendet, um ein neues zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="19e93-138">If it is expired, it uses the cached refresh token to obtain a new one.</span></span> <span data-ttu-id="19e93-139">Das Graph-Clientobjekt Ruft die `getToken` Methode in **auth.js** bei jeder Anforderung auf und stellt sicher, dass Sie über einen aktuellen Token verfügt.</span><span class="sxs-lookup"><span data-stu-id="19e93-139">The Graph client object calls the `getToken` method in **auth.js** on every request, ensuring that it has an up-to-date token.</span></span>

---
ms.openlocfilehash: 9b9b118c2d95710a5a3f9a1afe4d03a6185b4b14
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822850"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="620c2-101">Vorgehensweise Ausführen des abgeschlossenen Projekts</span><span class="sxs-lookup"><span data-stu-id="620c2-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="620c2-102">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="620c2-102">Prerequisites</span></span>

<span data-ttu-id="620c2-103">Um das abgeschlossene Projekt in diesem Ordner auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="620c2-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="620c2-104">[Node.js](https://nodejs.org) auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="620c2-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="620c2-105">Wenn Sie nicht über Node.js verfügen, besuchen Sie den vorherigen Link für Downloadoptionen.</span><span class="sxs-lookup"><span data-stu-id="620c2-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="620c2-106">( **Hinweis:** dieses Lernprogramm wurde mit Node Version 12.16.1 geschrieben.</span><span class="sxs-lookup"><span data-stu-id="620c2-106">( **Note:** This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="620c2-107">Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, aber das wurde nicht getestet.)</span><span class="sxs-lookup"><span data-stu-id="620c2-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="620c2-108">Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto.</span><span class="sxs-lookup"><span data-stu-id="620c2-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="620c2-109">Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="620c2-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="620c2-110">Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="620c2-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="620c2-111">Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="620c2-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="620c2-112">Registrieren einer Webanwendung im Azure-Active Directory Admin Center</span><span class="sxs-lookup"><span data-stu-id="620c2-112">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="620c2-113">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="620c2-113">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="620c2-114">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="620c2-114">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="620c2-115">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="620c2-115">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="620c2-116">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="620c2-116">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

    > <span data-ttu-id="620c2-117">**Hinweis:** Azure AD B2C-Benutzern werden möglicherweise nur **App-Registrierungen (Legacy)** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="620c2-117">**Note:** Azure AD B2C users may only see **App registrations (legacy)**.</span></span> <span data-ttu-id="620c2-118">Wechseln Sie in diesem Fall direkt zu [https://aka.ms/appregistrations](https://aka.ms/appregistrations) .</span><span class="sxs-lookup"><span data-stu-id="620c2-118">In this case, please go directly to [https://aka.ms/appregistrations](https://aka.ms/appregistrations).</span></span>

1. <span data-ttu-id="620c2-119">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="620c2-119">Select **New registration**.</span></span> <span data-ttu-id="620c2-120">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="620c2-120">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="620c2-121">Legen Sie **Name** auf `JavaScript Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="620c2-121">Set **Name** to `JavaScript Graph Tutorial`.</span></span>
    - <span data-ttu-id="620c2-122">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="620c2-122">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="620c2-123">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `http://localhost:8080` fest.</span><span class="sxs-lookup"><span data-stu-id="620c2-123">Under **Redirect URI** , set the first drop-down to `Single-page application (SPA)` and set the value to `http://localhost:8080`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="620c2-125">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="620c2-125">Choose **Register**.</span></span> <span data-ttu-id="620c2-126">Kopieren Sie auf der Seite **JavaScript Graph Tutorial** den Wert der **Anwendungs-ID (Client)** , und speichern Sie Sie, um Sie im nächsten Schritt zu benötigen.</span><span class="sxs-lookup"><span data-stu-id="620c2-126">On the **JavaScript Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="620c2-128">Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="620c2-128">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="620c2-129">Suchen Sie den **impliziten Grant** -Abschnitt, und aktivieren Sie **Zugriffstoken** und **ID-Token**.</span><span class="sxs-lookup"><span data-stu-id="620c2-129">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="620c2-130">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="620c2-130">Choose **Save**.</span></span>

    ![Screenshot des Abschnitts "Implizite Gewährung"](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a><span data-ttu-id="620c2-132">Konfigurieren des Beispiels</span><span class="sxs-lookup"><span data-stu-id="620c2-132">Configure the sample</span></span>

1. <span data-ttu-id="620c2-133">Benennen Sie die Datei **./Graph-Tutorial/config.example.js** in **./Graph-Tutorial/config.js** um.</span><span class="sxs-lookup"><span data-stu-id="620c2-133">Rename the **./graph-tutorial/config.example.js** file to **./graph-tutorial/config.js**.</span></span>
1. <span data-ttu-id="620c2-134">Bearbeiten Sie die Datei **./Graph-Tutorial/config.js** , und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="620c2-134">Edit the **./graph-tutorial/config.js** file and make the following changes.</span></span>
    1. <span data-ttu-id="620c2-135">Ersetzen `YOUR_APP_ID_HERE` Sie durch die **Anwendungs-ID** , die Sie im App-Registrierungs Portal erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="620c2-135">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="620c2-136">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="620c2-136">Run the sample</span></span>

1. <span data-ttu-id="620c2-137">Führen Sie den folgenden Befehl in der CLI aus, um die Anwendung zu starten.</span><span class="sxs-lookup"><span data-stu-id="620c2-137">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="620c2-138">Öffnen Sie einen Browser, und navigieren Sie zu `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="620c2-138">Open a browser and browse to `http://localhost:8080`.</span></span>

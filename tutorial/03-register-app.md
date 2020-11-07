---
ms.openlocfilehash: a89e87b24962caedf35463f1e3a4d7bbf91aa562
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822821"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="396fb-101">In dieser Übung erstellen Sie mithilfe des Azure Active Directory Admin Center eine neue Azure AD-Webanwendungs Registrierung.</span><span class="sxs-lookup"><span data-stu-id="396fb-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="396fb-102">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="396fb-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="396fb-103">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="396fb-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="396fb-104">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="396fb-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="396fb-105">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="396fb-105">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

    > [!NOTE]
    > <span data-ttu-id="396fb-106">Azure AD B2C-Benutzern werden möglicherweise nur **App-Registrierungen (Legacy)** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="396fb-106">Azure AD B2C users may only see **App registrations (legacy)**.</span></span> <span data-ttu-id="396fb-107">Wechseln Sie in diesem Fall direkt zu [https://aka.ms/appregistrations](https://aka.ms/appregistrations) .</span><span class="sxs-lookup"><span data-stu-id="396fb-107">In this case, please go directly to [https://aka.ms/appregistrations](https://aka.ms/appregistrations).</span></span>

1. <span data-ttu-id="396fb-108">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="396fb-108">Select **New registration**.</span></span> <span data-ttu-id="396fb-109">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="396fb-109">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="396fb-110">Legen Sie **Name** auf `JavaScript Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="396fb-110">Set **Name** to `JavaScript Graph Tutorial`.</span></span>
    - <span data-ttu-id="396fb-111">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="396fb-111">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="396fb-112">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `http://localhost:8080` fest.</span><span class="sxs-lookup"><span data-stu-id="396fb-112">Under **Redirect URI** , set the first drop-down to `Single-page application (SPA)` and set the value to `http://localhost:8080`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](./images/aad-register-an-app.png)

1. <span data-ttu-id="396fb-114">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="396fb-114">Choose **Register**.</span></span> <span data-ttu-id="396fb-115">Kopieren Sie auf der Seite **JavaScript Graph Tutorial** den Wert der **Anwendungs-ID (Client)** , und speichern Sie Sie, um Sie im nächsten Schritt zu benötigen.</span><span class="sxs-lookup"><span data-stu-id="396fb-115">On the **JavaScript Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](./images/aad-application-id.png)

---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822822"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9c08e-101">In diesem Lernprogramm erfahren Sie, wie Sie eine Einzel seitige JavaScript-app erstellen, die die Microsoft Graph-API zum Abrufen von Kalenderinformationen für einen Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="9c08e-101">This tutorial teaches you how to build a JavaScript single-page app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="9c08e-102">Wenn Sie das fertige Lernprogramm einfach herunterladen möchten, können Sie das GitHub- [Repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa)herunterladen oder Klonen.</span><span class="sxs-lookup"><span data-stu-id="9c08e-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c08e-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="9c08e-103">Prerequisites</span></span>

<span data-ttu-id="9c08e-104">Bevor Sie mit diesem Lernprogramm beginnen, benötigen Sie Zugriff auf einen HTTP-Server, um die Beispieldateien zu hosten.</span><span class="sxs-lookup"><span data-stu-id="9c08e-104">Before you start this tutorial, you will need access to an HTTP server to host the sample files.</span></span> <span data-ttu-id="9c08e-105">Dies kann ein Testserver auf dem Entwicklungscomputer oder ein Remoteserver sein.</span><span class="sxs-lookup"><span data-stu-id="9c08e-105">This could be a test server on your development machine, or a remote server.</span></span> <span data-ttu-id="9c08e-106">Das Lernprogramm enthält Anweisungen zur Verwendung eines Node.js Pakets zum Ausführen eines einfachen Testservers auf dem Entwicklungscomputer.</span><span class="sxs-lookup"><span data-stu-id="9c08e-106">The tutorial includes instructions to use a Node.js package to run a simple test server on your development machine.</span></span> <span data-ttu-id="9c08e-107">Wenn Sie diese Option verwenden möchten, sollten Sie [Node.js](https://nodejs.org) auf dem Entwicklungscomputer installiert haben.</span><span class="sxs-lookup"><span data-stu-id="9c08e-107">If you plan to use this option, you should have [Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="9c08e-108">Wenn Sie nicht über Node.js verfügen, besuchen Sie den vorherigen Link für Downloadoptionen.</span><span class="sxs-lookup"><span data-stu-id="9c08e-108">If you do not have Node.js, visit the previous link for download options.</span></span>

<span data-ttu-id="9c08e-109">Sie sollten auch über ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto verfügen.</span><span class="sxs-lookup"><span data-stu-id="9c08e-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="9c08e-110">Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="9c08e-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="9c08e-111">Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="9c08e-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="9c08e-112">Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="9c08e-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9c08e-113">Dieses Lernprogramm wurde mit Node Version 12.16.1 geschrieben.</span><span class="sxs-lookup"><span data-stu-id="9c08e-113">This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="9c08e-114">Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.</span><span class="sxs-lookup"><span data-stu-id="9c08e-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="9c08e-115">Feedback</span><span class="sxs-lookup"><span data-stu-id="9c08e-115">Feedback</span></span>

<span data-ttu-id="9c08e-116">Geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa)an.</span><span class="sxs-lookup"><span data-stu-id="9c08e-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>

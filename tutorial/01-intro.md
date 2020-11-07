---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822822"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Lernprogramm erfahren Sie, wie Sie eine Einzel seitige JavaScript-app erstellen, die die Microsoft Graph-API zum Abrufen von Kalenderinformationen für einen Benutzer verwendet.

> [!TIP]
> Wenn Sie das fertige Lernprogramm einfach herunterladen möchten, können Sie das GitHub- [Repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa)herunterladen oder Klonen.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit diesem Lernprogramm beginnen, benötigen Sie Zugriff auf einen HTTP-Server, um die Beispieldateien zu hosten. Dies kann ein Testserver auf dem Entwicklungscomputer oder ein Remoteserver sein. Das Lernprogramm enthält Anweisungen zur Verwendung eines Node.js Pakets zum Ausführen eines einfachen Testservers auf dem Entwicklungscomputer. Wenn Sie diese Option verwenden möchten, sollten Sie [Node.js](https://nodejs.org) auf dem Entwicklungscomputer installiert haben. Wenn Sie nicht über Node.js verfügen, besuchen Sie den vorherigen Link für Downloadoptionen.

Sie sollten auch über ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto verfügen. Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:

- Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.

> [!NOTE]
> Dieses Lernprogramm wurde mit Node Version 12.16.1 geschrieben. Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.

## <a name="feedback"></a>Feedback

Geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa)an.

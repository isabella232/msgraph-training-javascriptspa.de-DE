---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822865"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Abschnitt können Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzufügen.

## <a name="create-a-new-event-form"></a>Erstellen eines neuen Ereignis Formulars

1. Fügen Sie die folgende Funktion zu **ui.js** hinzu, um ein Formular für das neue Ereignis zu rendern.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a>Erstellen des Ereignisses

1. Fügen Sie die folgende Funktion zu **graph.js** hinzu, um die Werte aus dem Formular zu lesen und ein neues Ereignis zu erstellen.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. Speichern Sie Ihre Änderungen, und aktualisieren Sie die app. Klicken Sie auf das Navigationselement **Kalender** , und klicken Sie dann auf die Schaltfläche **Ereignis erstellen** . Geben Sie die Werte ein, und klicken Sie auf **Erstellen**. Die APP kehrt zur Kalenderansicht zurück, wenn das neue Ereignis erstellt wird.

    ![Screenshot des neuen Ereignis Formulars](images/create-event-01.png)

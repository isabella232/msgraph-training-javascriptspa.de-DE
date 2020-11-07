---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822865"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c1a01-101">In diesem Abschnitt können Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c1a01-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-a-new-event-form"></a><span data-ttu-id="c1a01-102">Erstellen eines neuen Ereignis Formulars</span><span class="sxs-lookup"><span data-stu-id="c1a01-102">Create a new event form</span></span>

1. <span data-ttu-id="c1a01-103">Fügen Sie die folgende Funktion zu **ui.js** hinzu, um ein Formular für das neue Ereignis zu rendern.</span><span class="sxs-lookup"><span data-stu-id="c1a01-103">Add the following function to **ui.js** to render a form for the new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a><span data-ttu-id="c1a01-104">Erstellen des Ereignisses</span><span class="sxs-lookup"><span data-stu-id="c1a01-104">Create the event</span></span>

1. <span data-ttu-id="c1a01-105">Fügen Sie die folgende Funktion zu **graph.js** hinzu, um die Werte aus dem Formular zu lesen und ein neues Ereignis zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1a01-105">Add the following function to **graph.js** to read the values from the form and create a new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. <span data-ttu-id="c1a01-106">Speichern Sie Ihre Änderungen, und aktualisieren Sie die app.</span><span class="sxs-lookup"><span data-stu-id="c1a01-106">Save your changes and refresh the app.</span></span> <span data-ttu-id="c1a01-107">Klicken Sie auf das Navigationselement **Kalender** , und klicken Sie dann auf die Schaltfläche **Ereignis erstellen** .</span><span class="sxs-lookup"><span data-stu-id="c1a01-107">Click the **Calendar** nav item, then click the **Create event** button.</span></span> <span data-ttu-id="c1a01-108">Geben Sie die Werte ein, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c1a01-108">Fill in the values and click **Create**.</span></span> <span data-ttu-id="c1a01-109">Die APP kehrt zur Kalenderansicht zurück, wenn das neue Ereignis erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c1a01-109">The app returns to the calendar view once the new event is created.</span></span>

    ![Screenshot des neuen Ereignis Formulars](images/create-event-01.png)

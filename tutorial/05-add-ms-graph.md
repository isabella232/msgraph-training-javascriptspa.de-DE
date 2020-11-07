---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822858"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="55bec-101">In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="55bec-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="55bec-102">Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliotheks](https://github.com/microsoftgraph/msgraph-sdk-javascript) Bibliothek, um Anrufe an Microsoft Graph vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="55bec-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="55bec-103">Abrufen von Kalenderereignissen von Outlook</span><span class="sxs-lookup"><span data-stu-id="55bec-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="55bec-104">In diesem Abschnitt verwenden Sie die Microsoft Graph-Clientbibliothek, um Kalenderereignisse für den Benutzer abzurufen.</span><span class="sxs-lookup"><span data-stu-id="55bec-104">In this section, you'll use the Microsoft Graph client library to get calendar events for the user.</span></span>

1. <span data-ttu-id="55bec-105">Erstellen Sie eine neue Datei im Stamm des Projekts mit dem Namen **timezones.js** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="55bec-105">Create a new file in the root of the project named **timezones.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    <span data-ttu-id="55bec-106">Mit diesem Code werden der IANA-Zeitzonenbezeichner Windows-Zeitzonenbezeichner für die Kompatibilität mit moment.js zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="55bec-106">This code maps Windows time zone identifiers to IANA time zone identifiers for compatibility with moment.js.</span></span>

1. <span data-ttu-id="55bec-107">Fügen Sie die folgende Funktion zu **graph.js** hinzu.</span><span class="sxs-lookup"><span data-stu-id="55bec-107">Add the following function to **graph.js**.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    <span data-ttu-id="55bec-108">Überlegen Sie sich, was dieser Code macht.</span><span class="sxs-lookup"><span data-stu-id="55bec-108">Consider what this code is doing.</span></span>

    - <span data-ttu-id="55bec-109">Die URL, die aufgerufen wird, lautet `/me/calendarview`.</span><span class="sxs-lookup"><span data-stu-id="55bec-109">The URL that will be called is `/me/calendarview`.</span></span>
    - <span data-ttu-id="55bec-110">Durch die `header` -Methode wird eine Kopfzeile hinzugefügt `Prefer` , die die bevorzugte Zeitzone des Benutzers angibt.</span><span class="sxs-lookup"><span data-stu-id="55bec-110">The `header` method adds a `Prefer` header specifying the user's preferred time zone.</span></span>
    - <span data-ttu-id="55bec-111">Die `query` -Methode fügt die Anfangs-und Endzeiten für die Kalenderansicht hinzu.</span><span class="sxs-lookup"><span data-stu-id="55bec-111">The `query` method adds the start and end times for the calendar view.</span></span>
    - <span data-ttu-id="55bec-112">Die `select` -Methode schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf genau diejenigen ein, die die Ansicht tatsächlich verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="55bec-112">The `select` method limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="55bec-113">Die `orderby` -Methode sortiert die Ergebnisse nach der Anfangszeit, wobei das früheste Ereignis zuerst ist.</span><span class="sxs-lookup"><span data-stu-id="55bec-113">The `orderby` method sorts the results by the start time, with the earliest event being first.</span></span>
    - <span data-ttu-id="55bec-114">Die `top` -Methode fordert in der Antwort bis zu 50 Ereignisse an.</span><span class="sxs-lookup"><span data-stu-id="55bec-114">The `top` method requests up to 50 events in the response.</span></span>

1. <span data-ttu-id="55bec-115">Öffnen Sie **ui.js** , und fügen Sie die folgende Funktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="55bec-115">Open **ui.js** and add the following function.</span></span>

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. <span data-ttu-id="55bec-116">Aktualisieren `switch` Sie die Anweisung in der `updatePage` Funktion, die aufgerufen werden soll, `showCalendar` Wenn sich die Ansicht befindet `Views.calendar` .</span><span class="sxs-lookup"><span data-stu-id="55bec-116">Update the `switch` statement in the `updatePage` function to call `showCalendar` when the view is `Views.calendar`.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. <span data-ttu-id="55bec-117">Speichern Sie Ihre Änderungen, und aktualisieren Sie die app.</span><span class="sxs-lookup"><span data-stu-id="55bec-117">Save your changes and refresh the app.</span></span> <span data-ttu-id="55bec-118">Melden Sie sich an, und klicken Sie in der Navigationsleiste auf den Link **Kalender** .</span><span class="sxs-lookup"><span data-stu-id="55bec-118">Sign in and click the **Calendar** link in the nav bar.</span></span> <span data-ttu-id="55bec-119">Wenn alles funktioniert, sollte ein JSON-Abbild von Ereignissen im Kalender des Benutzers angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="55bec-119">If everything works, you should see a JSON dump of events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="55bec-120">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="55bec-120">Display the results</span></span>

<span data-ttu-id="55bec-121">In diesem Abschnitt aktualisieren Sie die `showCalendar` -Funktion so, dass die Ereignisse benutzerfreundlicher angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="55bec-121">In this section you will update the `showCalendar` function to display the events in a more user-friendly manner.</span></span>

1. <span data-ttu-id="55bec-122">Ersetzen Sie die vorhandene `showCalendar`-Funktion durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="55bec-122">Replace the existing `showCalendar` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    <span data-ttu-id="55bec-123">Dadurch wird die Auflistung von Ereignissen durchlaufen, und für jede einzelne Tabelle wird eine Tabellenzeile hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="55bec-123">This loops through the collection of events and adds a table row for each one.</span></span>

1. <span data-ttu-id="55bec-124">Speichern Sie die Änderungen, und aktualisieren Sie die app.</span><span class="sxs-lookup"><span data-stu-id="55bec-124">Save the changes and refresh the app.</span></span> <span data-ttu-id="55bec-125">Klicken Sie auf den Link **Kalender** , und die APP sollte jetzt eine Tabelle mit Ereignissen für die aktuelle Woche rendern.</span><span class="sxs-lookup"><span data-stu-id="55bec-125">Click on the **Calendar** link and the app should now render a table of events for the current week.</span></span>

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/calendar-list.png)

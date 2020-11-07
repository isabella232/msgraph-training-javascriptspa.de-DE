---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822858"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren. Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliotheks](https://github.com/microsoftgraph/msgraph-sdk-javascript) Bibliothek, um Anrufe an Microsoft Graph vorzunehmen.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen von Outlook

In diesem Abschnitt verwenden Sie die Microsoft Graph-Clientbibliothek, um Kalenderereignisse für den Benutzer abzurufen.

1. Erstellen Sie eine neue Datei im Stamm des Projekts mit dem Namen **timezones.js** , und fügen Sie den folgenden Code hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    Mit diesem Code werden der IANA-Zeitzonenbezeichner Windows-Zeitzonenbezeichner für die Kompatibilität mit moment.js zugeordnet.

1. Fügen Sie die folgende Funktion zu **graph.js** hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    Überlegen Sie sich, was dieser Code macht.

    - Die URL, die aufgerufen wird, lautet `/me/calendarview`.
    - Durch die `header` -Methode wird eine Kopfzeile hinzugefügt `Prefer` , die die bevorzugte Zeitzone des Benutzers angibt.
    - Die `query` -Methode fügt die Anfangs-und Endzeiten für die Kalenderansicht hinzu.
    - Die `select` -Methode schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf genau diejenigen ein, die die Ansicht tatsächlich verwendet wird.
    - Die `orderby` -Methode sortiert die Ergebnisse nach der Anfangszeit, wobei das früheste Ereignis zuerst ist.
    - Die `top` -Methode fordert in der Antwort bis zu 50 Ereignisse an.

1. Öffnen Sie **ui.js** , und fügen Sie die folgende Funktion hinzu.

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

1. Aktualisieren `switch` Sie die Anweisung in der `updatePage` Funktion, die aufgerufen werden soll, `showCalendar` Wenn sich die Ansicht befindet `Views.calendar` .

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. Speichern Sie Ihre Änderungen, und aktualisieren Sie die app. Melden Sie sich an, und klicken Sie in der Navigationsleiste auf den Link **Kalender** . Wenn alles funktioniert, sollte ein JSON-Abbild von Ereignissen im Kalender des Benutzers angezeigt werden.

## <a name="display-the-results"></a>Anzeigen der Ergebnisse

In diesem Abschnitt aktualisieren Sie die `showCalendar` -Funktion so, dass die Ereignisse benutzerfreundlicher angezeigt werden.

1. Ersetzen Sie die vorhandene `showCalendar`-Funktion durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    Dadurch wird die Auflistung von Ereignissen durchlaufen, und für jede einzelne Tabelle wird eine Tabellenzeile hinzugefügt.

1. Speichern Sie die Änderungen, und aktualisieren Sie die app. Klicken Sie auf den Link **Kalender** , und die APP sollte jetzt eine Tabelle mit Ereignissen für die aktuelle Woche rendern.

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/calendar-list.png)

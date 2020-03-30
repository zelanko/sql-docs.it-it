---
title: Aggiunta di funzionalità tramite l'estendibilità
titleSuffix: Azure Data Studio
description: Informazioni sul modello di estendibilità e sulle principali aree di estendibilità per ampliare le funzionalità di Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: b263c3890ab9a03295212c723adad4a431fbf04f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76928002"
---
# <a name="getting-started-with-name-sos-extensibility"></a>Introduzione all'estendibilità di [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos.md)] include vari meccanismi di estendibilità per personalizzare l'esperienza utente e rendere le personalizzazioni disponibili per l'intera community di utenti. La piattaforma principale di [!INCLUDE[name-sos](../includes/name-sos.md)] è basata su Visual Studio Code ed è quindi disponibile la maggior parte delle API di estendibilità Visual Studio Code. Sono stati inoltre realizzati punti di estendibilità aggiuntivi per le attività specifiche di gestione dei dati.

I principali punti di estendibilità principali includono:

- API di estendibilità di Visual Studio Code
- Strumenti per la creazione di estensioni di Azure Data Studio
- Contributi ai panelli della scheda di gestione del dashboard
- Informazioni dettagliate con strumenti di azione
- API di estendibilità Azure Data Studio
- API di provider di dati personalizzati

## <a name="visual-studio-code-extensibility-apis"></a>API di estendibilità di Visual Studio Code

La piattaforma principale di [!INCLUDE[name-sos](../includes/name-sos.md)] è basata su Visual Studio Code e, per informazioni dettagliate sulle API di estendibilità di Visual Studio Code, è quindi possibile consultare gli articoli [Creazione di estensioni](https://code.visualstudio.com/docs/extensions/overview) e [API di estensione](https://code.visualstudio.com/docs/extensionAPI/overview) disponibili nel sito Web di Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Contributi ai panelli della scheda di gestione del dashboard

Per informazioni dettagliate, vedere [Punti di aggiunta contributi](#contribution-points) e [Variabili di contesto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>API di estendibilità Azure Data Studio

Per informazioni dettagliate, vedere [API di estendibilità](extensibility-apis.md).


## <a name="contribution-points"></a>Punti di aggiunta contributi

In questa sezione vengono illustrati i vari punti di aggiunta di contributi definiti nel manifesto dell'estensione package.json.

IntelliSense è supportato in azuredatastudio.

## <a name="contributes-dashboard"></a>Dashboard dei contributi

Scheda dei contributi, contenitore, widget di informazioni dettagliate nel dashboard.

![Dashboard](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs consente di creare sezioni delle schede nella pagina del dashboard. Prevede un oggetto o una matrice di oggetti.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

Anziché specificare il contenitore di dashboard inline (all'interno di dashboard.tab), è possibile registrare i contenitori con dashboard.containers. Accetta un oggetto o una matrice di oggetti.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

Per fare riferimento al contenitore registrato, specificare l'ID del contenitore

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

È possibile registrare informazioni dettagliate con dashboard.insights. Questa procedura è simile a quella illustrata in [Esercitazione: Creare un widget di informazioni dettagliate personalizzato](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>Tipi di contenitori di dashboard

Sono attualmente disponibili quattro tipi di contenitori supportati:

1. `widgets-container`

    ![Contenitore di widget](media/extensibility/widgets-container.png)

    Elenco dei widget che verranno visualizzati nel contenitore. Si tratta di un layout di flusso e accetta l'elenco di widget.

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![contenitore visualizzazione Web](media/extensibility/webview-container.png)

    La visualizzazione Web verrà visualizzata nell'intero contenitore. L'ID della visualizzazione Web deve essere identico all'ID della scheda

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![contenitore griglia](media/extensibility/grid-container.png)

   Elenco dei widget o delle visualizzazioni Web che verranno visualizzati nel layout griglia.

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![Sezione nav](media/extensibility/nav-section.png)

    La sezione di navigazione verrà visualizzata nel contenitore

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>Variabili di contesto

Per informazioni generali sul contesto in Visual Studio Code e quindi in Azure Data Studio, vedere [Estendibilità](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

In Azure Data Studio, per le estensioni è disponibile un contesto specifico per le connessioni al database.

### <a name="dashboard"></a>Dashboard

Nel dashboard vengono fornite le variabili di contesto seguenti:

|variabile di contesto| description|
|:---|:---|
|`connectionProvider` | Stringa dell'identificatore relativo al provider della connessione corrente. Ex. `connectionProvider == 'MSSQL'`.|
|`serverName`|Stringa del nome di server della connessione corrente. Ex. `serverName == 'localhost'`.|
|`databaseName` | Stringa del nome di database della connessione corrente. Ex. `databaseName == 'master'`.|
|`connection` | Profilo di connessione completo per la connessione corrente (IConnectionProfile)|
|`dashboardContext` | Stringa del contesto della pagina del dashboard attualmente attiva: "database" o "server". Ex. `dashboardContext == 'database'`|

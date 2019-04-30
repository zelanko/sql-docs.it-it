---
title: Aggiunta di ulteriori funzionalità tramite extensibility
titleSuffix: Azure Data Studio
description: Informazioni sul modello estendibilità e aree di estendibilità fondamentali per estendere le funzionalità di Studio dei dati di Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b595a353859ed7d69ccb6ad61ef6e5dc2a7073f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238987"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>Guida introduttiva a [!INCLUDE[name-sos](../includes/name-sos-short.md)] extensibility

[!INCLUDE[name-sos](../includes/name-sos.md)] dispone di diversi meccanismi di estendibilità per personalizzare l'esperienza utente e rendere disponibili tali personalizzazioni alla Comunità di utenti intero. Il nucleo [!INCLUDE[name-sos](../includes/name-sos.md)] piattaforma si basa su Visual Studio Code, in modo che la maggior parte delle API di estensibilità di Visual Studio Code sono disponibile. Inoltre, sono stati forniti i punti di estendibilità aggiuntive per attività di gestione specifici dei dati.

Alcuni dei punti di estendibilità principali sono:

- Extensibility di Visual Studio Code API
- Estensione di Azure Data Studio gli strumenti di creazione
- Gestire i contributi di pannello scheda Dashboard
- Informazioni dettagliate con esperienze di azioni
- API di estendibilità Data Studio Azure
- API del Provider di dati personalizzati

## <a name="visual-studio-code-extensibility-apis"></a>Extensibility di Visual Studio Code API

Poiché il nucleo [!INCLUDE[name-sos](../includes/name-sos.md)] piattaforma si basa su Visual Studio Code, i dettagli sulle API di estensibilità di Visual Studio Code sono disponibili nel [Extension Authoring](https://code.visualstudio.com/docs/extensions/overview) e [API di estensione](https://code.visualstudio.com/docs/extensionAPI/overview) documentazione sul sito Web di Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Gestire i contributi di pannello scheda Dashboard

Per informazioni dettagliate, vedere [contributo punti](#contribution-points) e [variabili di contesto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>API di estendibilità Data Studio Azure

Per informazioni dettagliate, vedere [API di estendibilità](extensibility-apis.md).


## <a name="contribution-points"></a>Punti di aggiunta contributo

Questa sezione descrive i vari punti contributo definiti nel manifesto di estensione del file package. JSON.

IntelliSense è supportata all'interno di azuredatastudio.

## <a name="contributes-dashboard"></a>Contribuisce dashboard

Contribuire con tab, contenitore, il widget insight al dashboard.

![Dashboard](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.Tabs crea le sezioni della scheda all'interno della pagina dashboard. È previsto che un oggetto o una matrice di oggetti.  

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

Anziché specificare dashboard contenitore inline (all'interno di dashboard.tab). È possibile registrare i contenitori usando dashboard.containers. Accetta un oggetto o una matrice dell'oggetto.

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

Per fare riferimento al contenitore registrato, specificare l'id del contenitore

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

È possibile registrare informazioni dettagliate usando dashboard.insights. È simile alla [esercitazione: Compilare un widget insight personalizzato](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

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


### <a name="dashboard-container-types"></a>Tipi di contenitori del dashboard

Esistono attualmente quattro tipi di contenitore supportati:

1. `widgets-container`

    ![Contenitore i widget](media/extensibility/widgets-container.png)

    L'elenco di widget che verrà visualizzato nel contenitore. È un layout di flusso. Accetta l'elenco di widget.

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

    ![contenitore di visualizzazione Web](media/extensibility/webview-container.png)

    La visualizzazione Web verrà visualizzata nell'intero contenitore. È previsto che l'id di webview per essere lo stesso ID scheda

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![contenitore della griglia](media/extensibility/grid-container.png)

   L'elenco di widget o di visualizzazioni Web che verrà visualizzato nel layout della griglia

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

    ![sezione NAV](media/extensibility/nav-section.png)

    La sezione di spostamento verrà visualizzata nel contenitore

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

Per informazioni generali sul contesto in Visual Studio Code e, successivamente, Azure Data Studio, vedere [estendibilità](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

In Azure Data Studio, abbiamo un contesto specifico per le connessioni di database disponibile per le estensioni.

### <a name="dashboard"></a>Dashboard

Nel dashboard, sono disponibili le seguenti variabili di contesto:

|variabile di contesto| description|
|:---|:---|
|`connectionProvider` | Stringa dell'identificatore per il provider della connessione corrente. Ex. `connectionProvider == 'MSSQL'` (Indici per tabelle con ottimizzazione per la memoria).|
|`serverName`|Stringa del nome del server della connessione corrente. Ex. `serverName == 'localhost'` (Indici per tabelle con ottimizzazione per la memoria).|
|`databaseName` | Stringa del nome del database della connessione corrente. Ex. `databaseName == 'master'` (Indici per tabelle con ottimizzazione per la memoria).|
|`connection` | L'oggetto profilo di connessione completa per la connessione corrente (IConnectionProfile)|
|`dashboardContext` | Una stringa del contesto della pagina del dashboard è attivo. 'Database' o 'server'. Ex. `dashboardContext == 'database'`|

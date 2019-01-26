---
title: Accedere rapidamente alle informazioni dettagliate e attività comuni
titleSuffix: Azure Data Studio
description: Informazioni sulla visualizzazione dei widget nel dashboard del database in Azure Data Studio.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 26e93209e2cbd9809d607f90c7eff4da32d2cd98
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045030"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Dashboard in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Per visualizzare un dashboard, pulsante destro del mouse un server o database e selezionare **Gestisci**.

![Dashboard di esempio](media/dashboards/sample-dashboard.png)

**Proprietà server** contiene le proprietà del server, inclusi versione, edizione, nome del Computer e versione del sistema operativo.

**Attività** contiene attività commons come nuova Query e di ripristino.

**I database di ricerca** cercare facilmente i database esistenti archiviati nel server, incluse le tabelle.

**Stato backup** cercare facilmente lo stato del backup per i database esistenti.

## <a name="configuring-insight-widgets"></a>Configurazione widget Insight
Si consiglia vivamente di seguire l'esercitazione per la configurazione di dashboard, che può essere recuperato [qui](tutorial-build-custom-insight-sql-server.md).

Inoltre, assicurarsi di consultare il [pratici sulla configurazione del widget insight]().

Dopo aver seguito questa esercitazione, continuare a leggere per altre informazioni sui widget specifici che non vengono analizzati in questa esercitazione.

## <a name="insight-detail"></a>Dettaglio Insight
Il riquadro a comparsa dettagli Insight fornisce informazioni più dettagliate per un widget insight correlati. 
- Un widget Insight esegue il rendering di una visualizzazione riepilogativa a immediata con conteggio, riga, grafico e così via. 
- Il riquadro a comparsa dettagli Insight fornisce dettagli "drill in", elenco approfondite dei dati per ciascun elemento elencato nel widget Insight di alto livello. 
  - Il contenuto del riquadro a comparsa dettagli è definito con una query SQL separata alla query del widget principale.

Non è necessario impostare per una query dei dettagli di informazioni dettagliate, ma il layout è standard.
- Nella metà superiore della visualizzazione è sempre una visualizzazione "riepilogo" 2-colonna. Le colonne da usare sono definite dalle proprietà "label" e "value" della configurazione di JSON
- Facendo clic su una riga nella tabella di riepilogo, nella parte inferiore della metà del controllo flyout elencherà il set completo di informazioni sulla colonna per la riga.

### <a name="insight-detail-configuration-in-packagejson"></a>Configurazione di dettaglio Insight in package. JSON

Configurazione di esempio Insight dettagli riquadro a comparsa
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```

|proprietà|Tipo|Valore|Valore predefinito|description|comment|
|:---|:---|:---|:---|:---|:---|
|dettagli|oggetto JSON|||proprietà obbligatorie per definire le definizioni di dettaglio insight all'interno della struttura||
|queryFile|string|||il percorso del file query sql detail informazioni dettagliate e il nome relativo al percorso del file package. JSON||
|Etichetta|oggetto JSON|||proprietà obbligatorie per definire ogni voce nella visualizzazione elenco riepilogo|in futuro il nome di questa proprietà per modificare, ad esempio 'summaryList'|
|icon|string|||indicare il nome dell'icona per il rendering per ogni elemento della visualizzazione elenco di riepilogo.|verrà documentato elenco (da definire) di icone supportate|
|column|string|||indicare il nome della prima colonna nella visualizzazione elenco di riepilogo dal set di risultati query|in futuro verrà modificato il nome di questa proprietà per nome più intuitiva|
|Valore|string|||indicare il nome della seconda colonna nella visualizzazione elenco di riepilogo dal set di risultati di query. Il valore di questa colonna viene utilizzato per controllare le condizioni e impostare colori per ogni punto di colore elementi di visualizzazione elenco di riepilogo|in futuro verrà modificato il nome di questa proprietà su un valore più intuitiva|
|condizione|oggetto JSON|||definisce il controllo della condizione di valore della colonna e determinare di colore per ogni elemento della visualizzazione elenco di riepilogo||
|if|string|always, equals, notEquals, greaterThan, lessThan, greaterThanOrEquals, lessThanOrEquals||operatore di controllo di condizione|in futuro verrà modificato il nome della proprietà da-operatore|
|equals|string|||valore del controllo di condizione|in futuro verrà modificato il nome della proprietà 'value'|

## <a name="insight-actions"></a>Azioni di Insight
Con un widget insight e i dettagli di informazioni dettagliate, si possono ottenere facilmente un piano d'azione per attenuare un problema o gestire. Ad esempio, si verrà considerare l'esecuzione di DBCC CHECKDB, leggere i log degli errori o ripristinare il database quando un database si trova in un recupero in sospeso. Oppure può essere una delle azioni che si desiderano eseguire.

Usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]della configurazione di azioni di informazioni dettagliate, è possibile mappare un azioni predefinite, ad esempio il ripristino oppure attivare un'azione personalizzata definita con uno script sql.

> Configurazione delle azioni personalizzate usando lo script sql è in fase di sviluppo e non è disponibile nella build di anteprima privata ancora.

## <a name="sample-insight-action-definition"></a>Definizione di azione Insight di esempio

```"actions"{}``` Definisce un'azione di informazioni dettagliate. Azione può essere definita in un ambito specifico, ad esempio ```"server"```, ```"database"``` e così via e [!INCLUDE[name-sos](../includes/name-sos-short.md)] passa le informazioni sul contesto di connessione corrente all'azione.

Ad esempio, quando l'azione di ripristino viene avviata per database WideWorldImporters ```"database": "${Database}"``` indica di definizione per il passaggio ```Database``` valore della colonna nel risultato della query per l'azione di ripristino. Azione di ripristino avvia quindi per il database. ```"types"``` è una matrice json e più azioni possono essere elencate nella matrice. In sostanza diventa un menu di scelta rapida nella finestra di dialogo Dettagli Insight che l'utente può scegliere ed eseguire l'azione. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] Anteprima 0.17.1 ha abilitato "backup", "restore", "nuova query" e "nuovo-database" come tipi di azione.

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```

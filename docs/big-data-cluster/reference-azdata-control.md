---
title: riferimento al controllo azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di controllo azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6fceea54c6ea7d5c904cc27c87033c4a40cff59f
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158216"
---
# <a name="azdata-control"></a>controllo azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Questo articolo è un articolo di riferimento per **azdata**. 

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creazione del controllo azdata](#azdata-control-create) | Creare il piano di controllo.
[eliminazione del controllo azdata](#azdata-control-delete) | Elimina il piano di controllo.
## <a name="azdata-control-create"></a>creazione del controllo azdata
Creazione del piano di controllo: è richiesta la configurazione di Kube nel sistema insieme alle variabili di ambiente seguenti: [' CONTROLLER_USERNAME ',' CONTROLLER_PASSWORD ',' MSSQL_SA_PASSWORD ',' KNOX_PASSWORD '].
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>Esempi
Controllare la distribuzione.
```bash
azdata control create
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del piano di controllo, usato per gli spazi dei nomi kubernetes.
#### `--config-profile -c`
Profilo di configurazione del cluster, usato per la distribuzione del cluster: [' AKS-dev-test ',' kubeadm-prod ',' minikube-dev-test ',' kubeadm-dev-test ']
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". Le condizioni di licenza di questo prodotto sono disponibili in https://aka.ms/azdata-eula.
#### `--node-label -l`
Etichetta del nodo, usata per definire i nodi in cui eseguire la distribuzione.
#### `--force -f`
Forza la creazione, all'utente non viene richiesto di inserire alcun valore e tutti i problemi vengono stampati come parte di stderr.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per i log di debug completi.
## <a name="azdata-control-delete"></a>eliminazione del controllo azdata
Eliminare il piano di controllo: è richiesta la configurazione di Kube nel sistema.
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>Esempi
Controllare la distribuzione.
```bash
azdata control delete
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del piano di controllo, usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--force -f`
Forza il piano di controllo Delete.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

- Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).

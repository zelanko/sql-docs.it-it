---
title: Informazioni di riferimento su azdata context
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata context.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d3506d3ab1b2fad9d07496d1041773d26aae6d68
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733706"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata context list](#azdata-context-list) | Elenca i contesti disponibili nel profilo utente.
[azdata context delete](#azdata-context-delete) | Elimina il contesto con lo spazio dei nomi specificato dal profilo utente.
[azdata context set](#azdata-context-set) | Imposta il contesto con lo spazio dei nomi specificato come contesto attivo nel profilo utente.
## <a name="azdata-context-list"></a>azdata context list
È possibile impostare o eliminare uno qualsiasi di questi con `azdata context set` o `azdata context delete`. Per accedere a un nuovo contesto, usare `azdata login`.
```bash
azdata context list [--active -a] 
                    
```
### <a name="examples"></a>Esempi
Elenco di tutti i contesti disponibili nel profilo utente.
```bash
azdata context list
```
Indicazione del contesto attivo nel profilo utente.
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--active -a`
Elenca solo il contesto attualmente attivo.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-context-delete"></a>azdata context delete
Se il contesto eliminato è attivo, l'utente dovrà impostare un nuovo contesto attivo. Per visualizzare i contesti disponibili per l'impostazione o l'eliminazione, usare `azdata context list`
```bash
azdata context delete --namespace -n 
                      
```
### <a name="examples"></a>Esempi
Eliminare contextNamespace dal profilo utente.
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Spazio dei nomi del contesto che si vuole eliminare.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-context-set"></a>azdata context set
Per visualizzare i contesti disponibili per l'impostazione, usare `azdata context list`. Se non viene elencato alcun contesto, è necessario eseguire l'accesso con `azdata login` per creare un contesto nel profilo utente. L'entità a cui si accede diventerà il contesto attivo. Se si accede a più entità, sarà possibile usare questo comando per passare da un contesto attivo a un altro. Per visualizzare il contesto attivo corrente, usare `azdata context list --active`
```bash
azdata context set --namespace -n 
                   
```
### <a name="examples"></a>Esempi
Imposta contextNamespace come contesto attivo nel profilo utente.
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Spazio dei nomi del contesto che si vuole impostare.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](../install/deploy-install-azdata.md).

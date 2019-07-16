---
title: riferimento di integrazione applicativa dei dati mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di mssqlctl integrazione applicativa dei dati.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a9da2de60248246bee3daeeaee40d3071da69c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957951"
---
# <a name="mssqlctl-bdc"></a>mssqlctl integrazione applicativa dei dati

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **bdc** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creare mssqlctl integrazione applicativa dei dati](#mssqlctl-bdc-create) | Creare Cluster di Big Data.
[eliminazione di integrazione applicativa dei dati mssqlctl](#mssqlctl-bdc-delete) | Eliminare Cluster di Big Data.
[mssqlctl bdc config](reference-mssqlctl-bdc-config.md) | Comandi di configurazione.
[endpoint di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-endpoint.md) | Comandi dell'endpoint.
[stato di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-status.md) | Comandi di stato.
[debug di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-debug.md) | I comandi di debug.
[pool di archiviazione di mssqlctl integrazione applicativa dei dati](reference-mssqlctl-bdc-storage-pool.md) | Comandi dei pool di archiviazione.
[controllo di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-control.md) | Comandi del controllo.
[pool di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-pool.md) | Comandi dei pool.
## <a name="mssqlctl-bdc-create"></a>creare mssqlctl integrazione applicativa dei dati
Creare un Cluster di dati SQL Server Big - configurazione kube è necessaria per il sistema con le seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl bdc create [--config-profile -c] 
                    [--accept-eula -a]  
                    [--node-label -l]  
                    [--force -f]
```
### <a name="examples"></a>Esempi
Esperienza di distribuzione guidata integrazione applicativa dei dati - si riceveranno istruzioni per i valori necessari.
```bash
mssqlctl bdc create
```
Distribuzione di integrazione applicativa dei dati con gli argomenti.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test
```
Distribuzione di integrazione applicativa dei dati con gli argomenti - alcuna richiesta visualizzata non verrà assegnato come--force flag viene utilizzato.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-profile -c`
Profilo di configurazione integrazione applicativa dei dati, utilizzata per la distribuzione del cluster: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [sì/no]. Se non vuoi usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su 'Sì'
#### `--node-label -l`
Etichetta del nodo integrazione applicativa dei dati, usato per designare quali nodi da distribuire.
#### `--force -f`
Forza la creazione, l'utente non verrà richiesto per tutti i valori e tutti i problemi verranno stampati come parte di stderr.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-bdc-delete"></a>eliminazione di integrazione applicativa dei dati mssqlctl
Eliminare il Cluster di dati Big data di SQL Server: configurazione di kube è necessaria per il sistema con le seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl bdc delete --name -n 
                    [--force -f]
```
### <a name="examples"></a>Esempi
Eliminazione di integrazione applicativa dei dati in cui il controller il nome utente e la password già impostati nel proprio ambiente di sistema.
```bash
mssqlctl bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome di integrazione applicativa dei dati, utilizzata per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--force -f`
Forzare l'eliminazione integrazione applicativa dei dati.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).

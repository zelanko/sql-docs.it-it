---
title: riferimento cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779256"
---
# <a name="mssqlctl-cluster"></a>cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[creare cluster mssqlctl](#mssqlctl-cluster-create) | Creare cluster.
[eliminazione del cluster mssqlctl](#mssqlctl-cluster-delete) | Eliminare il cluster.
[configurazione di cluster mssqlctl](reference-mssqlctl-cluster-config.md) | Comandi di configurazione del cluster.
[endpoint cluster mssqlctl](reference-mssqlctl-cluster-endpoint.md) | Comandi dell'endpoint.
[stato del cluster mssqlctl](reference-mssqlctl-cluster-status.md) | Comandi di stato.
[debug di cluster mssqlctl](reference-mssqlctl-cluster-debug.md) | I comandi di debug.
[mssqlctl-pool di archiviazione cluster](reference-mssqlctl-cluster-storage-pool.md) | Gestire i pool di archiviazione del cluster.
## <a name="mssqlctl-cluster-create"></a>creare cluster mssqlctl
Creare un Cluster di dati SQL Server Big - configurazione kube è necessaria per il sistema con le seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>Esempi
Esperienza di distribuzione del cluster - guidato si riceveranno istruzioni per i valori necessari.
```bash
mssqlctl cluster create
```
Distribuzione del cluster con gli argomenti.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
Distribuzione del cluster con gli argomenti - alcuna richiesta visualizzata verrà assegnata come--force flag viene utilizzato.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-file -c`
Profilo di configurazione, usato per la distribuzione del cluster del cluster: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [yes/no]. Se non vuoi usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su 'Sì'
#### `--node-label -l`
Etichetta del nodo cluster, usato per designare quali nodi da distribuire.
#### `--force -f`
Forza la creazione, l'utente non verrà richiesto per tutti i valori e tutti i problemi verranno stampati come parte di stderr.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-cluster-delete"></a>eliminazione del cluster mssqlctl
Eliminare il Cluster di dati Big data di SQL Server: configurazione di kube è necessaria per il sistema con le seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>Esempi
L'eliminazione del cluster in cui il controller il nome utente e la password già impostati nel proprio ambiente di sistema.
```bash
mssqlctl cluster delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del cluster, usata per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--force -f`
Cluster di eliminazione forzata.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).

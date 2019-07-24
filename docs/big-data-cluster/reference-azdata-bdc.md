---
title: riferimento BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426041"
---
# <a name="azdata-bdc"></a>azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **integrazione applicativa** dei dati nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:

|     |     |
| --- | --- |
[creazione BDC azdata](#azdata-bdc-create) | Creare un cluster di Big Data.
[eliminazione BDC azdata](#azdata-bdc-delete) | Eliminare un cluster di Big Data.
[azdata configurazione BDC](reference-azdata-bdc-config.md) | Comandi di configurazione.
[endpoint BDC azdata](reference-azdata-bdc-endpoint.md) | Comandi dell'endpoint.
[stato BDC azdata](reference-azdata-bdc-status.md) | Comandi di stato.
[debug BDC azdata](reference-azdata-bdc-debug.md) | Comandi di debug.
[controllo BDC azdata](reference-azdata-bdc-control.md) | Comandi di controllo.
[azdata pool di integrazione applicativa dei dati](reference-azdata-bdc-pool.md) | Comandi del pool.
[azdata BDC HDFS](reference-azdata-bdc-hdfs.md) | Il modulo HDFS fornisce i comandi per accedere a un file system HDFS.
[Spark azdata BDC](reference-azdata-bdc-spark.md) | I comandi Spark consentono all'utente di interagire con il sistema Spark creando e gestendo sessioni, istruzioni e batch.
## <a name="azdata-bdc-create"></a>creazione BDC azdata
Creare un cluster SQL Server Big Data: è richiesta la configurazione Kube nel sistema insieme alle variabili di ambiente seguenti [' CONTROLLER_USERNAME ',' CONTROLLER_PASSWORD ',' MSSQL_SA_PASSWORD ',' KNOX_PASSWORD '].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Esempi

Esperienza di distribuzione dell'integrazione applicativa dei dati guidata: si riceveranno richieste per i valori necessari.

```bash
azdata bdc create
```

Distribuzione BDC con argomenti.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Distribuzione BDC con il nome specificato anziché il nome predefinito nel profilo.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

Distribuzione di integrazione applicativa dei dati con argomenti: nessuna richiesta verrà assegnata quando viene utilizzato il flag--Force.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del cluster di Big data, usato per gli spazi dei nomi kubernetes.
#### `--config-profile -c`
Profilo di configurazione del cluster di Big data, usato per la distribuzione del cluster: [' AKS-dev-test ',' kubeadm-dev-test ',' minikube-dev-test ']
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [Sì/No]. Se non si vuole usare questo arg, è possibile impostare la variabile di ambiente ACCEPT_EULA su "Yes". Le condizioni di licenza per questo prodotto possono essere visualizzate https://aka.ms/azdata-eula in https://go.microsoft.com/fwlink/?LinkId=2002534 e.
#### `--node-label -l`
Etichetta del nodo del cluster di Big data, usata per definire i nodi in cui eseguire la distribuzione.
#### `--force -f`
Force create, all'utente non verrà richiesto alcun valore e tutti i problemi verranno stampati come parte di stderr.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="azdata-bdc-delete"></a>eliminazione BDC azdata
Eliminare il cluster di SQL Server Big Data-la configurazione KUBE è necessaria nel sistema insieme alle variabili di ambiente seguenti [' CONTROLLER_USERNAME ',' CONTROLLER_PASSWORD '].
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Esempi
Eliminazione di BDC in cui il nome utente e la password del controller sono già impostati nell'ambiente di sistema.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del cluster di Big Data usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--force -f`
Forzare l'eliminazione Big Data cluster.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).

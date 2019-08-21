---
title: Informazioni di riferimento su azdata bdc
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 44b0f8daafec86714bb8161c1d30130eed3d480d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653449"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi **bdc** dello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:

|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Crea un cluster Big Data.
[azdata bdc delete](#azdata-bdc-delete) | Elimina un cluster Big Data.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandi di configurazione.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandi dell'endpoint.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandi di stato.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandi di debug.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandi di controllo.
[azdata bdc pool](reference-azdata-bdc-pool.md) | Comandi di pool.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Il modulo HDFS fornisce i comandi per accedere a un file system HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | I comandi Spark consentono agli utenti di interagire con il sistema Spark creando e gestendo sessioni, istruzioni e batch.
## <a name="azdata-bdc-create"></a>azdata bdc create
Crea un cluster Big Data di SQL Server - Nel sistema è necessaria una configurazione kube insieme alle seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Esempi

Esperienza guidata di distribuzione del cluster Big Data: si riceveranno le indicazioni relative ai valori necessari.

```bash
azdata bdc create
```

Distribuzione del cluster Big Data con argomenti.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Distribuzione del cluster Big Data con il nome specificato anziché con il nome predefinito nel profilo.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

Distribuzione del cluster Big Data con argomenti: viene usato il flag --force e non verrà quindi visualizzato alcun messaggio di richiesta.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del cluster Big Data, usato per gli spazi dei nomi kubernetes.
#### `--config-profile -c`
Profilo di configurazione del cluster Big Data, usato per la distribuzione del cluster: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". Le condizioni di licenza per questo prodotto possono essere visualizzate [https://go.microsoft.com/fwlink/?LinkId=2002534](https://go.microsoft.com/fwlink/?LinkId=2002534)all'indirizzo.
#### `--node-label -l`
Etichetta del nodo del cluster Big data, usata per definire i nodi in cui eseguire la distribuzione.
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
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-delete"></a>azdata bdc delete
Elimina un cluster Big Data di SQL Server - Nel sistema è necessaria una configurazione kube insieme alle seguenti variabili di ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Esempi
Eliminazione di un cluster Big Data in cui il nome utente e la password del controller sono già impostati nell'ambiente di sistema.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del cluster Big Data, usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--force -f`
Forza l'eliminazione di un cluster Big Data.
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

Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per ulteriori informazioni su come installare lo strumento **azdata** , vedere [Install azdata to Manage [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).

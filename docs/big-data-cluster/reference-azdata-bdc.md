---
title: Informazioni di riferimento su azdata bdc
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408b3c2d55d5e2515a2df979cd54b380a0d54704
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155135"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Questo articolo è un articolo di riferimento per **azdata**. 

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Crea un cluster Big Data.
[azdata bdc delete](#azdata-bdc-delete) | Elimina un cluster Big Data.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandi di configurazione.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandi dell'endpoint.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandi di debug.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandi di stato BDC.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandi del servizio di controllo.
[SQL BDC azdata](reference-azdata-bdc-sql.md) | Comandi del servizio SQL.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Comandi del servizio HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Comandi del servizio Spark.
[Gateway BDC azdata](reference-azdata-bdc-gateway.md) | Comandi del servizio gateway.
[app BDC azdata](reference-azdata-bdc-app.md) | Comandi del servizio app.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Il modulo HDFS fornisce i comandi per accedere a un file system HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | I comandi Spark consentono agli utenti di interagire con il sistema Spark creando e gestendo sessioni, istruzioni e batch.
## <a name="azdata-bdc-create"></a>azdata bdc create
Creare un cluster di SQL Server Big Data: è richiesta la configurazione Kubernetes nel sistema insieme alle variabili di ambiente seguenti [' CONTROLLER_USERNAME ',' CONTROLLER_PASSWORD ',' MSSQL_SA_PASSWORD ',' KNOX_PASSWORD '].
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
Profilo di configurazione del cluster di Big data, usato per la distribuzione del cluster: [' AKS-dev-test ',' kubeadm-prod ',' minikube-dev-test ',' kubeadm-dev-test ']
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". Le condizioni di licenza di questo prodotto sono disponibili in https://aka.ms/azdata-eula e https://go.microsoft.com/fwlink/?LinkId=2002534.
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
Eliminare il cluster di SQL Server Big Data: è richiesta la configurazione Kubernetes nel sistema.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Esempi
Eliminazione dell'integrazione applicativa dei dati.
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

- Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

- Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).

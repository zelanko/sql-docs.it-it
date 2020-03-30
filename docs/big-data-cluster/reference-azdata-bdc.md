---
title: Informazioni di riferimento su azdata bdc
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5d5cb5256f4a1b8389d882300a89f0ee0012a99
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820982"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `bdc` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Crea un cluster Big Data.
[azdata bdc delete](#azdata-bdc-delete) | Elimina un cluster Big Data.
[azdata bdc upgrade](#azdata-bdc-upgrade) | Aggiorna le immagini distribuite in ogni contenitore del cluster Big Data di SQL Server.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandi di configurazione.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandi dell'endpoint.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandi di debug.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandi di stato del cluster Big Data.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandi del servizio di controllo.
[azdata bdc sql](reference-azdata-bdc-sql.md) | Comandi del servizio sql.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Comandi del servizio HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Comandi del servizio Spark.
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | Comandi del servizio gateway.
[azdata bdc app](reference-azdata-bdc-app.md) | Comandi del servizio app.
[azdata bdc spark](reference-azdata-bdc-spark.md) | I comandi Spark consentono agli utenti di interagire con il sistema Spark creando e gestendo sessioni, istruzioni e batch.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Il modulo HDFS fornisce i comandi per accedere a un file system HDFS.
## <a name="azdata-bdc-create"></a>azdata bdc create
Crea un cluster Big Data di SQL Server. È necessaria la configurazione di Kubernetes nel sistema in uso con le variabili di ambiente seguenti ['AZDATA_USERNAME', 'AZDATA_PASSWORD'].
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
Profilo di configurazione del cluster Big Data, usato per la distribuzione del cluster: ['kubeadm-dev-test', 'kubeadm-prod', 'aks-dev-test', 'aks-dev-test-ha']
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". È possibile visualizzare le condizioni di licenza per azdata all'indirizzo https://aka.ms/eula-azdata-en. È possibile visualizzare le condizioni di licenza per il cluster Big Data per le diverse edizioni agli indirizzi seguenti: Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292, Standard: https://go.microsoft.com/fwlink/?linkid=2104294, Developer: https://go.microsoft.com/fwlink/?linkid=2104079.
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-delete"></a>azdata bdc delete
Elimina il cluster Big Data di SQL Server. È necessaria la configurazione di Kubernetes nel sistema in uso.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Esempi
Eliminazione di un cluster Big Data.
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
Aggiorna le immagini distribuite in ogni contenitore del cluster Big Data di SQL Server. Le immagini aggiornate si basano sull'immagine Docker passata. Se le immagini aggiornate provengono da un repository di immagini Docker diverso rispetto alle immagini attualmente distribuite, è necessario anche il parametro "repository".
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   [--repository -r]
```
### <a name="examples"></a>Esempi
Aggiornamento del cluster Big Data con un nuovo tag immagine "cu2" dallo stesso repository.
```bash
azdata bdc upgrade -t cu2
```
Aggiornamento del cluster Big Data con nuove immagini con tag "cu2" dal nuovo repository "foo/bar/baz".
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del cluster Big Data, usato per gli spazi dei nomi kubernetes.
#### `--tag -t`
Tag dell'immagine Docker di destinazione a cui aggiornare tutti i contenitori del cluster.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--repository -r`
Repository Docker da cui tutti i contenitori del cluster devono trarre le proprie immagini.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).

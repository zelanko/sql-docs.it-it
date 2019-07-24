---
title: riferimento a azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425991"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per lo strumento **azdata** per i [cluster Big Data SQL Server 2019 (anteprima)](big-data-cluster-overview.md). Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
|[app azdata](reference-azdata-app.md) | Creare, eliminare, eseguire e gestire le applicazioni. |
|[azdata BDC](reference-azdata-bdc.md) | Consente di selezionare, gestire e utilizzare SQL Server cluster di Big Data. |
|[Notebook di azdata](reference-azdata-notebook.md) | Comandi per la visualizzazione, l'esecuzione e la gestione dei notebook da un terminale. |
[accesso azdata](#azdata-login) | Accedere all'endpoint controller del cluster.
[disconnessione azdata](#azdata-logout) | Disconnettersi dal cluster.
|[azdata SQL](reference-azdata-sql.md) | L'interfaccia della riga di comando di SQL database consente all'utente di interagire con SQL Server tramite T-SQL. |
## <a name="azdata-login"></a>accesso azdata
Quando si distribuisce il cluster, l'endpoint controller viene elencato durante la distribuzione, che è necessario utilizzare per l'accesso.  Se non si conosce l'endpoint del controller, è possibile effettuare l'accesso con la configurazione di Kube del cluster nel sistema nel percorso predefinito di <user home>/.Kube/config o usare KUBECONFIG env var, ad esempio Export KUBECONFIG = Path/to/. Kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Esempi
Eseguire l'accesso in modo interattivo. Se non viene specificato come argomento, viene sempre richiesto il nome del cluster. Se nel sistema sono impostate le variabili CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA ENV, queste non verranno richieste. Se nel sistema è presente la configurazione di Kube o si usa KUBECONFIG env var per specificare il percorso della configurazione, l'esperienza interattiva tenterà prima di tutto di usare il file di configurazione e quindi chiederà se la configurazione ha esito negativo.
```bash
azdata login
```
Accedi (in modo non interattivo). Eseguire l'accesso con il nome del cluster, il nome utente del controller, l'endpoint del controller e il set di accettazione EULA come argomenti. È necessario impostare la variabile di ambiente CONTROLLER_PASSWORD.  Se non si vuole specificare l'endpoint del controller, configurare la configurazione Kube nel computer nel percorso predefinito di <user home>/.Kube/config o usare KUBECONFIG env var, ad esempio Export KUBECONFIG = Path/to/. Kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Accedere con la configurazione di Kube nel computer e env var set per CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--cluster-name -n`
Nome del cluster.
#### `--controller-username -u`
Utente dell'account. Se non si vuole usare questo arg, è possibile impostare la variabile di ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Endpoint controller cluster "https://host:port ". Se non si vuole usare questo argomento, è possibile usare la configurazione di Kube nel computer. Assicurarsi che la configurazione si trovi nel percorso predefinito di <user home>/.Kube/config o usare KUBECONFIG env var.
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [Sì/No]. Se non si vuole usare questo arg, è possibile impostare la variabile di ambiente ACCEPT_EULA su "Yes". Le condizioni di licenza per questo prodotto possono essere visualizzate https://aka.ms/azdata-eula all'indirizzo.
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
## <a name="azdata-logout"></a>disconnessione azdata
Disconnettersi dal cluster.
```bash
azdata logout 
```
### <a name="examples"></a>Esempi
Disconnettere l'utente.
```bash
azdata logout
```
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

Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).

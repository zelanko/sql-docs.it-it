---
title: riferimento azdata
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
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68425991"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente offre informazioni di riferimento per lo strumento **azdata** per [cluster Big Data di SQL Server 2019 (anteprima)](big-data-cluster-overview.md). Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | Consente di creare, eliminare, eseguire e gestire applicazioni. |
|[azdata bdc](reference-azdata-bdc.md) | Consente di selezionare, gestire e usare cluster Big Data di SQL Server. |
|[azdata notebook](reference-azdata-notebook.md) | Comandi per la visualizzazione, l'esecuzione e la gestione di notebook da un terminale. |
[azdata login](#azdata-login) | Consente di accedere all'endpoint del controller del cluster.
[azdata logout](#azdata-logout) | Consente di disconnettersi dal cluster.
|[azdata sql](reference-azdata-sql.md) | L'interfaccia della riga di comando dei database SQL consente agli utenti di interagire con SQL Server tramite T-SQL. |
## <a name="azdata-login"></a>azdata login
Quando si distribuisce il cluster, durante la distribuzione viene elencato l'endpoint del controller, che è necessario usare per poter accedere.  Se non si conosce l'endpoint del controller, è possibile effettuare l'accesso se nel sistema è presente la configurazione kube del cluster nel percorso predefinito <user home>/.kube/config oppure usando la variabile di ambiente KUBECONFIG, ad esempio export KUBECONFIG=path/to/.kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Esempi
Accedere in modo interattivo. Se non è stato specificato come argomento, verrà sempre richiesto il nome del cluster. Le variabili di ambiente CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA non verranno richieste se sono già state impostate nel sistema. Se nel sistema è presente la configurazione kube o si usa la variabile di ambiente KUBECONFIG per specificare il percorso di configurazione, l'esperienza interattiva tenterà prima di usare il file di configurazione e, se la configurazione avrà esito negativo, chiederà quindi all'utente di specificarlo.
```bash
azdata login
```
Accedere (in modo non interattivo). Eseguire l'accesso con il nome del cluster, il nome utente del controller, l'endpoint del controller e il set di accettazione EULA come argomenti. Deve essere inoltre impostata la variabile di ambiente CONTROLLER_PASSWORD.  Se non si vuole specificare l'endpoint del controller, è necessario che nel sistema sia presente la configurazione kube nel percorso predefinito <user home>/.kube/config oppure usando la variabile di ambiente KUBECONFIG, ad esempio export KUBECONFIG=path/to/.kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Accedere con la configurazione kube presente nel computer e con le variabili di ambiente impostate per CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--cluster-name -n`
Nome del cluster.
#### `--controller-username -u`
Utente dell'account. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Endpoint del controller del cluster "https://host:port". Se non si vuole usare questo argomento, è possibile usare la configurazione kube presente nel sistema. Assicurarsi che la configurazione si trovi nel percorso predefinito <user home>/.kube/config oppure usare la variabile di ambiente KUBECONFIG.
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". Le condizioni di licenza di questo prodotto sono disponibili in https://aka.ms/azdata-eula.
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
## <a name="azdata-logout"></a>azdata logout
Consente di disconnettersi dal cluster.
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
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).

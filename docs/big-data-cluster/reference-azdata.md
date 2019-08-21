---
title: riferimento azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 33cc3070647c58e6ae57c8bff3d587a76ae0a28d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653093"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sullo strumento **azdata** per [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (anteprima)](big-data-cluster-overview.md). Per ulteriori informazioni su come installare lo strumento **azdata** , vedere [Install azdata to Manage [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | Consente di creare, eliminare, eseguire e gestire applicazioni. |
|[azdata bdc](reference-azdata-bdc.md) | Consente di selezionare, gestire e usare cluster Big Data di SQL Server. |
|[azdata login](#azdata-login) | Consente di accedere all'endpoint del controller del cluster.
|[azdata logout](#azdata-logout) | Consente di disconnettersi dal cluster.

## <a name="azdata-login"></a>azdata login
Quando si distribuisce il cluster, l'endpoint controller viene elencato durante la distribuzione, che è necessario utilizzare per l'accesso.  Se non si conosce l'endpoint del controller, è possibile accedere con la configurazione di Kube del cluster nel sistema nel percorso predefinito di <user home>/.Kube/config o usare KUBECONFIG env var, ovvero Export KUBECONFIG = Path/to/. Kube/config.
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
Accedere (in modo non interattivo). Eseguire l'accesso con il nome del cluster, il nome utente del controller, l'endpoint del controller e il set di accettazione EULA come argomenti. Deve essere inoltre impostata la variabile di ambiente CONTROLLER_PASSWORD.  Se non si vuole specificare l'endpoint del controller, fare in modo che la configurazione di Kube nel computer sia nel percorso <user home>predefinito di/.Kube/config o usare KUBECONFIG env var, ovvero Export KUBECONFIG = Path/to/. Kube/config.
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
Endpoint del controller del cluster "https://host:port". Se non si vuole usare questo argomento, è possibile usare la configurazione kube presente nel sistema. Verificare che la configurazione si trovi nel percorso predefinito di <user home>/.Kube/config o usare KUBECONFIG env var.
#### `--accept-eula -a`
Indica se accettare le condizioni di licenza: [yes/no]. Se non si vuole usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su "yes". 
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per ulteriori informazioni ed esempi [http://jmespath.org/](http://jmespath.org/]) , vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per log di debug completi.
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
Stringa di query JMESPath. Per ulteriori informazioni ed esempi [http://jmespath.org/](http://jmespath.org/]) , vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su come installare lo strumento **azdata** , vedere [Install azdata to Manage [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).

---
title: riferimento mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: acc25e6b3deca199ad774378318e17991614dcaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779238"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **mssqlctl** dello strumento per [cluster di big data 2019 Server SQL (anteprima)](big-data-cluster-overview.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
|[app mssqlctl](reference-mssqlctl-app.md) | Creare, eliminare, eseguire e gestire le applicazioni. |
|[cluster mssqlctl](reference-mssqlctl-cluster.md) | Selezionare, gestire e operare i cluster. |
[account di accesso mssqlctl](#mssqlctl-login) | Accedere all'endpoint del cluster controller.
[disconnessione mssqlctl](#mssqlctl-logout) | Disconnettersi dal cluster.
## <a name="mssqlctl-login"></a>account di accesso mssqlctl
Quando viene distribuito il cluster, verranno visualizzate durante la distribuzione, è consigliabile usare l'endpoint di controller per l'accesso.  Se non si conosce l'endpoint di controller, è possibile con configurazione kube del cluster nel sistema nel percorso predefinito dell'account di accesso <user home>/.kube/config o utilizzano file KUBECONFIG env var, ovvero esportare KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>Esempi
Accedere in modo interattivo. Nome del cluster verrà sempre richiesto se non viene specificato come argomento. Se hai le variabili env CONTROLLER_USERNAME CONTROLLER_PASSWORD e ACCEPT_EULA impostate nel sistema, queste non richiederà per. Se si dispone di file di configurazione kube nel sistema o utilizzano file KUBECONFIG env var per specificare il percorso di file di configurazione, l'esperienza interattiva prima tenterà di usare file di configurazione e quindi verrà richiesto se la configurazione ha esito negativo.
```bash
mssqlctl login
```
Accedere (non interattiva). Accedere con il nome del cluster, nome utente del controller, endpoint di controller e l'accettazione delle condizioni di licenza impostata come argomenti. La variabile di ambiente CONTROLLER_PASSWORD deve essere impostata.  Se non vuoi specificare l'endpoint del controller, presenti file di configurazione kube nel computer nel percorso predefinito di <user home>/.kube/config o utilizzano file KUBECONFIG env var, ovvero esportare KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Accedere con configurazione kube sul computer ed env var impostato per CONTROLLER_USERNAME CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--cluster-name -n`
Nome del cluster.
#### `--controller-username -u`
Account utente. Se non vuoi usare questo argomento, è possibile impostare la variabile di ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Controller endpoint cluster "https://host:port". Se non vuoi usare questo argomento, è possibile utilizzare file di configurazione kube nel computer. Assicurarsi che la configurazione si trova nel percorso predefinito di <user home>/.kube/config o l'utilizzo di VAR. env KUBECONFIG
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [yes/no]. Se non vuoi usare questo argomento, è possibile impostare la variabile di ambiente ACCEPT_EULA su 'Sì'
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
## <a name="mssqlctl-logout"></a>disconnessione mssqlctl
Disconnettersi dal cluster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Esempi
Disconnettere l'utente.
```bash
mssqlctl logout
```
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

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).
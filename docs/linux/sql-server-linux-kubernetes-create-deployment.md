---
title: Creare script di distribuzione per il gruppo di disponibilità Always On di SQL Server in Kubernetes
description: Questo articolo illustra come creare script di distribuzione per un gruppo di disponibilità Always On di SQL Server in Kubernetes
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000138"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Creare lo script di distribuzione per il gruppo di disponibilità Always On di SQL Server

Questo articolo descrive come distribuire un gruppo di disponibilità in un cluster Kubernetes in un unico comando con uno script di distribuzione di esempio. `deploy-ag.py` è uno script Python che crea i file `.yaml` per il cluster e può applicarli a un cluster Kubernetes.

Scaricare i file da [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Prima di iniziare

Installare gli strumenti seguenti nella workstation.

* [Python](https://www.python.org/downloads/) (3.5 o 3.6)
* [PyYAML](https://pyyaml.org/): pacchetti Python
* [Client Kubernetes](https://github.com/kubernetes-client/python): pacchetto Python

Aggiungere i percorsi Python alle variabili di ambiente (per Windows).

### <a name="install-the-required-components"></a>Installare i componenti necessari

L'esempio seguente illustra come installare i pacchetti client PyYAML e Kubernetes per Python.

Dopo aver installato Python, scaricare ed estrarre la cartella di esempio. 

Per configurare i file necessari, eseguire il comando seguente. Sostituire `<path>` con la posizione dei file di esempio estratti.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Creare il cluster e scaricare il file di configurazione

L'esempio seguente crea il cluster nel servizio Azure Kubernetes.

Prima di eseguire lo script, aggiornare i valori tra le parentesi acute `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>Per i gruppi di disponibilità è necessario Kubernetes versione 1.11.0 o successiva. Nell'esempio viene usata la versione 1.11.1.

## <a name="run-the-deployment-script"></a>Eseguire lo script di distribuzione

Negli esempi seguenti viene illustrato come eseguire `deploy-ag.py`.

### <a name="help"></a>Guida

```cmd
python ./deploy-ag.py --help
```

* **sintassi**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argomenti facoltativi**:
  * `-h, --help` visualizza questo messaggio della guida ed esce
* **sottocomandi**:
  * Azioni sull'agente k8s {deploy | failover}

  `deploy`

   Distribuisce un set di istanze di SQL Server in un gruppo di disponibilità

  `failover`

   Effettua il failover in una replica di destinazione.

### <a name="deploy-help"></a>Deploy help

```cmd
python ./deploy-ag.py deploy --help
```

* **sintassi**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  Distribuisce gli agenti SQL Server e k8s nello spazio dei nomi (nome AG)

* **argomenti facoltativi**:
  
  `-h, --help`
  
  Visualizza questo messaggio della guida ed esce
  
  `--verbose, -v`
  
  Livello di dettaglio dell'output
  
  `--ag AG`
  
  Nome del gruppo di disponibilità. Impostazione predefinita=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  Nome dello spazio dei nomi k8s. Se viene omesso, l'impostazione predefinita è il nome AG.

  `--dry-run`
  
  Crea i manifesti, ma non li applica.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  Nomi delle istanze di SQL Server (fino a 5, separati da spazi) Impostazione predefinita=["mssql1", "mssql2", "mssql3"]
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  Password dell'amministratore di sistema. Impostazione predefinita="SAPassword2018"
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  Ignora la creazione dello spazio dei nomi.

### <a name="failover-help"></a>Failover help

```cmd
python ./deploy-ag.py failover --help
```
* **sintassi**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  Failover manuale

* **argomenti posizionali**: `target_replica`

  Nome della replica di SQL Server di destinazione per il failover

* **argomenti facoltativi**:

  `-h, --help`
  
  Visualizza questo messaggio della guida ed esce

  `--verbose, -v`
  
  Livello di dettaglio dell'output

  `--ag AG`
  
  Nome del gruppo di disponibilità. Impostazione predefinita=ag1

  `--namespace NAMESPACE`

  Nome dello spazio dei nomi k8s. Se viene omesso, l'impostazione predefinita è il nome AG

  `--dry-run`
  
  Crea, ma non applica i manifesti.

### <a name="create-the-manifests---dont-apply"></a>Crea i manifesti, non li applica

Lo script seguente crea i file manifesto, ma non li applica.

```cmd
python ./deploy-ag.py deploy --dry-run
```

L'esempio seguente crea i manifesti per un gruppo di disponibilità sotto lo spazio dei nomi `AG1` con tre repliche. Prima di eseguire lo script, sostituire `<MyC0m91exP@55w0r!>` con una password complessa.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

Il comando precedente genera la directory dei file YAML di esempio.

In questo caso, l'output del comando mostra la posizione in cui vengono creati i file manifesto.

![Output dello script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Creare i manifesti e applicarli

L'esempio seguente crea i manifesti per un gruppo di disponibilità sotto lo spazio dei nomi `ag1` con tre repliche e li applica al cluster Kubernetes. Il cluster creerà quindi il gruppo di disponibilità. Prima di eseguire lo script, sostituire `<MyC0m91exP@55w0r!>` con una password complessa.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Al completamento dello script, l'operatore Kubernetes crea la risorsa di archiviazione, le istanze di SQL Server e i servizi di bilanciamento del carico. È possibile monitorare la distribuzione con il [dashboard di Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Dopo che Kubernetes ha creato i contenitori di SQL Server:

1. [Connettersi](sql-server-linux-kubernetes-connect.md) a un'istanza di SQL Server nel cluster.

1. Creazione di un database.

1. Eseguire un backup completo del database per avviare la catena di log.

1. Aggiungere il database al gruppo di disponibilità.

Il gruppo di disponibilità viene creato con il seeding automatico, quindi SQL Server creerà automaticamente i database secondari nelle repliche appropriate.

### <a name="manually-failover"></a>Failover manuale

L'esempio seguente effettua il failover della replica primaria.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Passaggi successivi

[Gruppo di disponibilità di SQL Server nel cluster Kubernetes](sql-server-ag-kubernetes.md)

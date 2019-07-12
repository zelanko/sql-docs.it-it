---
title: Creare script di distribuzione per SQL Server gruppo di disponibilità AlwaysOn in Kubernetes
description: Questo articolo illustra come creare script di distribuzione per un SQL Server gruppo di disponibilità AlwaysOn in Kubernetes
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dfee5188c6fe54ed91172f9d83de7af6395c8956
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833643"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Creare uno script di distribuzione per SQL Server gruppo di disponibilità AlwaysOn

Questo articolo descrive come distribuire un gruppo di disponibilità in un cluster Kubernetes in un singolo comando con un esempio di script di distribuzione. `deploy-ag.py` è uno script Python che crea il `.yaml` nei file per il cluster e applicarle collettivamente a un cluster Kubernetes.

I file del file da scaricare [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Prima di iniziare

Installare gli strumenti seguenti nella workstation.

* [Python](https://www.python.org/downloads/) (3.5 o 3.6)
* [PyYAML](https://pyyaml.org/) -i pacchetti Python
* [Client Kubernetes](https://github.com/kubernetes-client/python) -pacchetto Python

Aggiungere i percorsi di python alle variabili di ambiente (per Windows).

### <a name="install-the-required-components"></a>Installare i componenti necessari

Nell'esempio seguente il codice precedente installa i pacchetti PyYAML e Client di Kubernetes per Python.

Dopo aver installato Python, scaricare ed estrarre la cartella di esempio. 

Per configurare i file necessari, eseguire il comando seguente. Sostituire `<path>` con il percorso del file di esempio estratti.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Creare Cluster e scaricare file di configurazione

Nell'esempio seguente crea il cluster in Azure Kubernetes Service (AKS).

Prima di eseguire lo script, aggiornare i valori in parentesi acute - `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>I gruppi di disponibilità richiede Kubernetes versione 1.11.0 o successiva. L'esempio specifica 1.11.1.

## <a name="run-the-deployment-script"></a>Eseguire lo script di distribuzione

Gli esempi seguenti illustrano come eseguire `deploy-ag.py`.

### <a name="help"></a>Help

```cmd
python ./deploy-ag.py --help
```

* **utilizzo**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argomenti facoltativi**:
  * `-h, --help` Mostra questo messaggio della Guida e uscita
* **sottocomandi**:
  * Operazioni su agenti k8s {distribuire | failover}

  `deploy`

   Distribuire un set di istanze di SQL Server in un gruppo di disponibilità

  `failover`

   Eseguire il failover a una replica di destinazione.

### <a name="deploy-help"></a>Distribuire la Guida

```cmd
python ./deploy-ag.py deploy --help
```

* **usage**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  Distribuire SQL Server e gli agenti k8s in namespace(AG name)

* **argomenti facoltativi**:
  
  `-h, --help`
  
  Mostra questo messaggio della Guida e uscita
  
  `--verbose, -v`
  
  Livello di dettaglio dell'output
  
  `--ag AG`
  
  nome del gruppo di disponibilità. Default=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  nome dello spazio dei nomi k8s. L'impostazione predefinita al nome del gruppo di disponibilità se non specificato.

  `--dry-run`
  
  Creare i manifesti, ma non applicarle.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  nomi delle istanze di SQL Server (fino a 5, separati da spazi) Default = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  Password account SA. Default='SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  Ignorare la creazione dello spazio dei nomi.

### <a name="failover-help"></a>Failover della Guida in linea

```cmd
python ./deploy-ag.py failover --help
```
* **usage**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  Eseguire il failover manuale

* **gli argomenti posizionali**: `target_replica`

  nome della replica di SQL Server di destinazione per il failover

* **argomenti facoltativi**:

  `-h, --help`
  
  Mostra questo messaggio della Guida e uscita

  `--verbose, -v`
  
  Livello di dettaglio dell'output

  `--ag AG`
  
  nome del gruppo di disponibilità. Default=ag1

  `--namespace NAMESPACE`

  nome dello spazio dei nomi k8s. Il valore predefinito è nome del gruppo di disponibilità se non specificato

  `--dry-run`
  
  Creare, ma non si applicano i manifesti.

### <a name="create-the-manifests---dont-apply"></a>Creare i manifesti: non si applicano

Lo script seguente crea i file manifesto, ma non sono valide.

```cmd
python ./deploy-ag.py deploy --dry-run
```

L'esempio seguente crea i manifesti per un gruppo di disponibilità nello spazio dei nomi `AG1` con tre repliche. Prima di eseguire lo script, sostituire `<MyC0m91exP@55w0r!>` con una password complessa.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

Il comando precedente genera directory dei file yaml di esempio.

In questo caso, l'output del comando Mostra in cui vengono creati i file manifesto.

![Output dello script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Creare i manifesti e applicare

L'esempio seguente crea i manifesti per un gruppo di disponibilità nello spazio dei nomi `ag1` con tre repliche e le applica al cluster Kubernetes. Il cluster verrà quindi creato il gruppo di disponibilità. Prima di eseguire lo script, sostituire `<MyC0m91exP@55w0r!>` con una password complessa.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Al termine dell'esecuzione dello script, l'operatore di Kubernetes crea lo spazio di archiviazione, le istanze di SQL Server, i servizi di bilanciamento di carico. È possibile monitorare la distribuzione con [dashboard di Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Dopo che Kubernetes ha creato i contenitori di SQL Server:

1. [Connettere](sql-server-linux-kubernetes-connect.md) a un'istanza di SQL Server nel cluster.

1. Creazione di un database.

1. Eseguire un backup completo del database per avviare la catena di log.

1. Aggiungere il database al gruppo di disponibilità.

Viene creato il gruppo di disponibilità con seeding automatico in modo che SQL Server creerà automaticamente i database secondari nelle repliche appropriate.

### <a name="manually-failover"></a>Eseguire il failover manuale

Nell'esempio seguente esegue il failover della replica primaria.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Passaggi successivi

[Gruppo di disponibilità SQL Server in cluster Kubernetes](sql-server-ag-kubernetes.md)

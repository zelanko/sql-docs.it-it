---
title: Note sulla versione dei cluster Big Data di SQL Server
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive gli aggiornamenti più recenti e i problemi noti per i cluster Big Data di SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 136665cbe354ce0fdbbc575d2e97759f35cb3444
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286225"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>Note sulla versione dei cluster Big Data di SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Le note sulla versione seguenti si applicano a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Questo articolo è suddiviso in sezioni corrispondenti a ogni versione. Ogni versione ha un collegamento a un articolo del supporto che descrive le modifiche CU, oltre ai collegamenti ai download dei pacchetti Linux. L'articolo elenca anche i [problemi noti](#known-issues) per le versioni più recenti dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

## <a name="supported-platforms"></a>Piattaforme supportate

Questa sezione illustra le piattaforme supportate con i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

### <a name="kubernetes-platforms"></a>Piattaforme Kubernetes

|Piattaforma|Versioni supportate|
|---------|---------|
|Kubernetes|Il cluster Big Data richiede almeno la versione 1.13 di Kubernetes. Per i criteri di supporto delle versioni di Kubernetes, vedere [Criteri di supporto delle versioni e dello sfasamento tra versioni di Kubernetes](https://kubernetes.io/docs/setup/release/version-skew-policy/).|
|Servizio Azure Kubernetes|Il cluster Big Data richiede almeno la versione 1.13 del servizio Azure Kubernetes.<br/>Per i criteri di supporto delle versioni, vedere [Versioni di Kubernetes supportate nel servizio Azure Kubernetes](/azure/aks/supported-kubernetes-versions).|

### <a name="host-os-for-kubernetes"></a>Sistema operativo host per Kubernetes

|Piattaforma|Versioni supportate|
|---------|---------|
|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|Ubuntu|16.04|

### <a name="sql-server-editions"></a>Edizioni di SQL Server

|Edizione|Note|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| L'edizione del cluster Big Data è determinata dall'edizione dell'istanza master di SQL Server. In fase di distribuzione, per impostazione predefinita viene distribuita l'edizione Developer. È possibile modificare l'edizione dopo la distribuzione. Vedere [Configurare l'istanza master di SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="tools"></a>Strumenti

|Piattaforma|Versioni supportate|
|---------|---------|
|`azdata`|La versione secondaria deve corrispondere a quella del server (dell'istanza master di SQL Server).<br/><br/>Eseguire `azdata –-version` per convalidare la versione.<br/><br/>A partire da SQL Server 2019 CU3, questa versione è `15.0.4023`.|
|Azure Data Studio|Ottenere la build più recente di [Azure Data Studio](https://aka.ms/getazuredatastudio).|

## <a name="release-history"></a>Cronologia delle versioni

Nella tabella seguente viene elencata la cronologia delle versioni per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

| Versione               | Versione       | Data di rilascio |
|-----------------------|---------------|--------------|
| [CU3](#cu3)           | 15.0.4023.6    | 2020-03-12   |
| [CU2](#cu2)           | 15.0.4013.40    | 2020-02-13   |
| [CU1](#cu1)           | 15.0.4003.23   | 07 gennaio 2020   |
| [GDR1](#rtm)            | 15.0.2070.34  | 4 novembre 2019   |

## <a name="how-to-install-updates"></a>Come installare gli aggiornamenti

Per installare gli aggiornamenti, vedere [Come aggiornare [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

## <a name="cu3-mar-2020"></a><a id="cu3"></a> CU3 (marzo 2020)

Aggiornamento cumulativo 3 (CU3) per SQL Server 2019. La versione del motore di database di SQL Server per questa versione è 15.0.4023.6.

|Versione pacchetto | Tag dell'immagine |
|-----|-----|
|15.0.4023.6 |[2019-CU3-ubuntu-16.04]

### <a name="resolved-issues"></a>Problemi risolti

SQL Server 2019 CU3 risolve i problemi seguenti dalle versioni precedenti.

- [Distribuzione con repository privato](#deployment-with-private-repository)
- [Possibile esito negativo dell'aggiornamento a causa di un timeout](#upgrade-may-fail-due-to-timeout)

## <a name="cu2-feb-2020"></a><a id="cu2"></a> CU2 (feb 2020)

Aggiornamento cumulativo 2 (CU2) per SQL Server 2019. La versione del motore di database di SQL Server per questa versione è 15.0.4013.40.

|Versione pacchetto | Tag dell'immagine |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a name="cu1-jan-2020"></a><a id="cu1"></a> CU1 (gennaio 2020)

Versione Cumulative Update 1 (CU1) per SQL Server 2019. La versione del motore di database di SQL Server per questa versione è 15.0.4003.23.

|Versione pacchetto | Tag dell'immagine |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a name="gdr1-nov-2019"></a><a id="rtm"></a> GDR1 (novembre 2019)

SQL Server 2019 General Distribution Release 1 (GDR1): introduce la disponibilità generale per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)]. La versione del motore di database di SQL Server per questa versione è 15.0.2070.34.

|Versione pacchetto | Tag dell'immagine |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>Problemi noti

### <a name="deployment-with-private-repository"></a>Distribuzione con repository privato

- **Versioni interessate**: GDR1, CU1, CU2. Risolto per CU3.

- **Problema e impatto per i clienti**: L'aggiornamento da un repository privato presenta requisiti specifici

- **Soluzione alternativa**: Se si usa un repository privato per eseguire preventivamente il pull delle immagini per la distribuzione o l'aggiornamento dei cluster Big Data, verificare che le immagini di compilazione correnti e le immagini di compilazione di destinazione si trovino nel repository privato. Questo consente di ripristinare correttamente lo stato precedente, se necessario. Se le credenziali del repository privato sono state modificate dopo la distribuzione originale, poi, aggiornare il segreto corrispondente in Kubernetes prima di eseguire l'aggiornamento. `azdata` non supporta l'aggiornamento delle credenziali tramite `AZDATA_PASSWORD` e le variabili di ambiente `AZDATA_USERNAME`. Aggiornare il segreto tramite [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret). 

L'aggiornamento tramite repository diversi per le compilazioni correnti e di destinazione non è supportato.

### <a name="upgrade-may-fail-due-to-timeout"></a>Possibile esito negativo dell'aggiornamento a causa di un timeout

- **Versioni interessate**: GDR1, CU1, CU2. Risolto per CU3.

- **Problema e impatto per i clienti**: l'aggiornamento può avere esito negativo a causa di un timeout.

   Il codice seguente illustra il possibile aspetto dell'errore:

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   Questo errore si verifica con maggiore probabilità quando si aggiorna un cluster Big Data nel servizio Azure Kubernetes.

- **Soluzione alternativa**: aumentare il timeout per l'aggiornamento. 

   Per aumentare i timeout per un aggiornamento, modificare la mappa di configurazione dell'aggiornamento stesso. Per modificare la mappa di configurazione dell'aggiornamento:

   1. Eseguire il comando seguente:

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2. Modificare i campi seguenti:

       **`controllerUpgradeTimeoutInMinutes`** Indica il numero di minuti di attesa del completamento dell'aggiornamento del controller o del database del controller. Il valore predefinito è 5. Per l'aggiornamento impostare almeno il valore 20.

       **`totalUpgradeTimeoutInMinutes`** : Definisce la combinazione del tempo impiegato dal controller e il tempo impiegato dal database del controller per completare l'aggiornamento (aggiornamento controller + database del controller). Il valore predefinito è 10. Per l'aggiornamento impostare almeno il valore 40.

       **`componentUpgradeTimeoutInMinutes`** : Definisce la quantità di tempo disponibile per il completamento di ogni fase successiva dell'aggiornamento.  L'impostazione predefinita è 30. Per l'aggiornamento impostare su 45.

   3. Salvare e uscire.

   Lo script Python seguente rappresenta un altro metodo per l'impostazione del timeout:

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>L'invio di un processo Livy da Azure Data Studio (ADS) o curl ha esito negativo con l'errore 500

- **Problema e impatto per i clienti**: in una configurazione a disponibilità elevata, le risorse condivise Spark `sparkhead` sono configurate con più repliche. In questo caso, è possibile che si verifichino errori durante l'invio di un processo Livy da Azure Data Studio (ADS) o `curl`. A scopo di verifica, se si usa il comando `curl` per qualsiasi pod `sparkhead`, la connessione viene rifiutata. Ad esempio, `curl https://sparkhead-0:8998/` o `curl https://sparkhead-1:8998` restituisce l'errore 500.

   Ciò accade negli scenari seguenti:

   - I pod ZooKeeper o i processi per ogni istanza di ZooKeeper vengono riavviati alcune volte.
   - La connettività di rete tra il pod `sparkhead` e i pod ZooKeeper non è affidabile.

- **Soluzione alternativa**: riavviare entrambi i server Livy.

   ```bash
   kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

   ```bash
   kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>Creare una tabella ottimizzata per la memoria quando l'istanza master si trova in un gruppo di disponibilità

- **Problema e impatto per i clienti**: non è possibile usare l'endpoint primario esposto per la connessione ai database del gruppo di disponibilità (listener) per creare tabelle ottimizzate per la memoria.

- **Soluzione alternativa**: per creare tabelle ottimizzate per la memoria quando l'istanza master di SQL Server è in una configurazione di un gruppo di disponibilità, [connettersi all'istanza di SQL Server](deployment-high-availability.md#instance-connect), esporre un endpoint, connettersi al database di SQL Server e creare le tabelle ottimizzate per la memoria nella sessione creata con la nuova connessione.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Eseguire l'inserimento in tabelle esterne in modalità di autenticazione di Active Directory

- **Problema e impatto per i clienti**: quando l'istanza master di SQL Server è in modalità di autenticazione di Active Directory, una query che seleziona solo da tabelle esterne, dove almeno una delle tabelle esterne si trova in un pool di archiviazione, ed esegue l'inserimento in un'altra tabella esterna, restituisce:

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **Soluzione alternativa**: modificare la query in uno dei modi seguenti. Unire la tabella del pool di archiviazione a una tabella locale oppure eseguire prima l'inserimento nella tabella locale, quindi leggere dalla tabella locale per eseguire l'inserimento nel pool di dati.

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>Non è possibile usare le funzionalità Transparent Data Encryption con i database che fanno parte del gruppo di disponibilità nell'istanza master di SQL Server

- **Problema e impatto per i clienti**: in una configurazione a disponibilità elevata, non è possibile usare database con crittografia abilitata dopo un failover, perché la chiave master usata per la crittografia è diversa per ogni replica. 

- **Soluzione alternativa**: non è disponibile alcuna soluzione alternativa per questo problema. È consigliabile evitare di abilitare la crittografia in questa configurazione fino a quando non verrà resa disponibile una correzione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)

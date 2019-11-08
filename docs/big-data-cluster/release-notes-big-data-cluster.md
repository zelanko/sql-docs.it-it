---
title: Note sulla versione dei cluster Big Data di SQL Server
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive gli aggiornamenti più recenti e i problemi noti per i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e868d5db99c3f0be141d28a881d8d8bc6f9c241e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531636"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>Note sulla versione dei cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

È possibile ottenere informazioni dettagliate quasi in tempo reale da tutti i dati usando i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], che offrono un ambiente completo per la gestione di grandi set di dati, incluse funzionalità di Machine Learning e intelligenza artificiale.

Questo articolo elenca gli aggiornamenti e i problemi noti per le versioni più recenti dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

## <a id="rtm"></a> SQL Server 2019

In [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] vengono introdotti i cluster Big Data di SQL Server.

Usare i cluster Big Data di SQL Server per:

- [Distribuire cluster scalabili](../big-data-cluster/deploy-get-started.md) di contenitori SQL Server, Spark e HDFS in esecuzione in Kubernetes. 
- Leggere, scrivere ed elaborare Big Data da Transact-SQL o Spark.
- Combinare e analizzare con facilità dati relazionali di alto valore con volumi elevati di Big Data.
- Eseguire query su origini dati esterne.
- Archiviare Big Data in HDFS gestito da SQL Server.
- Eseguire query sui dati da più origini dati esterne tramite il cluster.
- Usare i dati per intelligenza artificiale, Machine Learning e altre attività di analisi.
- [Distribuire ed eseguire applicazioni](../big-data-cluster/concept-application-deployment.md) in [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)].
- Virtualizzare i dati con [PolyBase](../relational-databases/polybase/polybase-guide.md). Eseguire query sui dati da origini dati esterne SQL Server, Oracle, Teradata, MongoDB e ODBC con tabelle esterne.
- Fornire disponibilità elevata per l'istanza master di SQL Server e tutti i database tramite una tecnologia basata su gruppi di disponibilità Always On.

## <a name="sql-server-version"></a>Versione di SQL Server

La versione corrente di SQL Server è `15.0.2070.34`.

## <a name="image-tags"></a>Tag di immagine

Il tag di immagine per questa versione è `2019-GDR1-ubuntu-16.04`.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>Facilità di supporto

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

### <a name="tools"></a>Strumenti

|Piattaforma|Versioni supportate|
|---------|---------|
|`azdata`|La versione secondaria deve corrispondere a quella del server (dell'istanza master di SQL Server).<br/>Eseguire `azdata –-version` per convalidare la versione. Attualmente, questa versione è `15.0.2070`.|
|Azure Data Studio|Ottenere la build più recente di [Azure Data Studio](https://aka.ms/getazuredatastudio).|

### <a name="sql-server-editions"></a>Edizioni di SQL Server

|Edizione|Note|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| L'edizione del cluster Big Data è determinata dall'edizione dell'istanza master di SQL Server. In fase di distribuzione, per impostazione predefinita viene distribuita l'edizione Developer. È possibile modificare l'edizione dopo la distribuzione. Vedere [Configurare l'istanza master di SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="known-issues"></a>Problemi noti

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>L'invio di un processo Livy da Azure Data Studio (ADS) o curl ha esito negativo con l'errore 500

**Problema e impatto per i clienti**: in una configurazione a disponibilità elevata, le risorse condivise Spark (sparkhead) sono configurate con più repliche. In questo caso, è possibile che si verifichino errori durante l'invio di un processo Livy da Azure Data Studio (ADS) o `curl`. A scopo di verifica, quando si usa un comando `curl` per qualsiasi pod sparkhead la connessione viene rifiutata. Ad esempio, `curl https://sparkhead-0:8998/` o `curl https://sparkhead-1:8998` restituisce l'errore 500.

Ciò accade negli scenari seguenti:

- I pod ZooKeeper o il processo per ogni istanza di ZooKeeper vengono riavviati alcune volte.
- La connettività di rete non è affidabile tra il pod sparkhead e i pod ZooKeeper.

**Soluzione alternativa**: riavviare entrambi i server Livy.

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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)

---
title: Configura SQL Server gruppo di disponibilità AlwaysOn per la disponibilità elevata in Linux
titleSuffix: SQL Server
description: Informazioni sulla creazione di un SQL Server Always nel gruppo di disponibilità (AG) per la disponibilità elevata in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e97708fc227cbbcadfeb6fe961fce2ad9ee41765
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027252"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configura SQL Server gruppo di disponibilità AlwaysOn per la disponibilità elevata in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come creare un SQL Server Always nel gruppo di disponibilità (AG) per la disponibilità elevata in Linux. Esistono due tipi di configurazione per gruppi di disponibilità. Oggetto *disponibilità elevata* configurazione usa un manager di cluster per assicurare la continuità aziendale. Questa configurazione può inoltre includere le repliche di scalabilità in lettura. Questo documento illustra come creare il gruppo di disponibilità per la disponibilità elevata.

È anche possibile creare un gruppo di disponibilità senza cluster responsabile *scalabilità in lettura*. Il gruppo di disponibilità per scalabilità in lettura fornisce solo le repliche di sola lettura per la scalabilità delle prestazioni. Non fornisce la disponibilità elevata. Per creare un gruppo di disponibilità per scalabilità in lettura, vedere [configurare un gruppo di disponibilità SQL Server per scalabilità in lettura in Linux](sql-server-linux-availability-group-configure-rs.md).

Le configurazioni che garantiscono elevata disponibilità e protezione dei dati richiedono due o tre sincrona delle repliche di commit. Con tre repliche sincrone, il gruppo di disponibilità possa ripristinare automaticamente anche se non è disponibile un unico server. Per altre informazioni, vedere [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md). 

Tutti i server devono essere fisici o virtuali e server virtuali devono essere nella stessa piattaforma di virtualizzazione. Questo requisito è che gli agenti di fencing sono specifici della piattaforma. Visualizzare [i criteri per i cluster Guest](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Guida di orientamento

I passaggi per creare un gruppo di disponibilità nei server Linux per la disponibilità elevata sono diversi dai passaggi in un cluster di failover di Windows Server. L'elenco seguente descrive i passaggi generali: 

1. [Configurare SQL Server nel server di cluster di tre](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Tutti i tre server nel gruppo di disponibilità devono essere sulla stessa piattaforma - fisica o virtuale, perché la disponibilità elevata Linux Usa gli agenti di fencing per isolare le risorse nei server. Gli agenti di fencing sono specifici per ogni piattaforma.

2. Creare il gruppo di disponibilità. Questo passaggio è illustrato in questo articolo corrente. 

3. Configurare un cluster di resource manager, ad esempio Pacemaker.
   
   Il modo per configurare un gestore di risorse cluster dipende la distribuzione Linux specifica. Vedere i collegamenti seguenti per istruzioni specifiche di distribuzione: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Gli ambienti di produzione richiedono un agente di isolamento, ad esempio STONITH per la disponibilità elevata. Le dimostrazioni in questa documentazione non usano gli agenti di fencing. Le dimostrazioni sono per i test e convalida solo. 
   
   >Un cluster Linux Usa l'isolamento per restituire il cluster a uno stato noto. Il modo per configurare l'isolamento varia a seconda della distribuzione e l'ambiente. Attualmente, l'isolamento non è disponibile in alcuni ambienti cloud. Per altre informazioni, vedere [criteri di supporto per RHEL cluster disponibilità elevata - piattaforme di virtualizzazione](https://access.redhat.com/articles/29440).
   
   >Per SLES, vedere [estensione disponibilità elevata di SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Aggiungere il gruppo di disponibilità come una risorsa nel cluster.  

   Il modo per aggiungere il gruppo di disponibilità come una risorsa del cluster dipende la distribuzione Linux. Vedere i collegamenti seguenti per istruzioni specifiche di distribuzione: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Creare il gruppo di disponibilità

Gli esempi in questa sezione illustrano come creare il gruppo di disponibilità con Transact-SQL. È anche possibile usare la creazione guidata gruppo di SQL Server Management Studio disponibilità. Quando si crea un gruppo di disponibilità con la procedura guidata, restituirà un errore quando si crea un join le repliche per il gruppo di disponibilità. Per risolvere questo problema, concedere `ALTER`, `CONTROL`, e `VIEW DEFINITIONS` a di pacemaker nel gruppo di disponibilità in tutte le repliche. Una volta nella replica primaria vengono concesse le autorizzazioni, aggiungere i nodi per il gruppo di disponibilità tramite la procedura guidata, ma per la disponibilità elevata funzionare correttamente, concedere l'autorizzazione per tutte le repliche.

Per una configurazione a disponibilità elevata che garantisce il failover automatico, il gruppo di disponibilità richiede almeno tre repliche. Una delle seguenti configurazioni possono supportare la disponibilità elevata:

- [Tre repliche sincrone](sql-server-linux-availability-group-ha.md#threeSynch)

- [Due repliche sincrone oltre a una replica di configurazione](sql-server-linux-availability-group-ha.md#twoSynch)

Per informazioni, vedere [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>I gruppi di disponibilità possono includere altre repliche sincrone o asincrone. 

Creare il gruppo di disponibilità per la disponibilità elevata in Linux. Usare la [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) con `CLUSTER_TYPE = EXTERNAL`. 

* Gruppo di disponibilità - `CLUSTER_TYPE = EXTERNAL` specifica che un'entità esterna cluster gestisce un gruppo di disponibilità. Pacemaker è un esempio di un'entità cluster esterno. Quando il tipo di cluster del gruppo di disponibilità è esterno, 

* Set di repliche primarie e secondarie `FAILOVER_MODE = EXTERNAL`. 
   Specifica che la replica interagisce con un manager di cluster external, ad esempio Pacemaker. 

Gli script di Transact-SQL seguenti creano un gruppo di disponibilità per la disponibilità elevata denominata `ag1`. Lo script configura le repliche del gruppo di disponibilità con `SEEDING_MODE = AUTOMATIC`. Questa impostazione fa in modo che SQL Server creare automaticamente il database in ogni server secondario. Aggiornare lo script seguente per il proprio ambiente. Sostituire il `<node1>`, `<node2>`, o `<node3>` valori con i nomi delle istanze di SQL Server che ospitano le repliche. Sostituire il `<5022>` con la porta è impostata per i dati di endpoint del mirroring. Per creare il gruppo di disponibilità, eseguire l'istruzione Transact-SQL seguente sull'istanza di SQL Server che ospita la replica primaria.

Eseguire **sola** degli script seguenti: 

- [Creare il gruppo di disponibilità con tre repliche sincrone](#threeSynch).
- [Creare il gruppo di disponibilità con due repliche sincrone e una replica di configurazione](#configOnly)
- [Creare il gruppo di disponibilità con due repliche sincrone](#readScale).

<a name="threeSynch"></a>

- Creare gruppi di disponibilità con tre repliche sincrone

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Dopo aver eseguito lo script precedente per creare un gruppo di disponibilità con tre repliche sincrone, non eseguire lo script seguente:

<a name="configOnly"></a>
- Creare gruppi di disponibilità con due repliche sincrone e una replica di configurazione:

   >[!IMPORTANT]
   >Questa architettura consente a qualsiasi edizione di SQL Server per ospitare la replica di terza. Ad esempio, la terza replica può essere ospitata su SQL Server Enterprise Edition. In Enterprise Edition, è il tipo di endpoint valido solo `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Creare gruppi di disponibilità con due repliche sincrone

   Includere due repliche con modalità di disponibilità sincroni. Ad esempio, lo script seguente crea un gruppo di disponibilità denominato `ag1`. `node1` e `node2` ospitano le repliche in modalità sincrona, con il seeding automatico e il failover automatico.

   >[!IMPORTANT]
   >Eseguire solo lo script seguente per creare un gruppo di disponibilità con due repliche sincrone. Non eseguire lo script seguente se è stato eseguito uno script precedente. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


È anche possibile configurare un gruppo di disponibilità con `CLUSTER_TYPE=EXTERNAL` usando SQL Server Management Studio o PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Aggiungere le repliche secondarie al gruppo di disponibilità

Richiede all'utente di pacemaker `ALTER`, `CONTROL`, e `VIEW DEFINITION` autorizzazioni nel gruppo di disponibilità in tutte le repliche. Per concedere le autorizzazioni, eseguire lo script di Transact-SQL seguente dopo aver creato il gruppo di disponibilità nella replica primaria e ogni replica secondaria immediatamente dopo essere stati aggiunti al gruppo di disponibilità. Prima di eseguire lo script, sostituire `<pacemakerLogin>` con il nome dell'account utente pacemaker.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

Lo script di Transact-SQL seguente aggiunge un'istanza di SQL Server a un gruppo di disponibilità denominato `ag1`. Aggiornare lo script per il proprio ambiente. In ogni istanza di SQL Server che ospita una replica secondaria, eseguire il Transact-SQL seguente per creare un join del gruppo di disponibilità.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Dopo aver creato il gruppo di disponibilità, è necessario configurare l'integrazione con una tecnologia di cluster, ad esempio Pacemaker per la disponibilità elevata. Per una configurazione con scalabilità in lettura con gruppi di disponibilità, a partire da [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], configurazione di un cluster non è necessaria.

Se è stata seguita la procedura descritta in questo documento, è necessario un gruppo di disponibilità che non è ancora un indice cluster. Il passaggio successivo consiste nell'aggiungere il cluster. Questa configurazione è valida per gli scenari di bilanciamento del carico di read-scale/carico, non è completa per la disponibilità elevata. Per la disponibilità elevata, è necessario aggiungere il gruppo di disponibilità come risorsa cluster. Visualizzare [passaggi successivi](#next-steps) per le istruzioni. 

## <a name="notes"></a>Note

>[!IMPORTANT]
>Dopo aver configurato il cluster e aggiungere il gruppo di disponibilità come risorsa cluster, è possibile usare Transact-SQL per eseguire il failover le risorse del gruppo di disponibilità. Risorse del cluster SQL Server in Linux non sono collegate come strettamente con il sistema operativo perché sono in un Server Failover Cluster WSFC (Windows). Servizio SQL Server non riconosce la presenza del cluster. Tutte le orchestrazioni vengono eseguite mediante gli strumenti di gestione di cluster. In Ubuntu o RHEL utilizzare `pcs`. SLES usare `crm`. 

>[!IMPORTANT]
>Se il gruppo di disponibilità è una risorsa cluster, è presente un problema noto nella versione corrente in cui il failover forzato con perdita di dati a una replica asincrona non funziona. Questo problema verrà risolto nella prossima versione. Failover manuale o automatico in una replica asincrona ha esito positivo.


## <a name="next-steps"></a>Passaggi successivi

[Configurare Cluster di Red Hat Enterprise Linux per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurare Cluster di SUSE Linux Enterprise Server per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurare Cluster di Ubuntu per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)

---
title: Configurare un gruppo di disponibilità distribuito
description: 'In questo argomento viene descritto come creare e configurare un gruppo di disponibilità distribuito Always On. '
ms.custom: seodec18
ms.date: 08/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b311802506ac8d0517026a9258a340e927a10f9
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566560"
---
# <a name="configure-a-distributed-always-on-availability-group"></a>Configurare un gruppo di disponibilità distribuito Always On  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Per creare un gruppo di disponibilità distribuito, è necessario creare due gruppi di disponibilità ognuno con il proprio listener. È quindi possibile combinare questi gruppi di disponibilità in un gruppo di disponibilità distribuito. La procedura seguente illustra un esempio di base in Transact-SQL. Questo esempio non descrive in dettaglio la creazione di gruppi di disponibilità e listener, ma mette in rilievo i requisiti principali.

Per una panoramica tecnica dei gruppi di disponibilità distribuiti, vedere [Gruppi di disponibilità distribuiti](distributed-availability-groups.md).

## <a name="prerequisites"></a>Prerequisites

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>Impostare i listener di endpoint in ascolto per tutti gli indirizzi IP

Assicurarsi che gli endpoint possano comunicare tra i vari gruppi di disponibilità nel gruppo di disponibilità distribuito. Se un gruppo di disponibilità è impostato su una rete specifica dell'endpoint, il gruppo di disponibilità distribuito non funzionerà correttamente. In ogni server che ospita una replica nel gruppo di disponibilità distribuito, configurare il listener per l'ascolto su tutti gli indirizzi IP (`LISTENER_IP = ALL`).

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>Creare un listener per l'ascolto di tutti gli indirizzi IP

Ad esempio, lo script seguente crea un endpoint del listener sulla porta TCP 5022 in ascolto su tutti gli indirizzi IP.  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>Modificare un listener per l'ascolto di tutti gli indirizzi IP

Ad esempio, lo script seguente modifica un endpoint del listener per l'ascolto di tutti gli indirizzi IP.  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>Creare un primo gruppo di disponibilità

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>Creare il gruppo di disponibilità primario nel primo cluster  
Creare un gruppo di disponibilità nel primo cluster di failover di Windows Server (WSFC).   In questo esempio il gruppo di disponibilità è denominato `ag1` per il database `db1`. La replica primaria del gruppo di disponibilità primario è nota come **server primario globale** in un gruppo di disponibilità distribuito. Server1 è il server primario globale in questo esempio.        
  
```sql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
>[!NOTE]
>L'esempio precedente usa il seeding diretto, dove **SEEDING_MODE** è impostato su **AUTOMATIC** per le repliche e il gruppo di disponibilità distribuito. Questa configurazione imposta le repliche secondarie e il gruppo di disponibilità secondario in modo che vengano popolati automaticamente senza richiedere alcun backup e ripristino manuale del database primario.  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>Creare un join delle repliche secondarie al gruppo di disponibilità primario  
È necessario creare un join tra tutte le repliche secondarie al gruppo di disponibilità tramite **ALTER AVAILABILITY GROUP** con l'opzione **JOIN** . Dal momento che in questo esempio viene usato il seeding diretto, è necessario chiamare anche  **ALTER AVAILABILITY GROUP** con l'opzione **GRANT CREATE ANY DATABASE** . Questa impostazione consente al gruppo di disponibilità di creare il database e avviare il seeding automatico dalla replica primaria.  
  
In questo esempio i seguenti comandi vengono eseguiti sulla replica secondaria, `server2`, per creare un join del gruppo di disponibilità `ag1` . Il gruppo di disponibilità può quindi creare database sulla replica secondaria.  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>Quando il gruppo di disponibilità crea un database in una replica secondaria, imposta il proprietario del database come l'account che ha eseguito l'istruzione `ALTER AVAILABILITY GROUP` per concedere l'autorizzazione per la creazione di qualsiasi database. Per informazioni complete, vedere [Concedere le autorizzazioni di creazione di database sulla replica secondaria al gruppo di disponibilità](automatic-seeding-secondary-replicas.md#grantCreate).
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>Creare un listener per il gruppo di disponibilità primario  

Successivamente aggiungere un listener per il gruppo di disponibilità primario sul primo WSFC. In questo esempio il listener viene denominato `ag1-listener`. Per istruzioni dettagliate sulla creazione di un listener, vedere [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>Creare un secondo gruppo di disponibilità  
 Creare quindi un secondo gruppo di disponibilità, `ag2`, nel secondo WSFC. In questo caso il database non è specificato, perché viene eseguito il seeding automatico del database stesso dal gruppo di disponibilità primario.  La replica primaria del gruppo di disponibilità secondario è nota come **server di inoltro** in un gruppo di disponibilità distribuito. In questo esempio server3 è il server d'inoltro. 
  
```sql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
> Il gruppo di disponibilità secondario deve usare lo stesso endpoint del mirroring del database (in questo esempio la porta 5022). In caso contrario, la replica verrà interrotta dopo un failover locale.  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>Creare un join delle repliche secondarie al gruppo di disponibilità secondario  
 In questo esempio i seguenti comandi vengono eseguiti sulla replica secondaria, `server4`, per creare un join del gruppo di disponibilità `ag2` . Il gruppo di disponibilità può quindi creare database sulla replica secondaria per supportare il seeding diretto.  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>Creare un listener per il gruppo di disponibilità secondario  
 Successivamente aggiungere un listener per il gruppo di disponibilità secondario sul secondo WSFC. In questo esempio il listener viene denominato `ag2-listener`. Per istruzioni dettagliate sulla creazione di un listener, vedere [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>Creare un gruppo di disponibilità distribuito nel primo cluster  
 Creare un gruppo di disponibilità distribuito nel primo WSFC (in questo esempio denominato `distributedag` ). Usare il comando **CREATE AVAILABILITY GROUP** con l'opzione **DISTRIBUTED** . Il parametro **AVAILABILITY GROUP ON** specifica i gruppi di disponibilità membri, `ag1` e `ag2`.  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  Il parametro **LISTENER_URL** specifica il listener per ogni gruppo di disponibilità insieme all'endpoint del mirroring del database del gruppo di disponibilità. Questo esempio riguarda la porta `5022` (non la porta `60173` usata per creare il listener). Se si usa un bilanciamento del carico, ad esempio in Azure, [aggiungere una regola per il bilanciamento del carico per la porta del gruppo di disponibilità distribuito](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group). Aggiungere la regola per la porta del listener, oltre che alla porta dell'istanza di SQL Server. 
  
## <a name="join-distributed-availability-group-on-second-cluster"></a>Aggiungere un gruppo di disponibilità distribuito nel secondo cluster  
 Creare quindi un join del gruppo di disponibilità distribuito nel secondo WSFC.  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="failover"></a> Aggiungere il database nella replica secondaria del secondo gruppo di disponibilità
Quando il database nella replica secondaria del secondo gruppo di disponibilità è in uno stato di ripristino, è necessario aggiungerlo manualmente al gruppo di disponibilità.

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="failover"></a> Failover su un gruppo di disponibilità secondario  

In questo momento è supportato solo il failover manuale. Per eseguire il failover manuale di un gruppo di disponibilità distribuito:

1. Per evitare la perdita di dati, impostare il gruppo di disponibilità distribuito sulla modalità commit sincrono.
1. Attendere che il gruppo di disponibilità distribuito sia sincronizzato.
1. Nella replica primaria globale impostare il ruolo del gruppo di disponibilità distribuito su `SECONDARY`.
1. Verificare la conformità del failover.
1. Eseguire il failover del gruppo di disponibilità primario.

Gli esempi Transact-SQL seguenti illustrano i passaggi dettagliati per il failover del gruppo di disponibilità distribuito denominato `distributedag`:

1. Impostare il gruppo di disponibilità distribuito per il commit sincrono eseguendo il codice seguente *sia* nel server primario globale che nel server d'inoltro.   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   >[!NOTE]
   >In un gruppo di disponibilità distribuito, lo stato di sincronizzazione tra i due gruppi di disponibilità dipende dalla modalità di disponibilità di entrambe le repliche. Per la modalità con commit sincrono, il gruppo di disponibilità primario corrente e quello secondario corrente devono essere entrambi configurati con la modalità di disponibilità `SYNCHRONOUS_COMMIT`. Per questo motivo, è necessario eseguire lo script precedente nella replica primaria globale e nel server di inoltro.

1. Attendere che lo stato del gruppo di disponibilità distribuito diventi `SYNCHRONIZED`. Eseguire la query seguente nel server primario globale corrispondente alla replica primaria del gruppo di disponibilità primario. 
    
      ```sql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    Continuare dopo che il gruppo di disponibilità **synchronization_state_desc** diventa `SYNCHRONIZED`. Se **synchronization_state_desc** non è `SYNCHRONIZED`, eseguire il comando ogni cinque secondi fino a quando non viene modificato. Non continuare fino a **synchronization_state_desc** = `SYNCHRONIZED`. 

1. Nel server primario globale impostare il ruolo del gruppo di disponibilità distribuito su `SECONDARY`. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    A questo punto, il gruppo di disponibilità distribuito non è disponibile.

1. Verificare la conformità del failover. Eseguire la query riportata di seguito:

    ```sql
    SELECT ag.name, 
        drs.database_id, 
        drs.group_id, 
        drs.replica_id, 
        drs.synchronization_state_desc, 
        drs.end_of_log_lsn 
    FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
    WHERE drs.group_id = ag.group_id; 
    ```  
    Il gruppo di disponibilità è pronto per il failover quando **synchronization_state_desc** è `SYNCHRONIZED` e **end_of_log_lsn** è lo stesso per entrambi i gruppi di disponibilità. 

1. Failover dal gruppo di disponibilità primaria al gruppo di disponibilità secondaria. Eseguire il comando seguente nell'istanza di SQL Server che ospita la replica primaria del gruppo di disponibilità secondario. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    Dopo questo passaggio, il gruppo di disponibilità distribuito sarà disponibile.
      
Dopo aver completato i passaggi precedenti, si verifica il failover del gruppo di disponibilità distribuito senza perdita di dati. Se i gruppi di disponibilità si trovano a una distanza geografica che provoca latenza, reimpostare la modalità di disponibilità su ASYNCHRONOUS_COMMIT. 
  
## <a name="remove-a-distributed-availability-group"></a>Rimuovere un gruppo di disponibilità distribuito  
 L'istruzione Transact-SQL seguente rimuove un gruppo di disponibilità distribuito denominato `distributedag`:  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>Creare un gruppo di disponibilità distribuito in istanze del cluster di failover

È possibile creare un gruppo di disponibilità distribuito usando un gruppo di disponibilità in un'istanza del cluster di failover. In questo caso, non è necessario un listener del gruppo di disponibilità. Usare il nome di rete virtuale (VNN) per la replica primaria dell'istanza FCI. L'esempio seguente illustra un gruppo di disponibilità distribuito denominato SQLFCIDAG. Un gruppo di disponibilità è SQLFCIAG. SQLFCIAG ha due repliche FCI. Il nome di rete virtuale per la replica primaria FCI è SQLFCIAG-1 e il nome di rete virtuale per la replica FCI secondaria è SQLFCIAG-2. Il gruppo di disponibilità distribuito include anche SQLAG-DR, per il ripristino di emergenza.

![Gruppo di disponibilità AlwaysOn distribuito](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 Il DDL seguente crea questo gruppo di disponibilità distribuito. 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

L'URL del listener è il nome di rete virtuale dell'istanza FCI primaria.

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>Eseguire il failover manuale di FCI in un gruppo di disponibilità distribuito

Per eseguire manualmente il failover del gruppo di disponibilità FCI, aggiornare il gruppo di disponibilità distribuito in modo da riflettere la modifica dell'URL del listener. Ad esempio, eseguire il DDL seguente sul gruppo di disponibilità primaria e il gruppo di disponibilità secondaria di SQLFCIAG:

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>Passaggi successivi

 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  

---
title: Associare un database con tabelle con ottimizzazione per la memoria a un pool di risorse
ms.custom: seo-dt-2019
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8bc12c4ef792fe1df3d9855df72e025a2dafa6ac
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412757"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>Associare un database con tabelle con ottimizzazione per la memoria a un pool di risorse
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Un pool di risorse rappresenta un subset di risorse fisiche che è possibile governare. Per impostazione predefinita, i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono associati alle risorse del pool di risorse predefinito e usano queste ultime. Per evitare che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tutte le risorse vengano usate da una o più tabelle ottimizzate per la memoria e che altri utenti utilizzino la memoria necessaria per le tabelle ottimizzate per la memoria, è consigliabile creare un pool di risorse distinto per gestire l'utilizzo di memoria per il database con tabelle ottimizzate per la memoria.  
  
 Un database può essere associato a un solo pool di risorse. Tuttavia, è possibile associare più database allo stesso pool. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di associare un database senza tabelle ottimizzate per la memoria a un pool di risorse, ma questa operazione non ha alcun effetto. Può essere opportuno associare un database a un pool di risorse denominato se, in futuro, si intende creare tabelle ottimizzate per la memoria nel database.  
  
 Prima di poter associare un database a un pool di risorse, è necessario che sia presente sia il database che il pool di risorse. L'associazione viene applicata alla successiva connessione del database. Per altre informazioni, vedere [Stati del database](../../relational-databases/databases/database-states.md) .  
  
 Per informazioni sui pool di risorse, vedere [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
## <a name="steps-to-bind-a-database-to-a-resource-pool"></a>Passaggi per associare un database a un pool di risorse  
  
1.  [Creare il database e il pool di risorse](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreatePool)  
  
    1.  [Creare il database](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateDatabase)  
  
    2.  [Determinare il valore minimo per MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT.](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DeterminePercent)  
  
    3.  [Creare un pool di risorse e configurare la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateResourcePool)  
  
2.  [Associare il database al pool.](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DefineBinding)  
  
3.  [Verificare l'associazione](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ConfirmBinding)  
  
4.  [Rendere effettiva l'associazione](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_MakeBindingEffective)  
  
 Altro contenuto di questo argomento  
  
-   [Modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)  
  
-   [Percentuale di memoria disponibile per indici e tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)  
  
##  <a name="bkmk_CreatePool"></a> Creare il database e il pool di risorse  
 È possibile creare il database e il pool di risorse in qualsiasi ordine. La cosa importante è che entrambi esistano prima di associare il database al pool di risorse.  
  
###  <a name="bkmk_CreateDatabase"></a> Creare il database  
 Con l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene creato un database denominato IMOLTP_DB in cui saranno incluse una o più tabelle ottimizzate per la memoria. Il percorso \<UnitàPercorso> deve esistere prima dell'esecuzione del comando.  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
###  <a name="bkmk_DeterminePercent"></a> Determinare il valore minimo per MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT.  
 Dopo aver determinato la memoria necessaria per le tabelle ottimizzate per la memoria, è necessario determinare la percentuale di memoria disponibile necessaria e impostare le percentuali di memoria su un valore uguale o superiore.  
  
 **Esempio:**    
In questo esempio si suppone che sia stato calcolato che gli indici e le tabelle ottimizzate per la memoria richiedano 16 GB di memoria. Si suppone inoltre che siano stati riservati 32 GB di memoria per l'utilizzo da parte dell'utente.  
  
 A prima vista, si potrebbe ritenere corretto impostare MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT su 50 (16 è il 50% di 32).  Tuttavia, questo valore non garantirebbe memoria sufficiente alle tabelle ottimizzate per la memoria. Nella tabella seguente ([la sezione relativa alla percentuale di memoria disponibile per indici e tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)) è possibile notare che se si riservano 32 GB di memoria, solo l'80% di tale valore sarà disponibile per gli indici e le tabelle ottimizzate per la memoria.  Pertanto, le percentuali minima e massima sono calcolate in base alla memoria disponibile, non alla memoria riservata.  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 Inserimento di numeri reali:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 È pertanto necessario almeno il 62,5% della memoria disponibile per soddisfare il requisito di 16 GB degli indici e delle tabelle ottimizzate per la memoria.  Poiché i valori di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT devono essere numeri interi, viene impostato un valore pari almeno al 63%.  
  
###  <a name="bkmk_CreateResourcePool"></a> Creare un pool di risorse e configurare la memoria  
 Quando si configura la memoria per le tabelle ottimizzate per la memoria, la pianificazione della capacità deve essere eseguita in base a MIN_MEMORY_PERCENT, non MAX_MEMORY_PERCENT.  Per informazioni su MIN_MEMORY_PERCENT e su MAX_MEMORY_PERCENT, vedere [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md). Ciò rende maggiormente stimabile la disponibilità di memoria per le tabelle ottimizzate per la memoria, poiché MIN_MEMORY_PERCENT causa un utilizzo elevato di memoria per gli altri pool di risorse, al fine di garantire la disponibilità. Per garantire che la memoria sia disponibile ed evitare condizioni di memoria insufficiente, i valori di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT devono essere uguali. Vedere la sezione relativa alla [percentuale di memoria disponibile per indici e tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable) per i valori in base alla quantità di memoria riservata.  
  
 Per altre informazioni sull'uso di un ambiente di VM, vedere [Procedure consigliate: Uso di OLTP in memoria in un ambiente di VM](https://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) .  
  
 Con il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene creato un pool di risorse denominato Pool_IMOLTP con metà della memoria disponibile per l'utilizzo.  Dopo la creazione del pool, Resource Governor viene riconfigurato in modo da includere Pool_IMOLTP.  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bkmk_DefineBinding"></a> Associare il database al pool.  
 Usare la funzione di sistema `sp_xtp_bind_db_resource_pool` per associare il database al pool di risorse. La funzione accetta due parametri: il nome del database e il nome del pool di risorse.  
  
 Con l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene definita un'associazione del database IMOLTP_DB al pool di risorse Pool_IMOLTP. L'associazione non diventa effettiva finché il database non viene portato online.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 La funzione di sistema sp_xtp_bind_db_resourece_pool accetta due parametri di stringa: database_name e pool_name.  
  
##  <a name="bkmk_ConfirmBinding"></a> Verificare l'associazione  
 Verificare l'associazione, annotando l'ID del pool di risorse per IMOLTP_DB. Non deve essere NULL.  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
##  <a name="bkmk_MakeBindingEffective"></a> Rendere effettiva l'associazione  
 Dopo aver associato il database al pool di risorse, è necessario portare il database offline, quindi di nuovo online per rendere effettiva l'associazione. Se in precedenza il database era stato associato a un pool diverso, tramite questa operazione la memoria allocata verrà rimossa dal pool di risorse precedente e verranno usate le allocazioni di memoria per gli indici e la tabella ottimizzata per la memoria provenienti dal pool di risorse appena associato al database.  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 Il database è ora associato al pool di risorse.  
  
##  <a name="bkmk_ChangeAllocation"></a> Modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente  
 Se si aggiunge altra memoria al server o se cambia la quantità di memoria necessaria per le tabelle ottimizzate per la memoria, può essere necessario modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT. Nei passaggi seguenti viene illustrato come modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool di risorse. Per informazioni sui valori da usare per MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT, vedere la sezione seguente.  Per altre informazioni, vedere l'argomento [Procedure consigliate: Uso di OLTP in memoria in un ambiente di VM](https://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) .  
  
1.  Usare `ALTER RESOURCE POOL` per modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT.  
  
2.  Usare `ALTER RESURCE GOVERNOR` per riconfigurare Resource Governor con i nuovi valori.  
  
 **Codice di esempio**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
##  <a name="bkmk_PercentAvailable"></a> Percentuale di memoria disponibile per indici e tabelle ottimizzate per la memoria  
 Se si esegue il mapping di un database con tabella ottimizzata per la memoria e un carico di lavoro di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] allo stesso pool di risorse, tramite Resource Governor viene impostata una soglia interna per l'utilizzo di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] in modo tale che gli utenti del pool non abbiano conflitti per l'utilizzo del pool. In generale, la soglia per l'utilizzo di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è di circa l'80% del pool. Nella tabella seguente vengono illustrate le soglie effettive per varie dimensioni di memoria.  
  
 Quando si crea un pool di risorse dedicato per il database [!INCLUDE[hek_2](../../includes/hek-2-md.md)] , è necessario stimare la quantità di memoria fisica necessaria per le tabelle in memoria dopo aver tenuto conto delle versioni di riga e della crescita dei dati. Dopo avere stimato la memoria necessaria, è possibile creare un pool di risorse con una percentuale della memoria di destinazione di commit per l'istanza di SQL come indicato nella colonna 'committed_target_kb' nella DMV `sys.dm_os_sys_info` (vedere [sys.dm_os_sys_information](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)). Ad esempio, è possibile creare un pool di risorse P1 con il 40% della memoria totale disponibile per l'istanza. Da questo 40%, il motore di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ottiene una percentuale inferiore per archiviare i dati di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  Ciò garantisce che [!INCLUDE[hek_2](../../includes/hek-2-md.md)] non utilizzi tutta la memoria del pool.  Il valore della percentuale inferiore dipende dalla memoria riservata alla destinazione. Nella tabella seguente viene descritta la memoria disponibile per il database [!INCLUDE[hek_2](../../includes/hek-2-md.md)] in un pool di risorse (denominato o predefinito) prima che venga generato un errore di memoria insufficiente.  
  
|Memoria riservata di destinazione|Percentuale disponibile per le tabelle in memoria|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|> 96 GB|90%|  
  
 Ad esempio, se la 'memoria riservata alla destinazione' è di 100 GB e si stima che gli indici e le tabelle ottimizzate per la memoria richiedano 60 GB di memoria, è possibile creare un pool di risorse con MAX_MEMORY_PERCENT = 67 (60 GB necessari/0,90 = 66,667 GB - arrotondamento per eccesso a 67 GB; 67 GB/100 GB installato = 67%) per garantire i 60 GB di memoria necessari agli oggetti di [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
 Dopo l'associazione di un database a un pool di risorse denominato, usare la query seguente per visualizzare le allocazioni di memoria tra pool di risorse diversi.  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 In questo esempio campione viene illustrato che la memoria usata dagli oggetti ottimizzati per la memoria è 1356 MB nel pool di risorse, PoolIMOLTP, con un limite superiore di 2307 MB. Il limite superiore controlla la memoria totale che può essere usata dagli oggetti ottimizzati per la memoria di utente e sistema dei quali è stato eseguito il mapping a questo pool.  
  
 **Esempio di output**   
Questo output è tratto dal database e dalle tabelle create in precedenza.  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 Per altre informazioni, vedere [sys.dm_resource_governor_resource_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 Se il database non viene associato a un pool di risorse denominato, viene associato al pool predefinito ('default'). Poiché il pool di risorse predefinito è usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la maggior parte delle altre allocazioni, non sarà possibile monitorare in modo accurato la memoria usata dalle tabelle ottimizzate per la memoria tramite la DMV sys.dm_resource_governor_resource_pools per il database di interesse.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Modificare le impostazioni del pool di risorse](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Eliminare un pool di risorse](../../relational-databases/resource-governor/delete-a-resource-pool.md)  
  
  

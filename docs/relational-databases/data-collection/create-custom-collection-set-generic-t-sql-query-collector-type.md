---
title: Creare un set di raccolta personalizzato che usa il tipo agente di raccolta Query T-SQL generico | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7184a6d2e3f10889233f6ed4b2057755dc9bdd72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653438"
---
# <a name="create-custom-collection-set---generic-t-sql-query-collector-type"></a>Creare un set di raccolta personalizzato che usa il tipo agente di raccolta Query T-SQL generico
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile creare un set di raccolta personalizzato con elementi della raccolta che utilizzano il tipo di agente di raccolta Query T-SQL generico tramite le stored procedure fornite con l'agente di raccolta dati. Il completamento di questa attività comporta l'utilizzo dell'Editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per eseguire le procedure descritte di seguito:  
  
-   Configurazione delle pianificazioni di caricamento.  
  
-   Definizione e creazione del set di raccolta.  
  
-   Definizione e creazione di un elemento della raccolta.  
  
-   Verifica dell'esistenza del set di raccolta e degli elementi della raccolta.  
  
> [!NOTE]  
>  Prima di creare un set di raccolta personalizzato è necessario configurare i parametri della raccolta dati. Per altre informazioni, vedere [Configurazione dei parametri per la raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md).  
  
### <a name="define-and-create-the-collection-set"></a>Definizione e creazione del set di raccolta  
  
1.  Definire un nuovo set di raccolta utilizzando la stored procedure sp_syscollector_create_collection_set.  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     È possibile impostare la modalità di raccolta su 0 (in cache) o su 1 (non in cache).  
  
     Il livello di registrazione può essere impostato su 0, 1 o 2.  
  
     Le seguenti pianificazioni preconfigurate vengono fornite con l'agente di raccolta dati:  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     Se non si desidera utilizzare una delle pianificazioni fornite è possibile creare una nuova pianificazione e utilizzarla per il set di raccolta. Per altre informazioni, vedere [Creare e collegare le pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="define-and-create-a-collection-item"></a>Definizione e creazione di un elemento della raccolta  
  
1.  Poiché il nuovo elemento della raccolta è basato su un tipo di agente di raccolta generico già installato, è possibile eseguire il codice seguente per impostare il GUID in modo che corrisponda al tipo di agente di raccolta Query T-SQL generico.  
  
    ```sql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  Utilizzare la stored procedure sp_syscollector_create_collection_item per creare l'elemento della raccolta. Dichiarare lo schema per l'elemento della raccolta in modo che ne venga eseguito il mapping allo schema richiesto per il tipo di agente di raccolta Query T-SQL generico.  
  
    ```sql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>Verifica dell'esistenza del nuovo set di raccolta a dell'elemento della raccolta  
  
1.  Prima di avviare il nuovo set di raccolta, eseguire la query seguente per verificare che il nuovo set di raccolta e l'elemento della raccolta siano stati creati.  
  
    ```sql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     È anche possibile effettuare un controllo visivo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. In Esplora oggetti espandere il nodo **Gestione** , quindi **Raccolta dati**. Verrà visualizzato il nuovo set di raccolta. L'icona con il cerchio rosso per il set di raccolta indica che quest'ultimo è arrestato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente vengono combinati gli esempi documentati nei passaggi precedenti. Si noti che la frequenza di raccolta impostata per l'elemento della raccolta (5 secondi) viene ignorata, poiché la modalità di raccolta del set di raccolta è impostata su 0 (modalità cache). Per altre informazioni, vedere [Data Collection](../../relational-databases/data-collection/data-collection.md).  
  
```sql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Gestione pianificazioni](../../ssms/agent/manage-schedules.md)   
 [Avviare o arrestare un set di raccolta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  

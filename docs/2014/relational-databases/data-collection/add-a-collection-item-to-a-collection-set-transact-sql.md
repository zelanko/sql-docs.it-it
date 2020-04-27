---
title: Aggiungere un elemento della raccolta a un set di raccolta (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f3e7c74fcaebb0aaaf246cba94e32c6b602b6e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873585"
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>Aggiunta di un elemento della raccolta a un set di raccolta (Transact-SQL)
  È possibile aggiungere un elemento della raccolta a un set di raccolta esistente utilizzando le stored procedure fornite con l'agente di raccolta dati.  
  
 Eseguire i seguenti passaggi utilizzando l'Editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>Aggiunta di un elemento della raccolta a un set di raccolte  
  
1.  Arrestare il set di raccolta a cui aggiungere l'elemento eseguendo la stored procedure **sp_syscollector_stop_collection_set** . Ad esempio, per arrestare un set di raccolta denominato "Test Collection Set", eseguire le istruzioni seguenti:  
  
    ```sql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  È anche possibile arrestare il set di raccolta utilizzando Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Avviare o arrestare un set di raccolta](start-or-stop-a-collection-set.md).  
  
2.  Dichiarare il set di raccolta al quale si desidera aggiungere l'elemento della raccolta. Nel codice seguente viene fornito un esempio su come dichiarare l'ID del set di raccolta.  
  
    ```sql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  Dichiarare il tipo di agente di raccolta. Nel codice seguente viene fornito un esempio su come dichiarare il tipo di agente di raccolta Query T-SQL generico.  
  
    ```sql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     È possibile eseguire il codice seguente per ottenere un elenco dei tipi di agente di raccolta installati:  
  
    ```sql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  Eseguire la stored procedure **sp_syscollector_create_collection_item** per creare l'elemento della raccolta. È necessario dichiarare lo schema per l'elemento della raccolta in modo tale da eseguirne il mapping allo schema richiesto per il tipo di agente di raccolta desiderato. Nell'esempio seguente viene utilizzato lo schema di input Query T-SQL generico.  
  
    ```sql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  Prima di avviare il set di raccolta aggiornato, eseguire la query seguente per verificare che il nuovo elemento della raccolta sia stato creato:  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     I set di raccolta e i rispettivi elementi della raccolta sono visualizzati nella scheda **Risultati** .  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un set di raccolta personalizzato che usa il tipo agente di raccolta Query T-SQL generico &#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  

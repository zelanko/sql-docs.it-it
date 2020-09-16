---
title: Ripristinare un database e associarlo a un pool di risorse | Microsoft Docs
description: Informazioni sul ripristino di un database con tabelle ottimizzate per la memoria in SQL Server. Seguire le procedure consigliate associando il database a un pool di risorse denominato.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f5035a7dd7818e14ec594d04edabad138242527
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546931"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>Ripristinare un database e associarlo a un pool di risorse
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Anche se si dispone di memoria sufficiente per ripristinare un database con tabelle ottimizzate per la memoria, è possibile seguire le procedure consigliate e associare il database a un pool di risorse denominato. Poiché il database deve essere già presente per poter essere associato al pool, il ripristino del database è un processo costituito da più passaggi. In questo argomento viene illustrato tale processo.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Ripristino di un database con tabelle ottimizzate per la memoria  
 I passaggi seguenti consentono di ripristinare completamente il database IMOLTP_DB e di associarlo al pool Pool_IMOLTP.  
  
1.  [Ripristino con NORECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_NORECOVERY)  
  
2.  [Creazione del pool di risorse](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_createPool)  
  
3.  [Associazione del database e del pool di risorse](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_bind)  
  
4.  [Ripristino con RECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_RECOVERY)  
  
5.  [Monitoraggio delle prestazioni del pool di risorse](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_Monitor)  
  
###  <a name="restore-with-norecovery"></a><a name="bkmk_NORECOVERY"></a> Ripristino con NORECOVERY  
 Il ripristino di un database con NORECOVERY comporta la creazione del database e il ripristino dell'immagine disco senza l'uso di memoria.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
###  <a name="create-the-resource-pool"></a><a name="bkmk_createPool"></a> Creazione del pool di risorse  
 Il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di creare un pool di risorse denominato Pool_IMOLTP con il 50% della memoria disponibile per l'uso.  Dopo la creazione del pool, Resource Governor viene riconfigurato in modo da includere Pool_IMOLTP.  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
###  <a name="bind-the-database-and-resource-pool"></a><a name="bkmk_bind"></a> Associazione del database e del pool di risorse  
 Usare la funzione di sistema `sp_xtp_bind_db_resource_pool` per associare il database al pool di risorse. La funzione accetta due parametri: il nome del database seguito dal nome del pool di risorse.  
  
 Con l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene definita un'associazione del database IMOLTP_DB al pool di risorse Pool_IMOLTP. L'associazione non diventa effettiva finché non viene completato il passaggio successivo.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
###  <a name="restore-with-recovery"></a><a name="bkmk_RECOVERY"></a> Ripristino con RECOVERY  
 Quando si ripristina il database con recupero, il database viene portato online e vengono ripristinati tutti i dati.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
###  <a name="monitor-the-resource-pool-performance"></a><a name="bkmk_Monitor"></a> Monitoraggio delle prestazioni del pool di risorse  
 Dopo l'associazione del database al pool di risorse denominato e il ripristino con RECOVERY, monitorare l'oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Statistiche del pool di risorse. Per ulteriori informazioni, vedere [SQL Server - Oggetto Statistiche del pool di risorse](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md).  
  
## <a name="see-also"></a>Vedere anche  
 [a un pool di risorse, vedere l'argomento](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [SQL Server - Oggetto Statistiche del pool di risorse](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  

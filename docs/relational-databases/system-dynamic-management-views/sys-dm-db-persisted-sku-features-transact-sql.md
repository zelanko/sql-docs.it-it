---
title: sys.dm_db_persisted_sku_features (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9d8001765a06ce432ea8f5f7e3081e4a54e7efa
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202070"
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Alcune funzionalità del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] comportano una modifica del metodo di archiviazione delle informazioni nei file di database da parte del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Queste funzionalità sono disponibili solo in edizioni specifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un database che contiene queste funzionalità non può essere spostato a un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non le supporta. Usare la vista a gestione dinamica sys.dm_db_persisted_sku_features per elencare le funzionalità specifiche dell'edizione abilitate nel database corrente.
  
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Nome esterno della funzionalità abilitata nel database ma non supportata in tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa funzionalità deve essere rimossa prima di poter eseguire la migrazione del database in tutte le edizioni disponibili di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|feature_id|**int**|ID funzionalità associato alla funzionalità. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] (Indici per tabelle con ottimizzazione per la memoria).|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il database.  
  
## <a name="remarks"></a>Note  
 Se nessuna funzionalità che può essere limitata da un'edizione specifica viene utilizzata dal database, la vista non restituisce alcuna riga.  
  
 Sys.dm_db_persisted_sku_features può elencare le funzionalità di modifica del database seguenti come limitate a determinati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edizioni:  
  
-   **ChangeCapture**: Indica che Change Data Capture è abilitato in un database. Per rimuovere change data capture, usare il [Sys. sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) stored procedure. Per altre informazioni, vedere [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: Indica che almeno una tabella dispone di un indice columnstore. Per abilitare un database da spostare in un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supporta questa funzionalità, usare il [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) oppure [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) istruzione per rimuovere l'indice columnstore. Per altre informazioni, vedere [gli indici Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **La compressione**: Indica che la compressione dei dati o il formato di archiviazione vardecimal viene utilizzato almeno in una tabella o in un indice. Per abilitare un database da spostare in un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supporta questa funzionalità, usare il [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oppure [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) istruzione per rimuovere la compressione dei dati. Per rimuovere il formato di archiviazione vardecimal, utilizzare l'istruzione sp_tableoption. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: Indica che il database utilizza più contenitori FILESTREAM. Il database ha un filegroup FILESTREAM con più contenitori (file). Per altre informazioni, vedere [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **A OLTP in memoria**: Indica che il database utilizza OLTP in memoria. Al database è associato il filegroup MEMORY_OPTIMIZED_DATA. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **Il partizionamento.** Indica che il database contiene tabelle partizionate, indici partizionati, schemi di partizione o funzioni di partizione. Per consentire di spostare un database in un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa da Enterprise o Developer, non è sufficiente modificare la tabella affinché sia inclusa in una singola partizione, ma è necessario rimuovere la tabella partizionata. Se la tabella contiene dati, utilizzare SWITCH PARTITION per convertire ogni partizione in una tabella non partizionata. Eliminare quindi la tabella partizionata, lo schema di partizione e la funzione di partizione.  
  
-   **TransparentDataEncryption.** Indica che un database viene crittografato utilizzando Transparent Data Encryption. Per rimuovere Transparent Data Encryption, utilizzare l'istruzione ALTER DATABASE. Per altre informazioni sulla crittografia trasparente del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1, queste funzionalità sono disponibili in più [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edizioni e a titolo esemplificativo Enterprise o Developer Edition solo.

 Per determinare se in un database sono in uso funzionalità disponibili solo in edizioni specifiche, eseguire l'istruzione seguente nel database:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Edizioni e le funzionalità supportate di SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Edizioni e le funzionalità supportate di SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  

---
title: sys. dm_operation_status (database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c49e4e01dd8ddaf0667546a8cc221a7918f42c81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70911207"
---
# <a name="sysdm_operation_status-azure-sql-database"></a>sys.dm_operation_status (Database di SQL Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Restituisce informazioni sulle operazioni eseguite sui database in un server del [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|ID dell'operazione. Non Null.|  
|resource_type|**int**|Indica il tipo di risorsa in cui viene eseguita l'operazione. Non Null. Nella versione corrente questa vista tiene traccia delle operazioni eseguite solo nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e il valore intero corrispondente è 0.|  
|resource_type_desc|**nvarchar (2048)**|Descrizione del tipo di risorsa in cui viene eseguita l'operazione. Nella versione corrente, questa vista tiene traccia delle operazioni eseguite solo nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|major_resource_id|**sql_variant**|Nome del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] in cui viene eseguita l'operazione. Non Null.|  
|minor_resource_id|**sql_variant**|Solo per uso interno. Non Null.|  
|operation|**nvarchar (60)**|Operazione eseguita su un [!INCLUDE[ssSDS](../../includes/sssds-md.md)], ad esempio CREATE o ALTER.|  
|state|**tinyint**|Stato dell'operazione.<br /><br /> 0 = In sospeso<br />1 = In corso<br />2 = Completato<br />3 = Non completato<br />4 = Annullato|  
|state_desc|**nvarchar (120)**|PENDING = l'operazione è in attesa della disponibilità della quota o delle risorse.<br /><br /> IN_PROGRESS = l'operazione è stata avviata ed è in esecuzione.<br /><br /> COMPLETED = operazione completata.<br /><br /> FAILED = operazione non riuscita. Per informazioni dettagliate, vedere la colonna **error_desc** .<br /><br /> CANCELLED = l'operazione è stata arrestata su richiesta dell'utente.|  
|percent_complete|**int**|Percentuale dell'operazione completata. I valori non sono continui e i valori validi sono elencati di seguito. Non NULL.<br/><br/>0 = operazione non avviata<br/>50 = operazione in corso<br/>100 = operazione completata|  
|error_code|**int**|Codice che indica l'errore che si è verificato durante un'operazione non riuscita. Se il valore è 0, indica che l'operazione è stata completata correttamente.|  
|error_desc|**nvarchar (2048)**|Descrizione dell'errore che si è verificato durante un'operazione non riuscita.|  
|error_severity|**int**|Livello di gravità dell'errore che si è verificato durante un'operazione non riuscita. Per ulteriori informazioni sui livelli di gravità degli errori, vedere [motore di database gravità degli errori](https://go.microsoft.com/fwlink/?LinkId=251052).|  
|error_state|**int**|Riservato a un uso futuro. Non è garantita la compatibilità con le versioni future.|  
|start_time|**datetime**|Timestamp dell'inizio dell'operazione.|  
|last_modify_time|**datetime**|Timestamp dell'ultima modifica del record per un'operazione a esecuzione prolungata. In caso di operazioni completate correttamente, in questo campo viene visualizzato il timestamp del completamento dell'operazione.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Questa vista è disponibile solo nel database **Master** per l'account di accesso dell'entità di livello server.  
  
## <a name="remarks"></a>Osservazioni  
 Per utilizzare questa vista, è necessario essere connessi al database **Master** . Utilizzare la `sys.dm_operation_status` vista nel database **Master** del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server per tenere traccia dello stato delle operazioni seguenti eseguite su un [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:  
  
-   Creazione del database  
  
-   Copiare il database. Copia database crea un record in questa visualizzazione nel server di origine e in quello di destinazione.  
  
-   Modificare database  
  
-   Modifica del livello delle prestazioni di un livello del servizio  
  
-   Modificare il livello di servizio di un database, passando ad esempio da Base a Standard.  
  
-   Configurazione di una relazione di replica geografica  
  
-   Interruzione di una relazione di replica geografica.  
  
-   Ripristina database  
  
-   Elimina database  
  
## <a name="example"></a>Esempio  
 Mostra le operazioni di replica geografica più recenti associate al database ' MyDB '.  
  
```  
SELECT * FROM sys.dm_operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica con replica geografica &#40;database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys. dm_geo_replication_link_status &#40;database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys. geo_replication_links &#40;database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;database SQL di Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  

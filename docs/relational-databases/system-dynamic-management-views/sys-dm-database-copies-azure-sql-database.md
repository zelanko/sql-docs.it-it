---
title: DM database_copies (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6b5a0a656693d66e701642c9c2202c2862136a54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741959"
---
# <a name="sysdmdatabasecopies-azure-sql-database"></a>sys.dm_database_copies (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sulla copia del database.  
  
Per restituire informazioni sui collegamenti di replica geografica, usare il [Sys. geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md) oppure [DM geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) viste (disponibile nel Database SQL V12).
  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database corrente nella vista `sys.databases`.|  
|**start_date**|**datetimeoffset**|Ora UTC in un data center del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] regionale in cui è stata avviata la copia del database.|  
|**modify_date**|**datetimeoffset**|Ora UTC in un data center del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] regionale in cui è stata completata la copia del database. Al momento, il nuovo database è transazionalmente coerente con il database primario. Le informazioni sul completamento viene aggiornati ogni minuto.<br /><br />Ora UTC che riflette l'ultimo aggiornamento del campo percent_complete.|  
|**percent_complete**|**real**|Percentuale di byte copiati. I valori validi sono compresi tra 0 e 100. Il [!INCLUDE[ssSDS](../../includes/sssds-md.md)] potrebbe recuperare automaticamente da alcuni errori, ad esempio il failover, e riavviare la copia del database. In questo caso, percent_complete inizierebbe di nuovo da 0.|  
|**error_code**|**int**|Se maggiore di 0, il codice che indica l'errore che si è verificato durante copia. Il valore è uguale a 0 se non si sono verificati errori.|  
|**error_desc**|**nvarchar(4096)**|Descrizione dell'errore che si è verificato durante la copia.|  
|**error_severity**|**int**|Restituisce 16 se la copia del database ha esito negativo.|  
|**error_state**|**int**|Restituisce 1 se la copia ha esito negativo.|  
|**copy_guid**|**uniqueidentifier**|ID univoco dell'operazione di copia.|  
|**partner_server**|**sysname**|Nome del server di Database SQL in cui viene creata la copia.|  
|**partner_database**|**sysname**|Nome della copia del database nel server partner.|  
|**replication_state**|**tinyint**|Lo stato della replica di copia continua per questo database. I valori possibili sono:<br /><br /> 0 = in sospeso. La creazione della copia del database è pianificata ma i passaggi necessari per la preparazione non sono ancora stati completati o sono temporaneamente bloccati dalla quota di seeding.<br /><br /> 1 = Seeding. La copia del database in corso il seeding non è ancora completamente sincronizzato con il database di origine. In questo stato non è possibile connettersi alla copia. Per annullare l'operazione di seeding in corso, è necessario eliminare il database della copia.|  
|**replication_state_desc**|**nvarchar(256)**|Descrizione di replication_state. I valori possibili sono:<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|Campo riservato.|  
|**is_continuous_copy**|**bit**|0 = restituisce 0|  
|**is_target_role**|**bit**|0 = database di origine<br /><br /> 1 = copia del database|  
|**is_interlink_connected**|bit|Campo riservato.|  
|**is_offline_secondary**|bit|Campo riservato.|  
  
## <a name="permissions"></a>Permissions  
 In questa vista è disponibile solo nel **master** database all'account di accesso dell'entità a livello di server.  
  
## <a name="remarks"></a>Note  
 È possibile usare la **DM database_copies** visualizzare il **master** database di origine o destinazione [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. Quando la copia del database ha esito positivo e il nuovo database diventa ONLINE, la riga nel **DM database_copies** visualizzazione viene rimosso automaticamente.  
  
  

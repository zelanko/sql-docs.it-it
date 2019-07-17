---
title: continuous_copy_status (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: cace39108f3f99d5c165f42b4337e837e1fb7c5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121032"
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>sys.dm_continuous_copy_status (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni database utente (V11) che è attualmente occupato in una relazione di copia continua della replikaci. Se è stata avviata più di una relazione di copia continua per un determinato database primario, questa tabella contiene una riga per ogni database secondario attivo.  
  
Se si usa Database SQL V12 è necessario utilizzare [DM geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (poiché *continuous_copy_status* si applica solo alla versione 11).

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|ID univoco del database di replica.|  
|**partner_server**|**sysname**|Nome del server di database SQL collegato.|  
|**partner_database**|**sysname**|Nome del database collegato nel server di database SQL collegato.|  
|**last_replication**|**datetimeoffset**|Timestamp dell'ultima transazione replicata applicata.|  
|**replication_lag_sec**|**int**|Differenza di tempo in secondi tra l'ora corrente e il timestamp dell'ultimo commit della transazione completato nel database primario che non è stato riconosciuto dal database secondario attivo.|  
|**replication_state**|**tinyint**|Lo stato della replica di copia continua per questo database. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 1: Il seeding. La destinazione della replica viene sottoposta a seeding ed è dal punto di vista transazionale in uno stato non coerente. Finché il seeding non viene completato, non è possibile connettersi al database secondario attivo. <br />2: Esegue l'aggiornamento. Il database secondario attivo attualmente esegue l'aggiornamento al database primario e si trova in uno stato coerente dal punto di vista transazionale.<br />3: Ripetere il seeding. Il database secondario attivo automaticamente viene sottoposto nuovamente a seeding a causa di un errore di replica irreversibile.<br />4: Sospeso. Non è presente una relazione di copia continua attiva. Questo stato indica in genere che la larghezza di banda disponibile per l'interlink è insufficiente per il livello di attività di transazione nel database primario. La relazione di copia continua tuttavia rimane invariata.|  
|**replication_state_desc**|**nvarchar(256)**|Descrizione di replication_state. I valori possibili sono:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Questo valore è sempre impostato su 0|  
|**is_target_role**|**bit**|0 = Origine della relazione di copia<br /><br /> 1 = Destinazione della relazione di copia|  
|**is_interlink_connected**|**bit**|1 = L'interlink è connesso.<br /><br /> 0 = L'interlink è disconnesso.|  
  
## <a name="permissions"></a>Permissions  
 Per recuperare i dati, richiede l'appartenenza al **db_owner** ruolo predefinito del database. L'utente dbo, i membri del **dbmanager** ruolo predefinito del database e account di accesso sa possono effettuare query anche questa visualizzazione.  
  
## <a name="remarks"></a>Note  
 Il **continuous_copy_status** vista viene creata nel **risorsa** database ed è visibile in tutti i database, incluso il database master logico. Tuttavia, se si esegue una query su questa vista nel database master logico viene restituito un set vuoto.  
  
 Se la relazione di copia continua viene terminata su un database, la riga per il database nel **continuous_copy_status** visualizzazione scomparirà.  
  
 Come le **DM database_copies** visualizzazione **continuous_copy_status** riflette lo stato della relazione di copia continua in cui il database è entrambi un database primario o attivo secondario . A differenza **DM database_copies**, **continuous_copy_status** contiene molte colonne che riportano informazioni dettagliate sulle operazioni e le prestazioni. Tali colonne includono **last_replication**, e **replication_lag_sec**...  
  
## <a name="see-also"></a>Vedere anche  
 [DM database_copies &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Stored procedure di replica geografica attiva &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  

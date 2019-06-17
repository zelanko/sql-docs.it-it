---
title: sys.dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8acb2fae0aa0edadf1995a0a103ff60b66a912a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686226"
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui servizi SQL Server, Full-text e SQL Server Agent nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Per segnalare informazioni sullo stato di tali servizi, utilizzare la DMV.  
  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Nome del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Full-text, o un servizio di SQL Server Agent. Non può essere null.|  
|startup_type|**int**|Indica la modalità di avvio del servizio. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 0: Altro<br />1: Altro<br />2: Automatico<br />3: Manual<br />4: Disabilitata<br /><br /> Ammette i valori Null.|  
|startup_desc|**nvarchar(256)**|Descrive la modalità di avvio del servizio. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> Altro: Altro (esecuzione avvio)<br />Altro: Altro (avvio del sistema)<br />Automatico: Avvio automatico<br />Manuale: Inizio richiesta<br />Disabilitato: Disabilitata<br /><br /> Non può essere null.|  
|status|**int**|Indica lo stato corrente del servizio. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 1: Stopped<br />2: Altro (avvio in sospeso)<br />3: Altro (in attesa dell'arresto)<br />4: In esecuzione<br />5: Altro (in attesa della ripresa)<br />6: Altro (sospensione in sospeso)<br />7: Paused<br /><br /> Ammette i valori Null.|  
|status_desc|**nvarchar(256)**|Descrive lo stato corrente del servizio. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> Arrestato: Il servizio è stato arrestato.<br />Altro (avvio dell'operazione in sospeso): Il servizio è in corso di avvio.<br />Altro (operazione di arresto in sospeso): Il servizio è in corso l'arresto.<br />corsa: Il servizio è in esecuzione.<br />Altri (continuare le operazioni in sospeso): Il servizio è in sospeso.<br />Altro (in attesa della sospensione): Il servizio è in corso la sospensione.<br />Sospeso: Il servizio è stato sospeso.<br /><br /> Non può essere null.|  
|process_id|**int**|ID di processo del servizio. Non può essere null.|  
|last_startup_time|**datetimeoffset(7)**|Data e ora dell'ultimo avvio del servizio. Ammette i valori Null.|  
|service_account|**nvarchar(256)**|Account autorizzato a controllare il servizio. L'account consente di avviare o arrestare il servizio oppure di modificarne le proprietà. Non può essere null.|  
|filename|**nvarchar(256)**|Percorso e nome file dell'eseguibile del servizio. Non può essere null.|  
|is_clustered|**nvarchar(1)**|Indica se il servizio è installato come risorsa di un server di cluster. Non può essere null.|  
|cluster_nodename|**nvarchar(256)**|Il nome del nodo del cluster su cui è installato il servizio. Ammette i valori Null.|
|instant_file_initialization_enabled|**nvarchar(1)**|Specifica se l'inizializzazione immediata dei file è abilitato per il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] servizio.<br /><br />Y = inizializzazione immediata dei file è abilitato per il servizio.<br /><br />N = inizializzazione immediata dei file è disabilitato per il servizio.<br /><br /> Ammette i valori Null.<br /><br /> **Nota:** Non è applicabile ad altri servizi, ad esempio SQL Server Agent.<br /><br /> **Si applica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (A partire [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  

## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  

---
title: sys. dm_server_services (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: a480ba134a4f3049f7501cb68a0331ac8fdd386b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095375"
---
# <a name="sysdm_server_services-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sul servizio SQL Server, full-text, Launchpad di SQL Server (SQL Server 2017 +) e SQL Server Agent Services nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per segnalare informazioni sullo stato di tali servizi, utilizzare la DMV.  
  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Nome del servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], full-text o SQL Server Agent. Non può essere null.|  
|startup_type|**int**|Indica la modalità di avvio del servizio. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> 0: altro<br />1: altro<br />2: automatico<br />3: manuale<br />4: disabilitato<br /><br /> Ammette i valori Null.|  
|startup_type_desc|**nvarchar(256)**|Descrive la modalità di avvio del servizio. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> Altro: altro (avvio avvio)<br />Altro: altro (avvio del sistema)<br />Automatico: avvio automatico<br />Manuale: avvio della richiesta<br />Disabilitato: disabilitato<br /><br /> Non può essere null.|  
|status|**int**|Indica lo stato corrente del servizio. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> 1: arrestato<br />2: altro (avvio in sospeso)<br />3: altro (arresto in sospeso)<br />4: in esecuzione<br />5: altro (continua in sospeso)<br />6: altro (sospensione in sospeso)<br />7: in pausa<br /><br /> Ammette i valori Null.|  
|status_desc|**nvarchar(256)**|Descrive lo stato corrente del servizio. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> Arrestato: il servizio è stato arrestato.<br />Altro (operazione di avvio in sospeso): il servizio è in fase di avvio.<br />Altro (arresta operazione in sospeso): il servizio è in fase di arresto.<br />Running: il servizio è in esecuzione.<br />Altro (operazioni continue in sospeso): il servizio è in uno stato in sospeso.<br />Altro (sospensione in sospeso): il servizio è in fase di sospensione.<br />Sospesa: il servizio è sospeso.<br /><br /> Non può essere null.|  
|process_id|**int**|ID di processo del servizio. Non può essere null.|  
|last_startup_time|**datetimeoffset(7)**|Data e ora dell'ultimo avvio del servizio. Ammette i valori Null.|  
|service_account|**nvarchar(256)**|Account autorizzato a controllare il servizio. L'account consente di avviare o arrestare il servizio oppure di modificarne le proprietà. Non può essere null.|  
|filename|**nvarchar(256)**|Percorso e nome file dell'eseguibile del servizio. Non può essere null.|  
|is_clustered|**nvarchar (1)**|Indica se il servizio è installato come risorsa di un server di cluster. Non può essere null.|  
|cluster_nodename|**nvarchar(256)**|Il nome del nodo del cluster su cui è installato il servizio. Ammette i valori Null.|
|instant_file_initialization_enabled|**nvarchar (1)**|Specifica se l'inizializzazione immediata dei file è [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] abilitata per il servizio.<br /><br />Y = inizializzazione immediata dei file abilitata per il servizio.<br /><br />N = l'inizializzazione immediata dei file è disabilitata per il servizio.<br /><br /> Ammette i valori Null.<br /><br /> **Nota:** Non si applica ad altri servizi, ad esempio la SQL Server Agent.<br /><br /> **Si applica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a [!INCLUDE[sssql11](../../includes/sssql11-md.md)] partire da SP4 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e SP1 e versioni successive).|  

## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys. dm_server_registry &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  

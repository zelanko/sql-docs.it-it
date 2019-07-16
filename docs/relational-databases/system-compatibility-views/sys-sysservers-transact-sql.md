---
title: sys.sysservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
author: rothja
ms.author: jroth
ms.openlocfilehash: 03875d828940a2baa5d9f30f7beb58adb77abf07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018111"
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni server accessibile come origine dati OLE DB da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|ID del server remoto (solo per uso locale).|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|Nome del server.|  
|**srvproduct**|**sysname**|Nome del prodotto del server remoto.|  
|**providername**|**nvarchar(128)**|Nome del provider OLE DB per l'accesso al server.|  
|**datasource**|**nvarchar(4000)**|Valore dell'origine dei dati OLE DB.|  
|**Posizione**|**nvarchar(4000)**|Valore della posizione di OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valore stringa del provider OLE DB.|  
|**schemadate**|**datetime**|Data dell'ultimo aggiornamento della riga.|  
|**topologyx**|**int**|Non usato.|  
|**topologyy**|**int**|Non usato.|  
|**catalog**|**sysname**|Catalogo utilizzato quando viene stabilita una connessione a un provider OLE DB.|  
|**srvcollation**|**sysname**|Regole di confronto del server.|  
|**connecttimeout**|**int**|Impostazione del timeout per la connessione al server.|  
|**querytimeout**|**int**|Impostazione del timeout per le query eseguite sul server.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = Server remoto.<br /><br /> 0 = Server collegato.|  
|**rpc**|**bit**|1 = **sp_serveroption@rpc** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@rpc** impostata su **false** oppure **off**.|  
|**pub**|**bit**|1 = **sp_serveroption@pub** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@pub** impostata su **false** oppure **off**.|  
|**sub**|**bit**|1 = **sp_serveroption@sub** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@sub** impostata su **false** oppure **off**.|  
|**dist**|**bit**|1 = **sp_serveroption@dist** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@dist** impostata su **false** oppure **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption@dpub** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@dpub** impostata su **false** oppure **off**.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc out** impostata su **true** oppure **su**.<br /><br /> 0 =  **sp_serveroption@rpc out** impostata su **false** oppure **off**.|  
|**DataAccess**|**bit**|1 =  **sp_serveroption@data access** impostata su **true** oppure **su**.<br /><br /> 0 =  **sp_serveroption@data access** impostata su **false** oppure **off**.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation compatibili** impostata su **true** oppure **su**.<br /><br /> 0 =  **sp_serveroption@collation compatibili** impostata su **false** oppure **off**.|  
|**system**|**bit**|1 = **sp_serveroption@system** impostata su **true** oppure **su**.<br /><br /> 0 = **sp_serveroption@system** impostata su **false** oppure **off**.|  
|**UseRemoteCollation**|**bit**|1 =  **sp_serveroption@remote regole di confronto** impostata su **true** oppure **su**.<br /><br /> 0 =  **sp_serveroption@remote regole di confronto** impostata su **false** oppure **off**.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy convalida dello schema** impostata su **true** oppure **su**.<br /><br /> 0 =  **sp_serveroption@lazy convalida dello schema** impostata su **false** oppure **off**.|  
|**regole di confronto**|**sysname**|Regole di confronto del server come impostato da  **sp_serveroption@collation nome**.|  
|**nonsqlsub**|bit|0 = il server è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = il server non è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

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
ms.openlocfilehash: 333be9cb6c86c1db3801ac50159610c6d19d1611
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941105"
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
|**percorso**|**nvarchar(4000)**|Valore della posizione di OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valore stringa del provider OLE DB.|  
|**schemadate**|**datetime**|Data dell'ultimo aggiornamento della riga.|  
|**topologyx**|**int**|Non usato.|  
|**topologyy**|**int**|Non usato.|  
|**catalog**|**sysname**|Catalogo utilizzato quando viene stabilita una connessione a un provider OLE DB.|  
|**srvcollation**|**sysname**|Regole di confronto del server.|  
|**connecttimeout**|**int**|Impostazione del timeout per la connessione al server.|  
|**querytimeout**|**int**|Impostazione del timeout per le query eseguite sul server.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**IsRemote**|**bit**|1 = Server remoto.<br /><br /> 0 = Server collegato.|  
|**rpc**|**bit**|1 = **sp_serveroption\@RPC** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@RPC** è impostata su **false** o **off**.|  
|**pub**|**bit**|1 = **sp_serveroption\@pub** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@pub** è impostata su **false** o **off**.|  
|**sub**|**bit**|1 = **sp_serveroption\@Sub** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@Sub** è impostata su **false** o **off**.|  
|**dist**|**bit**|1 = **sp_serveroption\@dist** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@dist** è impostata su **false** o **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption\@dpub** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@dpub** è impostata su **false** o **off**.|  
|**rpcout**|**bit**|1 = **sp_serveroption\@RPC out** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@RPC out** è impostata su **false** o **off**.|  
|**DataAccess**|**bit**|1 = **sp_serveroption\@Data Access** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@Data Access** è impostata su **false** o **off**.|  
|**CollationCompatible**|**bit**|1 = **sp_serveroption\@collation compatible** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@collation compatible** è impostata su **false** o **off**.|  
|**system**|**bit**|1 = **sp_serveroption\@System** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@System** è impostata su **false** o **off**.|  
|**UseRemoteCollation**|**bit**|1 = **sp_serveroption\@remote collation** è impostata su **true** o **on**.<br /><br /> 0 = **sp_serveroption\@remote collation** è impostata su **false** o **off**.|  
|**lazyschemavalidation**|**bit**|1 = **la\@convalida dello schema lazy di sp_serveroption** è impostata su **true** o **on**.<br /><br /> 0 = **la\@convalida dello schema lazy di sp_serveroption** è impostata su **false** o **off**.|  
|**confronto**|**sysname**|Regole di confronto del server impostate **dal\@nome delle regole di confronto di sp_serveroption**.|  
|**nonsqlsub**|bit|0 = il server è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = il server non è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a &#40;viste di sistema Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

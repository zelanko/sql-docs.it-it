---
title: sys. dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 052402d3a394e8da3e08828992127d3cd89b95ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900170"
---
# <a name="sysdm_os_host_info-transact-sql"></a>sys. dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Restituisce una riga in cui sono visualizzate le informazioni sulla versione del sistema operativo.  
  
|Nome colonna |Tipo di dati |Descrizione |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |Tipo di sistema operativo: Windows o Linux |
|**host_distribution** |**nvarchar(256)** |Descrizione del sistema operativo. |
|**host_release**|**nvarchar(256)**|Versione del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (numero di versione). Per un elenco di valori e descrizioni, vedere [versione del sistema operativo (Windows)](/windows/desktop/SysInfo/operating-system-version). <br> Per Linux, restituisce una stringa vuota. |  
|**host_service_pack_level**|**nvarchar(256)**|Livello Service Pack del sistema operativo Windows <br> Per Linux, restituisce una stringa vuota. |  
|**host_sku**|**int**|ID Windows del codice di riferimento del prodotto (SKU). Per un elenco di ID SKU e descrizioni, vedere [funzione GetProductInfo](https://msdn.microsoft.com/library/ms724358.aspx). Ammette i valori Null. <br> Per Linux, restituisce NULL. |  
|**os_language_version**|**int**|Identificatore delle impostazioni locali (LCID) Windows del sistema operativo. Per un elenco di valori e descrizioni LCID, vedere [ID delle impostazioni locali assegnati da Microsoft](https://go.microsoft.com/fwlink/?LinkId=208080). Non può essere null.|  

## <a name="remarks"></a>Osservazioni  
Questa visualizzazione è simile a [sys. dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), aggiungendo colonne per distinguere Windows e Linux.
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
Per `SELECT` impostazione predefinita `sys.dm_os_host_info` , l'autorizzazione per `public` è concessa al ruolo. Se revocato, `VIEW SERVER STATE` richiede l'autorizzazione per il server.   
 
> [!CAUTION]
>  A partire dalla [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] versione CTP 1,3 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] , la versione `SELECT` 17 richiede `sys.dm_os_host_info` l'autorizzazione per la connessione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]a. Se `SELECT` l'autorizzazione viene revocata da `public`, solo gli `VIEW SERVER STATE` account di accesso con autorizzazione possono connettersi con la versione più recente di SSMS. Altri strumenti, ad esempio, `sqlcmd.exe` possono connettersi senza `SELECT` autorizzazione `sys.dm_os_host_info`.

  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite tutte le colonne della vista **sys. dm_os_host_info** .  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Ecco un set di risultati di esempio per Windows:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Ecco un set di risultati di esempio in Linux:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>Vedi anche  
 [sys. dm_os_sys_info &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 


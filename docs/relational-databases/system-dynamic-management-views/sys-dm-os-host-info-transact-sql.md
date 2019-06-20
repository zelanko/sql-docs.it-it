---
title: sys.dm_os_host_info (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32ef1fff3b5309da587aacc2fca14099e6bf2cac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047229"
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Restituisce una riga che visualizza le informazioni sulla versione del sistema operativo.  
  
|Nome colonna |Tipo di dati |Descrizione |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |Il tipo del sistema operativo: Windows o Linux |
|**host_distribution** |**nvarchar(256)** |Descrizione del sistema operativo. |
|**host_release**|**nvarchar(256)**|Versione del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (numero di versione). Per un elenco di valori e descrizioni, vedere [versione del sistema operativo (Windows)](/windows/desktop/SysInfo/operating-system-version). <br> Per Linux, restituisce una stringa vuota. |  
|**host_service_pack_level**|**nvarchar(256)**|Livello Service Pack del sistema operativo Windows <br> Per Linux, restituisce una stringa vuota. |  
|**host_sku**|**int**|ID Windows del codice di riferimento del prodotto (SKU). Per un elenco degli ID SKU e descrizioni, vedere [funzione GetProductInfo](https://msdn.microsoft.com/library/ms724358.aspx). Ammette i valori Null. <br> Per Linux, viene restituito NULL. |  
|**os_language_version**|**int**|Identificatore delle impostazioni locali (LCID) Windows del sistema operativo. Per un elenco dei valori LCID e delle descrizioni, vedere [Locale IDs Assigned by Microsoft](https://go.microsoft.com/fwlink/?LinkId=208080). Non può essere null.|  

## <a name="remarks"></a>Note  
Questa visualizzazione è simile a [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), aggiunta di colonne per differenziare Windows e Linux.
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
Il `SELECT` autorizzazione `sys.dm_os_host_info` viene concesso al `public` ruolo per impostazione predefinita. Se è stato revocato, è necessario `VIEW SERVER STATE` autorizzazione nel server.   
 
> [!CAUTION]
>  Partire dalla versione [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] richiede la versione 17 `SELECT` autorizzazione `sys.dm_os_host_info` per connettersi a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Se `SELECT` autorizzazione viene revocata `public`, solo gli account di accesso con `VIEW SERVER STATE` autorizzazione può connettersi con la versione più recente di SSMS. (Altri strumenti, ad esempio `sqlcmd.exe` possono connettersi senza `SELECT` autorizzazione `sys.dm_os_host_info`.)

  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce tutte le colonne dai **DM os_host_info** visualizzazione.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Ecco un esempio set di risultati su Windows:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Ecco un esempio di risultato impostato in Linux:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 


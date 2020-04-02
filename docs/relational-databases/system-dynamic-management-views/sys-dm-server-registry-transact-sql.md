---
title: metodo sys.dm_server_registry (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_registry_TSQL
- sys.dm_server_registry
- dm_server_registry
- sys.dm_server_registry_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_registry dynamic management view
ms.assetid: 9b3e0c74-2e99-4996-a383-104d51831e97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8daa2d195ab1f4cf4602b9633394ed1705a3d7d2
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/01/2020
ms.locfileid: "80530819"
---
# <a name="sysdm_server_registry-transact-sql"></a>sys.dm_server_registry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le informazioni di configurazione e installazione archiviate nel Registro di sistema di Windows per l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Restituisce una riga per ogni chiave del Registro di sistema. Utilizzare la DMV in per restituire informazioni diverse, ad esempio i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili nel computer host o i valori di configurazione della rete per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|Nome della chiave del Registro di sistema Ammette i valori Null.|  
|value_name|**nvarchar(256)**|Nome del valore della chiave. Si tratta dell'elemento visualizzato nella colonna **Nome** dell'Editor del Registro di sistema. Ammette i valori Null.|  
|value_data|**sql_variant**|Valore dei dati della chiave. Questo è il valore visualizzato nella colonna **Dati** dell'Editor del Registro di sistema per una determinata voce. Ammette i valori Null.|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-display-the-sql-server-services"></a>R. Visualizzazione dei servizi SQL Server  
 Nell'esempio seguente vengono restituiti i valori della chiave del Registro di sistema per i servizi SQL Server e SQL Server Agent per l'istanza corrente di SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%ControlSet%';  
```  
  
### <a name="b-display-the-sql-server-agent-registry-key-values"></a>B. Visualizzazione di valori della chiave del Registro di sistema di SQL Server Agent  
 Nell'esempio seguente vengono restituiti i valori della chiave del Registro di sistema di SQL Server Agent per l'istanza corrente di SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SQLAgent%';  
```  
  
### <a name="c-display-the-current-version-of-the-instance-of-sql-server"></a>C. Visualizzazione della versione corrente dell'istanza di SQL Server  
 Nell'esempio seguente viene restituita la versione dell'istanza corrente di SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE value_name = N'CurrentVersion';  
```  
  
### <a name="d-display-the-parameters-passed-to-the-instance-of-sql-server-during-startup"></a>D. Visualizzazione dei parametri passati all'istanza di SQL Server durante l'avvio  
 Nell'esempio seguente vengono restituiti i parametri passati all'istanza di SQL Server durante l'avvio.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%Parameters';  
```  
  
### <a name="e-return-network-configuration-information-for-the-instance-of-sql-server"></a>E. Restituzione delle informazioni di configurazione della rete per l'istanza di SQL Server  
 Nell'esempio seguente vengono restituiti i valori di configurazione della rete per l'istanza corrente di SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SuperSocketNetLib%';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [dm_server_services&#41;Transact-SQLdisql &#40;di sistema](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  

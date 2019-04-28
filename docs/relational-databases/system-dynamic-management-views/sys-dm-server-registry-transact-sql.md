---
title: sys.dm_server_registry (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e4e0b1069977c14216952e537d4bd12b28190529
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62684007"
---
# <a name="sysdmserverregistry-transact-sql"></a>sys.dm_server_registry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le informazioni di configurazione e installazione archiviate nel Registro di sistema di Windows per l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Restituisce una riga per ogni chiave del Registro di sistema. Utilizzare la DMV in per restituire informazioni diverse, ad esempio i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili nel computer host o i valori di configurazione della rete per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|Nome della chiave del Registro di sistema Ammette i valori Null.|  
|value_name|**nvarchar(256)**|Nome del valore della chiave. Si tratta dell'elemento visualizzato nei **nome** colonna dell'Editor del Registro di sistema. Ammette i valori Null.|  
|value_data|**sql_variant**|Valore dei dati della chiave. Si tratta del valore visualizzato nei **dati** colonna dell'Editor del Registro di sistema per una voce specificata. Ammette i valori Null.|  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-display-the-sql-server-services"></a>A. Visualizzazione dei servizi SQL Server  
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
WHERE registry_key = N'CurrentVersion';  
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
 [sys.dm_server_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  

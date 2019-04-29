---
title: sp_syscollector_set_cache_directory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 300a59bb09fa28a626b117f51cfa6509b5ca883e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004280"
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Specifica la directory in cui vengono archiviati i dati raccolti prima di essere caricati nel data warehouse di gestione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @cache_directory = ] 'cache_directory'` La directory del file System in cui i dati raccolti vengono archiviati temporaneamente. *cache_directory* viene **nvarchar(255**, con un valore predefinito NULL. Se non viene specificato alcun valore, viene utilizzata la directory temporanea predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario disabilitare l'agente di raccolta dati prima di modificare la configurazione della directory della cache. La stored procedure ha esito negativo se l'agente di raccolta dati è abilitato. Per altre informazioni, vedere [Abilita o disabilita raccolta dati](../../relational-databases/data-collection/enable-or-disable-data-collection.md), e [gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md).  
  
 Nel momento in cui sp_syscollector_set_cache_directory viene eseguita la directory specificata non deve essere esistere. I dati tuttavia non possono essere memorizzati nella cache né caricati in modo corretto fino a quando la directory non viene creata. È consigliabile pertanto creare la directory prima di eseguire questa stored procedure.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente disabilita l'agente di raccolta dati, imposta la directory della cache per l'agente di raccolta `D:\tempdata`e quindi Abilita l'agente di raccolta dati.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  

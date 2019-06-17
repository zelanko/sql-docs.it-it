---
title: sp_syscollector_set_cache_window (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd261178b852e8e890dd654893ce8fc167a15915
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004298"
---
# <a name="spsyscollectorsetcachewindow-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta il numero di nuovi tentativi di caricamento dei dati in caso di esito negativo. Se si ritenta il caricamento in caso di esito negativo, è possibile ridurre il rischio di perdita dei dati raccolti.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>Argomenti  
 [ @cache_window = ] *cache_window*  
 Numero di volte in cui viene eseguito un tentativo di caricamento dati nel data warehouse di gestione in caso di errore, senza perdita dei dati. *cache_window* viene **int** con valore predefinito è 1. *cache_window* può avere uno dei valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|-1|Vengono memorizzati nella cache tutti i dati di caricamento dei precedenti tentativi di caricamento non riusciti.|  
|0|Non vengono memorizzati nella cache dati dei tentativi di caricamento non riusciti.|  
|*n*|Memorizzare nella cache i dati di n errori di caricamento precedenti, dove *n* > = 1.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 È necessario disabilitare l'agente di raccolta dati prima di modificare la configurazione della finestra della cache. La stored procedure ha esito negativo se l'agente di raccolta dati è abilitato. Per altre informazioni, vedere [Abilita o disabilita raccolta dati](../../relational-databases/data-collection/enable-or-disable-data-collection.md), e [gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md).  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene disabilitato l'agente di raccolta dati, viene configurata la finestra della cache per conservare i dati per un massimo di tre tentativi di caricamento non riusciti, quindi viene riabilitato l'agente di raccolta dati.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  

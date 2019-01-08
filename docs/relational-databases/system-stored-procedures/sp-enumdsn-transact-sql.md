---
title: sp_enumdsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f58a16b3d4d393a94dc5e42413ddfeb2a8eb5d9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773893"
---
# <a name="spenumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di tutti i nomi di origini dei dati ODBC e OLE DB definiti per un server in esecuzione con un account utente specifico di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Nome dell'origine dati**|**sysname**|Nome dell'origine dei dati.|  
|**Descrizione**|**varchar(255)**|Descrizione dell'origine dei dati.|  
|**Tipo**|**int**|Tipo di origine dei dati:<br /><br /> **1** = DSN ODBC<br /><br /> **3** = origine dei dati OLE DB|  
|**Nome del provider**|**varchar(255)**|Nome del provider OLE DB. Il valore è NULL per DSN ODBC.|  
  
## <a name="remarks"></a>Note  
 Ogni [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio dispone di un contesto utente. ovvero un set di voci del Registro di sistema che include le definizioni delle origini dei dati ODBC disponibili per l'utente. Il contesto utente dipende dal nome utente utilizzato per l'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ad esempio, se il server è in esecuzione nel contesto utente dell'account di sistema, i DSN restituiti sono tutti DSN di sistema associati all'account di sistema. Se invece il server viene eseguito con un account utente privato, vengono restituiti solo i DSN definiti per tale account privato di tale utente.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_enumdsn**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: sp_helpdatatypemap (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf42231158f646e34c63bd148ba66c9780b14785
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529593"
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui mapping dei tipi di dati definiti tra [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database (DBMS) i sistemi di gestione. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @source_dbms = ] 'source_dbms'` È il nome del DBMS da cui vengono eseguito il mapping di tipi di dati. *source_dbms* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**MSSQLSERVER**|L'origine è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|L'origine è un database Oracle.|  
  
`[ @source_version = ] 'source_version'` È la versione del prodotto del sistema DBMS di origine. *source_version*viene **varchar (10)**, e se non specificato, il tipo di dati i mapping per tutte le versioni dell'origine di DBMS vengono restituiti. Consente al set dei risultati di venire filtrato in base alla versione di origine del sistema DBMS.  
  
`[ @source_type = ] 'source_type'` È il tipo di dati elencato nel sistema DBMS di origine. *source_type* viene **sysname**, se non specificato, vengono restituiti i mapping per tutti i tipi di dati nel DBMS di origine. Consente al set di risultati di venire filtrato in base al tipo di dati nel sistema DBMS di origine.  
  
`[ @destination_dbms = ] 'destination_dbms'` È il nome del sistema DBMS di destinazione. *destination_dbms* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**MSSQLSERVER**|La destinazione è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|La destinazione è un database Oracle.|  
|**DB2**|La destinazione è un database IBM DB2.|  
|**SYBASE**|La destinazione è un database Sybase.|  
  
`[ @destination_version = ] 'destination_version'` È la versione del prodotto del sistema DBMS di destinazione. *destination_version*viene **varchar (10)**, se non specificato, vengono restituiti i mapping per tutte le versioni del sistema DBMS di destinazione. Consente al set dei risultati di venire filtrato in base alla versione di destinazione del sistema DBMS.  
  
`[ @destination_type = ] 'destination_type'` È il tipo di dati elencato nel sistema DBMS di destinazione. *destination_type*viene **sysname**, se non specificato, vengono restituiti i mapping per tutti i tipi di dati nel DBMS di destinazione. Consente al set di risultati di venire filtrato in base al tipo di dati nel sistema DBMS di destinazione.  
  
`[ @defaults_only = ] defaults_only` È il mapping dei tipi di dati predefiniti vengono restituiti solo. *defaults_only* viene **bit**, il valore predefinito è **0**. **1** indica che solo i dati predefiniti i mapping dei tipi vengono restituiti. **0** indica che il valore predefinito e qualsiasi dato definito dall'utente mapping dei tipi vengono restituiti.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**mapping_id**|Identifica il mapping dei tipi di dati.|  
|**source_dbms**|Nome e numero di versione del sistema DBMS di origine.|  
|**source_type**|Tipo di dati nel sistema DBMS di origine.|  
|**destination_dbms**|Nome del sistema DBMS di destinazione.|  
|**destination_type**|Tipo di dati nel sistema DBMS di destinazione.|  
|**is_default**|Indica il mapping predefinito o un mapping alternativo. Un valore pari **0** indica che questo mapping è definito dall'utente.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpdatatypemap** definisce i mapping dei tipi di dati dal Server di pubblicazione non SQL e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agli editori di non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
 Se non è supportata la combinazione specificata di origine e destinazione DBMS **sp_helpdatatypemap** restituisce un set di risultati vuoto.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di distribuzione membri del ruolo predefinito del server di **db_owner** ruolo predefinito del database nel database di distribuzione possono eseguire **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  

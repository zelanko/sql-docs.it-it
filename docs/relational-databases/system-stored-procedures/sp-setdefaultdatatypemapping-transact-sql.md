---
title: sp_setdefaultdatatypemapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c229fe6355e4fe463038dd7ef44d89217b0de77
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202230"
---
# <a name="spsetdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contrassegna un mapping esistente di tipo dati fra [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestione sistema di database (DBMS come impostazione predefinita). Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@mapping_id=** ] *mapping_id*  
 Identifica un mapping esistente di tipi di dati.  *mapping_id* viene **int**, con valore predefinito è NULL. Se si specifica *mapping_id*, quindi non sono necessari i parametri rimanenti.  
  
 [ **@source_dbms**=] **'***source_dbms***'**  
 Nome del DBMS da cui viene eseguito il mapping dei tipi di dati. *source_dbms* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**MSSQLSERVER**|L'origine è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|L'origine è un database Oracle.|  
|NULL (predefinito)||  
  
 È necessario specificare questo parametro se *mapping_id* è NULL.  
  
 [  **@source_version=** ] **'***source_version***'**  
 Numero di versione del DBMS di origine. *source_version* viene **varchar (10)**, con un valore predefinito NULL.  
  
 [ **@source_type**=] **'***source_type***'**  
 Tipo di dati nel sistema DBMS di origine. *source_type* viene **sysname**. È necessario specificare questo parametro se *mapping_id* è NULL.  
  
 [  **@source_length_min=** ] *source_length_min*  
 Lunghezza minima del tipo di dati nel DBMS di origine. *source_length_min* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@source_length_max=** ] *source_length_max*  
 Lunghezza massima del tipo di dati nel DBMS di origine. *source_length_max* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@source_precision_min=** ] *source_precision_min*  
 Precisione minima del tipo di dati nel DBMS di origine. *source_precision_min* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@source_precision_max=** ] *source_precision_max*  
 Precisione massima del tipo di dati nel DBMS di origine. *source_precision_max* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@source_scale_min=** ] *source_scale_min*  
 Scala minima del tipo di dati nel DBMS di origine. *source_scale_min* viene **int**, con un valore predefinito NULL.  
  
 [  **@source_scale_max=** ] *source_scale_max*  
 Scala massima del tipo di dati nel DBMS di origine. *source_scale_max* viene **int**, con un valore predefinito NULL.  
  
 [  **@source_nullable=** ] *source_nullable*  
 Specifica se il tipo dati nel DBMS di origine ammette valori NULL. *source_nullable* viene **bit**, con un valore predefinito NULL. **1** indica che i valori NULL sono supportati.  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 Nome del sistema DBMS di destinazione. *destination_dbms* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**MSSQLSERVER**|La destinazione è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|La destinazione è un database Oracle.|  
|**DB2**|La destinazione è un database IBM DB2.|  
|**SYBASE**|La destinazione è un database Sybase.|  
|NULL (predefinito)||  
  
 [ **@destination_version**=] **'***destination_version***'**  
 Numero di versione del DBMS di destinazione. *destination_version* viene **varchar (10)**, con un valore predefinito NULL.  
  
 [ **@destination_type**=] **'***destination_type***'**  
 Tipo di dati nel DBMS di destinazione. *destination_type* viene **sysname**, con un valore predefinito NULL.  
  
 [  **@destination_length=** ] *destination_length*  
 Lunghezza del tipo di dati nel DBMS di destinazione. *destination_length* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@destination_precision=** ] *destination_precision*  
 Precisione del tipo di dati nel DBMS di destinazione. *destination_precision* viene **bigint**, con un valore predefinito NULL.  
  
 [  **@destination_scale=** ] *destination_scale*  
 Scala del tipo di dati nel DBMS di destinazione. *destination_scale* viene **int**, con un valore predefinito NULL.  
  
 [  **@destination_nullable=** ] *destination_nullable*  
 Specifica se il tipo di dati nel DBMS di destinazione ammette valori NULL. *destination_nullable* viene **bit**, con un valore predefinito NULL. **1** indica che i valori NULL sono supportati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_setdefaultdatatypemapping** viene utilizzata in tutti i tipi di replica tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS.  
  
 I mapping dei tipi di dati predefiniti vengono applicati a tutte le topologie di replica che includono il sistema DBMS specificato.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_setdefaultdatatypemapping**.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare i mapping dei tipi di dati per un server di pubblicazione Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  

---
title: sp_dsninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2836db0eef25c21861ec7b2d766f1195d250f20
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817733"
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sull'origine dati ODBC o OLE DB provenienti dal server di distribuzione associato al server corrente. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@dsn =**] **'***dsn***'**  
 Nome del server collegato DSN ODBC o OLE DB. *DSN* viene **varchar(128)**, non prevede alcun valore predefinito.  
  
 [  **@infotype =**] **'***Info***'**  
 Tipo di informazioni che si desidera ottenere. Se *Info* viene omesso o se viene specificato NULL, vengono restituiti tutti i tipi di informazioni. *Info* viene **varchar(128)**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**DBMS_NAME**|Specifica il nome del produttore dell'origine dati.|  
|**DBMS_VERSION**|Specifica la versione dell'origine dati.|  
|**DATABASE_NAME**|Specifica il nome del database.|  
|**SQL_SUBSCRIBER**|Specifica che l'origine dati può essere un Sottoscrittore.|  
  
 [  **@login =**] **'***account di accesso***'**  
 Account di accesso per l'origine dati. Se l'origine dati include un account di accesso, specificare NULL oppure omettere il parametro. *account di accesso*viene **varchar(128)**, con un valore predefinito è NULL.  
  
 [  **@password =**] **'***password***'**  
 Password per l'account di accesso. Se l'origine dati include un account di accesso, specificare NULL oppure omettere il parametro. *la password*viene **varchar(128)**, con un valore predefinito è NULL.  
  
 [  **@dso_type=**] *dso_type*  
 Tipo dell'origine dati. *dso_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Origine dati ODBC|  
|**3**|Origine dati OLE DB|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Tipo di informazioni**|**nvarchar(64)**|Tipi di informazioni quali DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER|  
|**Valore**|**nvarchar(512)**|Valore del tipo di informazioni associato.|  
  
## <a name="remarks"></a>Note  
 **sp_dsninfo** viene utilizzata in tutti i tipi di replica.  
  
 **sp_dsninfo** recupera informazioni origine dati ODBC o OLE DB che mostra se il database può essere utilizzato per la replica o l'esecuzione di query.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_dsninfo**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_enumdsn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

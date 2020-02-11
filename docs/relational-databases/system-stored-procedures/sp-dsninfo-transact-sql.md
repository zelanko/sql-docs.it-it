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
ms.openlocfilehash: cb67524304807eba6765387590fd53a52b92f19a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124711"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sull'origine dati ODBC o OLE DB provenienti dal server di distribuzione associato al server corrente. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @dsn = ] 'dsn'`Nome del DSN ODBC o del server OLE DB collegato. *DSN* è di tipo **varchar (128)** e non prevede alcun valore predefinito.  
  
`[ @infotype = ] 'info_type'`Tipo di informazioni da restituire. Se *info_type* non viene specificato o se viene specificato null, vengono restituiti tutti i tipi di informazioni. *info_type* è di tipo **varchar (128)** e il valore predefinito è null. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**DBMS_NAME**|Specifica il nome del produttore dell'origine dati.|  
|**DBMS_VERSION**|Specifica la versione dell'origine dati.|  
|**DATABASE_NAME**|Specifica il nome del database.|  
|**SQL_SUBSCRIBER**|Specifica che l'origine dati può essere un Sottoscrittore.|  
  
`[ @login = ] 'login'`Account di accesso per l'origine dati. Se l'origine dati include un account di accesso, specificare NULL oppure omettere il parametro. *login*è di tipo **varchar (128)** e il valore predefinito è null.  
  
`[ @password = ] 'password'`Password per l'account di accesso. Se l'origine dati include un account di accesso, specificare NULL oppure omettere il parametro. *password*è di tipo **varchar (128)** e il valore predefinito è null.  
  
`[ @dso_type = ] dso_type`Tipo di origine dati. *dso_type* è di **tipo int**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Origine dati ODBC|  
|**3**|Origine dati OLE DB|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Information Type**|**nvarchar (64)**|Tipi di informazioni quali DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER|  
|**Valore**|**nvarchar(512)**|Valore del tipo di informazioni associato.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dsninfo** viene utilizzato in tutti i tipi di replica.  
  
 **sp_dsninfo** recupera le informazioni sull'origine dati ODBC o OLE DB che indicano se il database può essere utilizzato per la replica o l'esecuzione di query.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_dsninfo**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_enumdsn &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

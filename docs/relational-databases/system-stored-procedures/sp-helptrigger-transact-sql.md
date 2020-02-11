---
title: sp_helptrigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1e6244443fc1f6ba7d83376226fedd56563e0d39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048226"
---
# <a name="sp_helptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Viene restituito il tipo o i tipi di trigger DML definiti nella tabella specificata per il database corrente. non è possibile usare sp_helptrigger con i trigger DDL. In alternativa, eseguire una query sulla vista del catalogo delle [stored procedure di sistema](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @tabname = ] 'table'`Nome della tabella del database corrente per cui si desidera ottenere informazioni sul trigger. *Table* è di **tipo nvarchar (776)** e non prevede alcun valore predefinito.  
  
`[ @triggertype = ] 'type'`Tipo di trigger DML per cui restituire informazioni. il *tipo* è **char (6)** e il valore predefinito è null. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**DELETE**|Restituisce informazioni sui trigger DELETE.|  
|**INSERT**|Restituisce informazioni sui trigger INSERT.|  
|**UPDATE**|Restituisce informazioni sui trigger UPDATE.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
 Nella tabella seguente vengono descritte le informazioni contenute nel set di risultati.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|Nome del trigger.|  
|**trigger_owner**|**sysname**|Nome del proprietario della tabella in cui il trigger è definito.|  
|**aggiornamento di**|**int**|1 = Trigger UPDATE<br /><br /> 0 = Trigger diverso da UPDATE|  
|**IsDelete**|**int**|1 = Trigger DELETE<br /><br /> 0 = Trigger diverso da DELETE|  
|**isinsert**|**int**|1 = Trigger INSERT<br /><br /> 0 = Trigger diverso da INSERT|  
|**isafter**|**int**|1 = Trigger AFTER<br /><br /> 0 = Trigger diverso da AFTER|  
|**isinsteadof**|**int**|1 = Trigger INSTEAD OF<br /><br /> 0 = Trigger diverso da INSTEAD OF|  
|**trigger_schema**|**sysname**|Nome dello schema a cui appartiene il trigger.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione di [configurazione della visibilità dei metadati](../../relational-databases/security/metadata-visibility-configuration.md) per la tabella.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguita la stored procedure `sp_helptrigger` per generare informazioni sui trigger definiti nella tabella `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di motore di database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

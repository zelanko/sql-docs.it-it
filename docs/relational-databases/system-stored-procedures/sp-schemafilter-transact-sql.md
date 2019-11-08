---
title: sp_schemafilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 231796d1678a19106eb89f3039cd755e8385082c
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633010"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di visualizzare e modificare le informazioni nello schema che vengono escluse dall'elenco delle tabelle Oracle idonee per la pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` è il nome del server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non [!INCLUDE[msCoName](../../includes/msconame-md.md)]. *Publisher* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @schema = ] 'schema'` è il nome dello schema. *schema* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @operation = ] 'operation'` è l'azione da intraprendere per questo schema. *Operation* è di **tipo nvarchar (4)** . i possibili valori sono i seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**aggiungere**|Aggiunge lo schema specificato all'elenco di schemi non idonei per la pubblicazione.|  
|**goccia**|Elimina lo schema specificato dall'elenco di schemi non idonei per la pubblicazione.|  
|**Guida**|Restituisce l'elenco degli schemi non idonei per la pubblicazione.|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**SchemaName**|**sysname**|Nome dello schema non idoneo per la pubblicazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_schemafilter** deve essere utilizzato solo per i Publisher eterogenei.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** nel server di distribuzione possono eseguire **sp_schemafilter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

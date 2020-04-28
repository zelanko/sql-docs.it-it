---
title: sp_changedistributor_property (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_property_TSQL
- sp_changedistributor_property
helpviewer_keywords:
- sp_changedistributor_property
ms.assetid: 04f503a1-307c-4de0-bac6-e6e97d5b6940
author: stevestein
ms.author: sstein
ms.openlocfilehash: 18921fa57cfa203b0d8e5274caeb1e17c385405c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771297"
---
# <a name="sp_changedistributor_property-transact-sql"></a>sp_changedistributor_property (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Modifica le proprietà del server di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changedistributor_property [ [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @property = ] 'property'`Proprietà di un database di distribuzione specificato. *Property* è di **tipo sysname**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**heartbeat_interval**|Periodo massimo in minuti durante il quale un agente può essere eseguito senza registrare alcun messaggio di stato.|  
|NULL (predefinito)|Vengono stampati tutti i valori delle *Proprietà* disponibili.|  
  
`[ @value = ] 'value'`Valore per la proprietà del server di distribuzione specificata. *value* è di tipo **varchar (255)** e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_changedistributor_property** viene utilizzato in tutti i tipi di replica.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pro_1.sql)]  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_changedistributor_property**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di distribuzione e dell'editore](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_dropdistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

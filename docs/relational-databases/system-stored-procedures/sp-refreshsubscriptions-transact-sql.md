---
title: sp_refreshsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_refreshsubscriptions
- sp_refreshsubscriptions_TSQL
helpviewer_keywords:
- sp_refreshsubscriptions
ms.assetid: 6cb9b1ce-1ce7-43ab-9451-201f79ed1ffa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9de03f10d16e81f97bd155212c8e2dafbd81216b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075766"
---
# <a name="sprefreshsubscriptions-transact-sql"></a>sp_refreshsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiungere le sottoscrizioni a nuovi articoli per tutti i sottoscrittori esistenti a una pubblicazione ad aggiornamento immediato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_refreshsubscriptions [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È la pubblicazione per cui si desidera aggiornare le sottoscrizioni. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **sp_refreshsubscriptions** viene utilizzata nella replica di tipo merge e snapshot, transazionale.  
  
 **sp_refreshsubscriptions** viene chiamato dal **sp_addarticle** per le pubblicazioni ad aggiornamento immediato.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_refreshsubscriptions**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: sp_scriptpublicationcustomprocs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 89cd3991819bdba99d3a4b95c16e7b3247808031
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126383"
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea gli script delle procedure personalizzate INSERT, UPDATE e DELETE per tutti gli articoli di tabella in una pubblicazione in cui è abilitata l'opzione per la generazione automatica dello schema delle procedure personalizzate. **sp_scriptpublicationcustomprocs** è particolarmente utile per la configurazione di sottoscrizioni per cui lo snapshot viene applicato manualmente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication_name'` È il nome della pubblicazione. *publication_name* viene **sysname** non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce un set di risultati è costituito da un unico **nvarchar (4000)** colonna. Il set di risultati forma l'istruzione CREATE PROCEDURE completa utilizzata per creare la stored procedure personalizzata.  
  
## <a name="remarks"></a>Note  
 Lo script delle procedure personalizzate non viene creato per gli articoli senza l'opzione per la generazione automatica dello schema delle procedure personalizzate (0x2).  
  
 Le procedure seguenti vengono utilizzate da **sp_scriptpublicationcustomprocs** per creare procedure nel sottoscrittore e non deve essere eseguito direttamente:  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Permissions  
 Eseguire l'autorizzazione viene concessa per **pubbliche**; un controllo della sicurezza procedurale viene eseguito all'interno di questa stored procedure per limitare l'accesso ai membri del **sysadmin** ruolo predefinito del server e **DB _ proprietario** ruolo predefinito del database nel database corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

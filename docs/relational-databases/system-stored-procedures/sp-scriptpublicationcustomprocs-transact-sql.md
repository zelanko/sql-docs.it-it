---
description: sp_scriptpublicationcustomprocs (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae7c24167b06f659006d44f469c92383adc96d21
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538601"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Crea gli script delle procedure personalizzate INSERT, UPDATE e DELETE per tutti gli articoli di tabella in una pubblicazione in cui è abilitata l'opzione per la generazione automatica dello schema delle procedure personalizzate. **sp_scriptpublicationcustomprocs** è particolarmente utile per la configurazione di sottoscrizioni per le quali lo snapshot viene applicato manualmente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication_name'` Nome della pubblicazione. *publication_name* è di **tipo sysname** e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce un set di risultati costituito da una singola colonna **nvarchar (4000)** . Il set di risultati forma l'istruzione CREATE PROCEDURE completa utilizzata per creare la stored procedure personalizzata.  
  
## <a name="remarks"></a>Osservazioni  
 Lo script delle procedure personalizzate non viene creato per gli articoli senza l'opzione per la generazione automatica dello schema delle procedure personalizzate (0x2).  
  
 Le procedure riportate di seguito vengono utilizzate da **sp_scriptpublicationcustomprocs** per creare procedure per il Sottoscrittore e non devono essere eseguite direttamente:  
  
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
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione Execute è concessa a **public**; all'interno di questa stored procedure viene eseguito un controllo di sicurezza procedurale per limitare l'accesso ai membri del ruolo predefinito del server **sysadmin** e **db_owner** ruolo predefinito del database nel database corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

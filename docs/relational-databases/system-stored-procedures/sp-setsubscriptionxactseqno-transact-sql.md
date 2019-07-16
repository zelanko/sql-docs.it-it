---
title: sp_setsubscriptionxactseqno (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27a7f35a915e2bff62932124aef64984a63cbd0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021079"
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usato durante la risoluzione dei problemi per specificare l'ultima transazione recapitata utilizzando il numero di sequenza del log (LSN), consentendo all'agente di distribuzione avviare l'esecuzione della transazione successiva. Al riavvio, l'agente di distribuzione restituisce le transazioni superiore a questo limite (LSN) dalla cache del database di distribuzione (msrepl_commands). Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore. e non è supportata per Sottoscrittori non SQL Server.  
  
> [!CAUTION]  
>  Se si utilizza questa stored procedure in modo non corretto oppure si specifica un valore LSN non corretto, è possibile che l'agente di distribuzione annulli modifiche già applicate nel Sottoscrittore oppure ignori tutte le restanti modifiche.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del database di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito. Per un Server di pubblicazione non SQL, *publisher_db* è il nome del database di distribuzione.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito. Quando l'agente di distribuzione è condiviso da più di una pubblicazione, è necessario specificare un valore all per *publication*.  
  
`[ @xact_seqno = ] xact_seqno` È il valore LSN della successiva transazione nel server di distribuzione da applicare nel Sottoscrittore. *xact_seqno* viene **varbinary(16)** , non prevede alcun valore predefinito.  
  
## <a name="result-set"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|LSN originale della successiva transazione da applicare nel Sottoscrittore.|  
|**XACT_SEQNO AGGIORNATO**|**varbinary(16)**|LSN aggiornato della successiva transazione da applicare nel Sottoscrittore.|  
|**NUMERO DI FLUSSO DELLA SOTTOSCRIZIONE**|**int**|Numero di flussi di sottoscrizione utilizzati durante l'ultima sincronizzazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_setsubscriptionxactseqno** viene utilizzata nella replica transazionale.  
  
 **sp_setsubscriptionxactseqno** non può essere utilizzata in una topologia di replica transazionale peer-to-peer.  
  
 **sp_setsubscriptionxactseqno** può essere utilizzato per ignorare una transazione specifica che ha causato un errore quando viene applicato nel Sottoscrittore. Quando si verifica un errore e quando si arresta l'agente di distribuzione, chiamare [sp_helpsubscriptionerrors &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) nel server di distribuzione per recuperare il valore xact_seqno della transazione non riuscita e quindi chiamare **sp_setsubscriptionxactseqno**, passando questo valore per *xact_seqno*. In questo modo verranno elaborati solo i comandi successivi a questo LSN.  
  
 Specificare il valore **0** per *xact_seqno* a recapitare tutti i comandi in sospeso nel database di distribuzione al sottoscrittore.  
  
 **sp_setsubscriptionxactseqno** potrebbe non riuscire se l'agente di distribuzione utilizza più flussi di sottoscrizione.  
  
 Quando si verifica questo errore, è necessario eseguire l'agente di distribuzione con un flusso di sottoscrizione singolo. Per altre informazioni, vedere [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_setsubscriptionxactseqno**.  
  
## <a name="see-more"></a>Altre informazioni

[Blog: Come ignorare una transazione](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  

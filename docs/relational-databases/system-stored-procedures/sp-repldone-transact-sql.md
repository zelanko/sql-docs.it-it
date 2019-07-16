---
title: sp_repldone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5ed4502b7f3e737b8e3adbfae852c2a513e2ccd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006889"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna il record che identifica l'ultima transazione distribuita del server. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!CAUTION]  
>  Se si esegue **sp_repldone** manualmente, si potrebbero invalidare l'ordine e la consistenza delle transazioni recapitate. **sp_repldone** deve essere utilizzato solo per la risoluzione dei problemi di replica come indicato da un professionista del supporto tecnico esperto della replica.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @xactid = ] xactid` È il numero di sequenza del log (LSN) del primo record relativo all'ultima transazione distribuita del server. *xactid* viene **binary(10)** , non prevede alcun valore predefinito.  
  
`[ @xact_seqno = ] xact_seqno` È il numero LSN dell'ultimo record per l'ultima transazione distribuita del server. *xact_seqno* viene **binary(10)** , non prevede alcun valore predefinito.  
  
`[ @numtrans = ] numtrans` È il numero di transazioni distribuite. *numtrans* viene **int**, non prevede alcun valore predefinito.  
  
`[ @time = ] time` È il numero di millisecondi, se specificato, necessario per distribuire l'ultimo batch di transazioni. *tempo* viene **int**, non prevede alcun valore predefinito.  
  
`[ @reset = ] reset` È lo stato di reimpostazione. *reimpostare* viene **int**, non prevede alcun valore predefinito. Se **1**, replicate tutte le transazioni nel log vengono contrassegnate come distribuite. Se **0**, il log delle transazioni viene reimpostato sulla prima transazione replicata e Nessuna transazione replicata viene contrassegnata come distribuita. *reimpostare* è valido solo quando entrambe *xactid* e *xact_seqno* sono NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_repldone** viene utilizzata nella replica transazionale.  
  
 **sp_repldone** usata dal processo di lettura log per rilevare le transazioni distribuite.  
  
 Con **sp_repldone**, è possibile informare manualmente il server che una transazione è stata replicata (inviata ai server di distribuzione). È inoltre possibile cambiare la transazione contrassegnata come transazione successiva in attesa di replica e scorrere l'elenco delle transazioni replicate. Tutte le transazioni che precedono la transazione specificata, inclusa tale transazione, vengono contrassegnate come distribuite.  
  
 I parametri obbligatori *xactid* e *xact_seqno* possono essere ottenuti utilizzando **sp_repltrans** oppure **sp_replcmds**.  
  
## <a name="permissions"></a>Permissions  
 I membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_repldone**.  
  
## <a name="examples"></a>Esempi  
 Quando *xactid* è NULL, *xact_seqno* è NULL, e *reimpostare* è **1**, tutto replicate nel log delle transazioni contrassegnate come distribuite. Ciò risulta utile quando nel log delle transazioni sono presenti transazioni replicate non più valide e si desidera troncare il log, ad esempio:  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  È possibile utilizzare questa procedura in situazioni di emergenza per consentire il troncamento del log delle transazioni quando sono presenti transazioni in sospeso in attesa di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

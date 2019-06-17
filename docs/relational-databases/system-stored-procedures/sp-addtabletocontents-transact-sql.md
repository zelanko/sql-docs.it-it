---
title: sp_addtabletocontents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 991ee7139ae4a323a1d426d1882e4f6b3a4df871
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049724"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inserisce riferimenti nelle tabelle di rilevamento per le operazioni di merge per tutte le righe di una tabella di origine non incluse nelle tabelle di rilevamento. Usare questa opzione se si hanno il caricamento bulk una grande quantità di dati mediante **bcp**, cui non vengono attivati i trigger di rilevamento di merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @table_name = ] 'table_name'` È il nome della tabella. *TABLE_NAME* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @owner_name = ] 'owner_name'` È il nome del proprietario della tabella. *owner_name* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @filter_clause = ] 'filter_clause'` Specifica una clausola di filtro che controlla quali righe di dati appena caricati devono essere aggiunte per l'unione di tabelle di rilevamento. *filter_clause* viene **nvarchar (4000)** , con un valore predefinito NULL. Se *filter_clause* viene **null**, tutte le operazioni bulk vengono aggiunte le righe caricate.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addtabletocontents** viene utilizzato solo nella replica di tipo merge.  
  
 Le righe nel *nome_tabella* fa riferimento il loro **rowguidcol** e i riferimenti vengono aggiunti per l'unione di tabelle di rilevamento. **sp_addtabletocontents** deve essere usato dopo la copia bulk dei dati in una tabella pubblicata tramite una replica di tipo merge. La stored procedure inizia il rilevamento delle righe copiate e include le nuove righe nella sincronizzazione successiva.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addtabletocontents**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

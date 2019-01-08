---
title: sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18ccbda41c5b7683c33bc0258a05738ab227ec69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813318"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce i comandi per le transazioni contrassegnate per la replica in formato leggibile. **sp_replshowcmds** può essere eseguito solo quando le connessioni client, inclusa la connessione corrente, non leggono le transazioni replicate dal log. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@maxtrans** =] *maxtrans*  
 Numero di transazioni per cui si desidera restituire informazioni. *maxtrans* viene **int**, il valore predefinito è **1**, che consente di specificare il numero massimo di transazioni in attesa di replica per il quale **sp_replshowcmds** Restituisce informazioni.  
  
## <a name="result-sets"></a>Set di risultati  
 **sp_replshowcmds** è una procedura diagnostica che restituisce informazioni sul database di pubblicazione da cui viene eseguito.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Numero di sequenza del comando.|  
|**originator_id**|**int**|ID dell'origine del comando, sempre **0**.|  
|**publisher_database_id**|**int**|ID del database di pubblicazione, sempre **0**.|  
|**article_id**|**int**|ID dell'articolo.|  
|**type**|**int**|Tipo di comando.|  
|**comando**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="remarks"></a>Note  
 **sp_replshowcmds** viene utilizzata nella replica transazionale.  
  
 Usando **sp_replshowcmds**, è possibile visualizzare le transazioni che sono attualmente non distribuiti (quelle che rimangono nel log delle transazioni che non sono stati inviati al server di distribuzione).  
  
 I client che eseguono **sp_replshowcmds** e **sp_replcmds** nello stesso database ricevono l'errore 18752.  
  
 Per evitare questo errore, è necessario disconnettere il primo client o il ruolo del client come agente di lettura log deve essere liberato eseguendo **sp_replflush**. Dopo che tutti i client sono stati disconnessi dall'agente di lettura log **sp_replshowcmds** può essere eseguito correttamente.  
  
> [!NOTE]  
>  **sp_replshowcmds** deve essere eseguito solo per risolvere i problemi con la replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_replshowcmds**.  
  
## <a name="see-also"></a>Vedere anche  
 [Messaggi di errore](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

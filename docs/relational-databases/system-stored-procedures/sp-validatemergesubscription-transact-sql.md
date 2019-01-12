---
title: sp_validatemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergesubscription
- sp_validatemergesubscription_TSQL
helpviewer_keywords:
- sp_validatemergesubscription
ms.assetid: d73ad03c-e5b3-4606-a0ee-7d75e12762a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ddf4c57901682cb099dc0e92c09b763651e32f6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131711"
---
# <a name="spvalidatemergesubscription-transact-sql"></a>sp_validatemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esegue la convalida della sottoscrizione specificata. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>Argomenti  
 [**@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@subscriber=** ] **'***sottoscrittore***'**  
 Nome del Sottoscrittore. *Sottoscrittore* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 Nome del database di sottoscrizione. *subscriber_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@level=** ] *livello*  
 Tipo di convalida da eseguire. *livello* viene **tinyint**, non prevede alcun valore predefinito. I possibili valori del livello sono i seguenti.  
  
|Valore del livello|Descrizione|  
|-----------------|-----------------|  
|**1**|Convalida solo tramite conteggio delle righe.|  
|**2**|Convalida mediante conteggio delle righe e checksum.|  
|**3**|Convalida mediante conteggio delle righe e checksum binario.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_validatemergesubscription** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_validatemergesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  

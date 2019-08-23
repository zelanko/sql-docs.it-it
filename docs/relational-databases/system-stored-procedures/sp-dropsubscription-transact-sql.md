---
title: sp_dropsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 21d90c94c73eb6e49fcfedf997fffe2881146a22
ms.sourcegitcommit: 676458a9535198bff4c483d67c7995d727ca4a55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69903634"
---
# <a name="sp_dropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Elimina le sottoscrizioni di un determinato articolo, pubblicazione o set di sottoscrizioni nel server di pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione associata. *Publication* è di **tipo sysname**e il valore predefinito è null. Se **tutti**, tutte le sottoscrizioni per tutte le pubblicazioni per il Sottoscrittore specificato vengono annullate. la *pubblicazione* è un parametro obbligatorio.  
  
`[ @article = ] 'article'`Nome dell'articolo. *article* è di **tipo sysname**e il valore predefinito è null. Se **tutte**, le sottoscrizioni di tutti gli articoli per ogni pubblicazione e Sottoscrittore specificati vengono eliminate. Usare **tutti per le** pubblicazioni che consentono l'aggiornamento immediato.  
  
`[ @subscriber = ] 'subscriber'`Nome del Sottoscrittore per il quale vengono eliminate le sottoscrizioni. *Subscriber* è di **tipo sysname**e non prevede alcun valore predefinito. Se **tutti**, vengono eliminate tutte le sottoscrizioni per tutti i sottoscrittori.  
  
`[ @destination_db = ] 'destination_db'`Nome del database di destinazione. *destination_db* è di **tipo sysname**e il valore predefinito è null. con cui vengono eliminate tutte le sottoscrizioni dal Sottoscrittore specificato.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_dropsubscription** viene utilizzata per la replica snapshot e transazionale.  
  
 Se si elimina la sottoscrizione di un articolo in una pubblicazione a sincronizzazione immediata, non è possibile aggiungerla nuovamente, a meno che le sottoscrizioni di tutti gli articoli della pubblicazione non vengano eliminate e aggiunte nuovamente in una sola operazione.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** , del ruolo predefinito del database **db_owner** o dell'utente che ha creato la sottoscrizione possono eseguire **sp_dropsubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una sottoscrizione push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  

---
title: sp_dropanonymousagent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
manager: craigg
ms.openlocfilehash: dc5cc9c4d7bb7ca9b2d758e33142d140bf6fc6fa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818983"
---
# <a name="spdropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina dal server di pubblicazione un agente anonimo per il monitoraggio della replica nel server di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@subid=**] *sub_id*  
 Identificatore globale di una sottoscrizione anonima. *sub_id* viene **uniqueidentifier**, non prevede alcun valore predefinito. Questo identificatore può essere recuperato nel Sottoscrittore utilizzando **sp_helppullsubscription**. Il valore di **subid** campo del set di risultati restituito è l'identificatore globale.  
  
 [  **@type=**] *tipo*  
 Tipo di sottoscrizione. *tipo di* viene **int**, non prevede alcun valore predefinito. I valori validi sono **1** oppure **2**. Specificare **1**, se la replica snapshot o la replica transazionale con l'agente di distribuzione. Specificare **2**, se tramite l'agente di Merge di replica di tipo merge.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropanonymousagent** viene utilizzata in tutti i tipi di replica.  
  
 Questa stored procedure consente di eliminare solo agenti di sottoscrizioni anonime, non di sottoscrizione note.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** ruolo predefinito del database nel database di distribuzione possono eseguire **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

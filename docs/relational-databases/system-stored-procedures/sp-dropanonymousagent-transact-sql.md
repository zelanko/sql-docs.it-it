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
author: VanMSFT
ms.openlocfilehash: 7e82023ed750c77d87a2536debfb5fceb7321db4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911949"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina dal server di pubblicazione un agente anonimo per il monitoraggio della replica nel server di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @subid = ] sub_id`Identificatore globale di una sottoscrizione anonima. *sub_id* è di tipo **uniqueidentifier**e non prevede alcun valore predefinito. Questo identificatore può essere recuperato nel Sottoscrittore utilizzando **sp_helppullsubscription**. Il valore nel campo **subid** del set di risultati restituito è questo identificatore globale.  
  
`[ @type = ] type`Tipo di sottoscrizione. *Type* è di tipo **int**e non prevede alcun valore predefinito. I valori validi sono **1** o **2**. Specificare **1**se la replica snapshot o transazionale utilizza la agente di distribuzione. Specificare **2**se eseguire la replica di tipo merge utilizzando la agente di merge.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dropanonymousagent** viene utilizzato in tutti i tipi di replica.  
  
 Questa stored procedure consente di eliminare solo agenti di sottoscrizioni anonime, non di sottoscrizione note.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del database **db_owner** nel database di distribuzione possono eseguire **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

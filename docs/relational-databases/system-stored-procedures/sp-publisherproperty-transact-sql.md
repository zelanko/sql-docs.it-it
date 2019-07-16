---
title: sp_publisherproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c4ba291619ae756fa9803606eda4427a155ae39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896486"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza o modifica proprietà server di pubblicazione per non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. Questa stored procedure viene eseguita nel database di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@publisher** = ] **'***publisher***'**  
 Nome del server di pubblicazione eterogeneo. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@propertyname** =] **'***propertyname***'**  
 Nome della proprietà da impostare. *PropertyName* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**xactsetbatching**|Indica se le transazioni nel server di pubblicazione sono raggruppate in set con consistenza transazionale per elaborazioni successive, noti come Xactset. Un valore pari **abilitato** significa che è possibile creare XactSet, ovvero l'impostazione predefinita. Un valore pari **disabilitato** significa che XactSet esistenti vengono elaborati da alcun nuovo XactSet viene creati.|  
|**xactsetjob**|Indica se è attivo il processo Xactset per la creazione di Xactset. Un valore pari **abilitato** significa che il processo Xactset viene eseguito periodicamente per creazione di XactSet nel server di pubblicazione. Un valore pari **disabilitato** significa che il XactSet vengono creati solo dall'agente di lettura Log quando si esegue il polling server di pubblicazione per le modifiche.|  
|**xactsetjobinterval**|Intervallo tra le esecuzioni del processo Xactset, espresso in minuti.|  
  
 Quando *propertyname* viene omessa vengono restituite tutte le proprietà impostabili.  
  
 [ **@propertyvalue** =] **'***propertyvalue***'**  
 Nuovo valore per la proprietà. *PropertyValue* viene **sysname**, con un valore predefinito NULL. Quando *propertyvalue* viene omesso, l'impostazione corrente per la proprietà viene restituita.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Restituisce le proprietà delle pubblicazioni seguenti che è possibile impostare:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|È l'impostazione corrente per la proprietà nel **propertyname** colonna.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_publisherproperty** viene utilizzata nella replica transazionale per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione.  
  
 Quando solo *server di pubblicazione* è specificato, il set di risultati include le impostazioni correnti per tutte le proprietà che è possibile impostare.  
  
 Quando *propertyname* viene specificato, viene visualizzata solo la proprietà del set di risultati.  
  
 Se si specificano tutti i parametri, la proprietà viene modificata e non viene restituito alcun set di risultati.  
  
 Quando si modifica il **xactsetjobinterval** proprietà per un processo in esecuzione, è necessario riavviare il processo per il nuovo intervallo rendere effettive.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server nel server di distribuzione possono eseguire **sp_publisherproperty**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare il processo del set di transazioni per un server di pubblicazione Oracle &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: sp_resyncmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63a3ff2cdb075dc8ce48aaa6c6951458d12710b0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538153"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Risincronizza una sottoscrizione di tipo merge in base a uno stato di convalida noto specificato. In questo modo è possibile forzare la convergenza oppure sincronizzare il database di sottoscrizione fino a un momento specifico, ad esempio fino all'ultima convalida riuscita oppure fino a una data specificata. Quando si risincronizza una sottoscrizione in base a questa modalità, lo snapshot non viene riapplicato. Questa stored procedure non viene utilizzata per sottoscrizioni di replica snapshot o transazionali. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL. Il valore NULL è valido se la stored procedure viene eseguita nel server di pubblicazione. Se la stored procedure viene eseguita nel Sottoscrittore, è necessario specificare un server di pubblicazione.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del database di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito è NULL. Il valore NULL è valido se la stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Se la stored procedure viene eseguita nel Sottoscrittore, è necessario specificare un server di pubblicazione.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione*viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL. Il valore NULL è valido se la stored procedure viene eseguita nel Sottoscrittore. Se la stored procedure viene eseguita nel server di pubblicazione, è necessario specificare un Sottoscrittore.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL. Il valore NULL è valido se la stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore. Se la stored procedure viene eseguita nel server di pubblicazione, è necessario specificare un Sottoscrittore.  
  
`[ @resync_type = ] resync_type` Definisce quando avviare il processo di risincronizzazione. *resync_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|La sincronizzazione ha inizio dopo lo snapshot iniziale. Questa opzione comporta il maggior utilizzo di risorse, in quanto tutte le modifiche apportate dopo lo snapshot iniziale vengono riapplicate nel Sottoscrittore.|  
|**1**|La sincronizzazione ha inizio dopo l'ultima convalida riuscita. Tutte le generazioni nuove o incomplete eseguite dopo l'ultima convalida riuscita vengono riapplicate nel Sottoscrittore.|  
|**2**|La sincronizzazione ha inizio dalla data specificata *resync_date_str*. Tutte le generazioni nuove o incomplete eseguite dopo tale data vengono riapplicate nel Sottoscrittore.|  
  
`[ @resync_date_str = ] resync_date_string` Definisce la data quando avviare il processo di risincronizzazione. *resync_date_string* viene **nvarchar(30)**, con un valore predefinito è NULL. Questo parametro viene utilizzato quando la *resync_type* è un valore di **2**. La data specificata viene convertita nell'equivalente **datetime** valore.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_resyncmergesubscription** viene utilizzata nella replica di tipo merge.  
  
 Un valore pari **0** per il *resync_type* parametro, che Riapplica tutte le modifiche apportate dopo lo snapshot iniziale, potrebbe essere a elevato utilizzo di risorse, ma comunque molto minore rispetto a una reinizializzazione completa. Se, ad esempio, lo snapshot iniziale è stato recapitato un mese fa, vengono riapplicati i dati relativi all'ultimo mese. Se lo snapshot iniziale contiene 1 gigabyte (GB) di dati, ma i dati modificati nell'ultimo mese corrispondono a 2 megabyte (MB), risulta più efficiente riapplicare i dati anziché l'intero snapshot da 1 GB.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_resyncmergesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

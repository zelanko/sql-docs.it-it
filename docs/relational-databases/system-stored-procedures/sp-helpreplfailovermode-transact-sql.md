---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19fafb4b3ef3737018aaae21992f0b6a859c7ef3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796432"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza la modalità di failover corrente di una sottoscrizione. Questa stored procedure viene eseguita in qualsiasi database del Sottoscrittore. Per altre informazioni sulle modalità di failover, vedere [le sottoscrizioni aggiornabili per la replica transazionale](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione che partecipa all'aggiornamento del Sottoscrittore. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito. Il server di pubblicazione deve essere già configurato per la pubblicazione.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione che partecipa all'aggiornamento del Sottoscrittore. *pubblicazione*viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' OUTPUT**  
 Restituisce il valore intero della modalità di failover ed è un' **OUTPUT** parametro. *failover_mode_id* è un **tinyint** con valore predefinito è **0**. Viene restituito **0** per l'aggiornamento immediato e **1** per l'aggiornamento in coda.  
  
 [**@failover_mode=**] **'***failover_mode***' OUTPUT**  
 Restituisce la modalità di implementazione delle modifiche dei dati nel Sottoscrittore. *failover_mode* è un **nvarchar(10)** con valore predefinito è NULL. È un' **OUTPUT** parametro.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Controllo immediato**|Aggiornamento immediato: gli aggiornamenti implementati nel Sottoscrittore vengono propagati immediatamente al server di pubblicazione tramite il protocollo di commit in due fasi (2PC).|  
|**In coda**|Aggiornamento in coda: gli aggiornamenti implementati nel Sottoscrittore vengono archiviati in una coda.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpreplfailovermode** viene utilizzata nella replica snapshot o transazionale per le sottoscrizioni sono abilitate per l'aggiornamento immediato con aggiornamento in coda come failover, in caso di errore.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  

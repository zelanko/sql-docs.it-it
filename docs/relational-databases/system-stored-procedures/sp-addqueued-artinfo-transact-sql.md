---
title: sp_addqueued_artinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c326a8e3a5fa2bd95f536d434ff9782952ba70d3
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590896"
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  Il [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) procedura deve essere utilizzata al posto di **sp_addqueued_artinfo**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) genera uno script che contiene il **sp_addqueued_artinfo** e **sp_addsynctrigger** chiamate.  
  
 Crea il [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) tabella nel Sottoscrittore utilizzata per tenere traccia delle informazioni sulla sottoscrizione di articolo (aggiornamento in coda e l'aggiornamento immediato con aggiornamento in coda come Failover). Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@artid=** ] **'**_artid_**'**  
 ID dell'articolo. *artid* viene **int**, non prevede alcun valore predefinito  
  
 [  **@article=**] **'**_articolo_**'**  
 Nome dell'articolo per cui si desidera creare lo script. *articolo* viene **sysname**, non prevede alcun valore predefinito  
  
 [  **@publisher=**] **'**_editore_**'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 Nome del database del server di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'**_pubblicazione_**'**  
 Nome della pubblicazione per cui si desidera creare lo script. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@dest_table=** ] _' dest_table_**'**  
 Nome della tabella di destinazione. *dest_table* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@owner =** ] **'**_proprietario_**'**  
 Proprietario della sottoscrizione. *proprietario* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@cft_table=** ] **'**_cft_table_**'**  
 Nome della tabella dei conflitti ad aggiornamento in coda per l'articolo. *cft_table*viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addqueued_artinfo** viene usato dall'agente di distribuzione come parte dell'inizializzazione della sottoscrizione. In genere, non viene eseguita dagli utenti, ma può risultare utile se l'utente deve configurare una sottoscrizione in modo manuale.  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) invece di **sp_addqueued_artinfo**.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addqueued_artinfo**.  
  
## <a name="see-also"></a>Vedere anche  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

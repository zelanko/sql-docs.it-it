---
title: sysmail_event_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ac38c2e54fde2beb02e009e00b9f587e9265a43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759949"
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni messaggio di Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito dal sistema di Posta elettronica database. (Messaggio in questo contesto si riferisce a un messaggio, ad esempio un messaggio di errore, non un messaggio di posta elettronica). Configura il **a livello di registrazione** parametro usando la **configurazione parametri di sistema** la finestra di dialogo di configurazione guidata posta elettronica Database, o il [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)stored procedure per determinare quali messaggi vengono restituiti.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|Identificatore degli elementi nel log.|  
|**event_type**|**varchar(11)**|Tipo di avviso inserito nel log. I possibili valori sono errori, avvisi, messaggi informativi, messaggi di operazione riuscita e altri messaggi interni.|  
|**log_date**|**datetime**|Data e ora di creazione della voce del log.|  
|**description**|**nvarchar(max)**|Testo del messaggio registrato.|  
|**process_id**|**int**|ID di processo del programma esterno Posta elettronica database. In genere, viene modificato a ogni avvio del programma esterno Posta elettronica database.|  
|**mailitem_id**|**int**|Identificatore dell'elemento di posta nella coda della posta. Se il messaggio non è correlato a un elemento di posta elettronica specifico, viene restituito NULL.|  
|**account_id**|**int**|Il **account_id** dell'account correlato all'evento. Se il messaggio non è correlato a un account specifico, viene restituito NULL.|  
|**last_mod_date**|**datetime**|Data e ora dell'ultima modifica della riga.|  
|**last_mod_user**|**sysname**|Autore dell'ultima modifica della riga. Per i messaggi di posta elettronica corrisponde all'utente che ha inviato il messaggio. Per i messaggi generati dal programma esterno Posta elettronica database corrisponde al contesto utente del programma.|  
  
## <a name="remarks"></a>Note  
 La risoluzione dei problemi di posta elettronica Database, eseguire la ricerca di **sysmail_event_log** vista per gli eventi correlati a errori di posta elettronica. Alcuni messaggi, ad esempio quelli relativi agli errori del programma esterno Posta elettronica database, non sono associati a messaggi di posta elettronica specifici. Per cercare gli errori correlati a specifici messaggi di posta elettronica, cercare il **mailitem_id** del messaggio in questione il **sysmail_faileditems** visualizzare e quindi cercare il **sysmail_event_log**per i messaggi relativi a quella **mailitem_id**. Quando viene restituito un errore dal **sp_send_dbmail**, messaggio di posta elettronica non viene inviato al sistema di posta elettronica Database e non verrà visualizzato l'errore in questa visualizzazione.  
  
 Quando i tentativi di recapito con singoli account hanno esito negativo, i messaggi di errore rimangono visualizzati durante i successivi tentativi di invio fino a quando il recapito dell'elemento di posta non ha definitivamente esito positivo o negativo. In caso di esito positivo finale, tutti gli errori accumulati registrati come avvisi separati tra cui il **account_id**. Pertanto, è possibile che vengano visualizzati messaggi di avviso anche se il messaggio di posta elettronica è stato inviato. In caso di errore finale del recapito, tutti gli avvisi precedenti registrati come messaggio di errore senza un' **account_id**, dal momento che tutti gli account hanno avuto esito negativo.  
  
## <a name="permissions"></a>Permissions  
 È necessario essere un membro del **sysadmin** ruolo predefinito del server o il **DatabaseMailUserRole** ruolo del database per accedere a questa visualizzazione. I membri del **DatabaseMailUserRole** che non fanno parte di **sysadmin** ruolo, possono visualizzare solo gli eventi di posta elettronica che hanno inviato personalmente.  
  
## <a name="see-also"></a>Vedere anche  
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Programma esterno di Posta elettronica database](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  

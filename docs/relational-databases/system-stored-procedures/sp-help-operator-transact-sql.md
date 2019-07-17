---
title: sp_help_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
author: stevestein
ms.author: sstein
ms.openlocfilehash: e6568b15a12949180ca0e2df41063c100abc3290
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085306"
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli operatori definiti per il server.  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @operator_name = ] 'operator_name'` Il nome dell'operatore. *nome_operatore* viene **sysname**. Se *nome_operatore* viene omesso, vengono restituite informazioni su tutti gli operatori.  
  
`[ @operator_id = ] operator_id` Il numero di identificazione dell'operatore per il quale vengono richieste informazioni. *operator_id*viene **int**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *operator_id* oppure *nome_operatore* devono essere specificati, ma non è possibile specificarli entrambi.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Numero di identificazione dell'operatore.|  
|**name**|**sysname**|Nome dell'operatore.|  
|**enabled**|**tinyint**|Specifica se l'operatore è disponibile per la ricezione di notifiche:<br /><br /> **1** = Sì<br /><br /> **0** = No|  
|**email_address**|**nvarchar(100)**|Indirizzo di posta elettronica dell'operatore.|  
|**last_email_date**|**int**|Data dell'ultima notifica dell'operatore tramite posta elettronica.|  
|**last_email_time**|**int**|Ora dell'ultima notifica dell'operatore tramite posta elettronica.|  
|**pager_address**|**nvarchar(100)**|Indirizzo cercapersone dell'operatore.|  
|**last_pager_date**|**int**|Data dell'ultima notifica dell'operatore tramite cercapersone.|  
|**last_pager_time**|**int**|Ora dell'ultima notifica dell'operatore tramite cercapersone.|  
|**weekday_pager_start_time**|**int**|Inizio del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone in un giorno feriale.|  
|**weekday_pager_end_time**|**int**|Termine del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone in un giorno feriale|  
|**saturday_pager_start_time**|**int**|Inizio del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone il sabato.|  
|**saturday_pager_end_time**|**int**|Termine del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone il sabato.|  
|**sunday_pager_start_time**|**int**|Inizio del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone la domenica.|  
|**sunday_pager_end_time**|**int**|Termine del periodo di tempo durante il quale l'operatore è disponibile per ricevere notifiche tramite cercapersone la domenica.|  
|**pager_days**|**tinyint**|Maschera di bit (**1** = domenica **64** = sabato) dei giorni della-settimana che indica quando l'operatore è disponibile per ricevere le notifiche tramite cercapersone.|  
|**netsend_address**|**nvarchar(100)**|Indirizzo dell'operatore per le notifiche dei messaggi popup di rete.|  
|**last_netsend_date**|**int**|Data dell'ultima notifica inviata all'operatore tramite un messaggio popup di rete.|  
|**last_netsend_time**|**int**|Ora dell'ultima notifica inviata all'operatore tramite un messaggio popup di rete.|  
|**category_name**|**sysname**|Nome della categoria a cui appartiene l'operatore.|  
  
## <a name="remarks"></a>Note  
 **sp_help_operator** deve essere eseguita la **msdb** database.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sull'operatore `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

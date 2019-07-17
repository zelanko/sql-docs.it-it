---
title: sp_add_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 49d7ac030eb8e391f083311fc0248b0f0752e72a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121023"
---
# <a name="spaddoperator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un operatore (destinatario delle notifiche) da utilizzare con avvisi e processi.  
  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]   
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]   
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]   
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'` Il nome di un operatore (destinatario della notifica). Questo nome deve essere univoco e non può contenere la percentuale ( **%** ) caratteri. *nome* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @enabled = ] enabled` Indica lo stato corrente dell'operatore. *abilitata* viene **tinyint**, il valore predefinito è **1** (abilitato). Se **0**, l'operatore non è abilitato e non riceve le notifiche.  
  
`[ @email_address = ] 'email_address'` L'indirizzo di posta elettronica dell'operatore. Questa stringa viene passata direttamente al sistema di posta elettronica. *email_address* viene **nvarchar(100)** , con un valore predefinito è NULL.  
  
 È possibile specificare un indirizzo di posta elettronica fisico o un alias per *email_address*. Ad esempio:  
  
 «**jdoe**'o' **jdoe@xyz.com** »  
  
> [!NOTE]  
>  È necessario utilizzare l'indirizzo di posta elettronica per Posta elettronica database.  
  
`[ @pager_address = ] 'pager_address'` Indirizzo cercapersone dell'operatore. Questa stringa viene passata direttamente al sistema di posta elettronica. *pager_address* viene **narchar(100)** , con un valore predefinito è NULL.  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time` Il tempo trascorso il quale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent invia notifiche al cercapersone dell'operatore specificato nei giorni della settimana, dal lunedì al venerdì. *weekday_pager_start_time*viene **int**, il valore predefinito è **090000**, che indica le 9.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time` Il tempo trascorso il quale **SQLServerAgent** servizio non è più invia notifiche al cercapersone dell'operatore specificato nei giorni della settimana, dal lunedì al venerdì. *weekday_pager_end_time*viene **int**, e il valore predefinito è 180000, che indica le 18.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time` Il tempo trascorso il quale **SQLServerAgent** servizio invia notifiche al cercapersone dell'operatore specificato sabato. *saturday_pager_start_time* viene **int**, valore predefinito è 090000, che indica le 9.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time` Il tempo trascorso il quale **SQLServerAgent** servizio non è più invia notifiche al cercapersone dell'operatore specificato sabato. *saturday_pager_end_time*viene **int**, il valore predefinito è **180000**, ovvero le 18.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time` Il tempo trascorso il quale **SQLServerAgent** servizio invia notifiche al cercapersone dell'operatore specificato la domenica. *sunday_pager_start_time*viene **int**, il valore predefinito è **090000**, che indica le 9.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time` Il tempo trascorso il quale **SQLServerAgent** servizio non è più invia notifiche al cercapersone dell'operatore specificato la domenica. *sunday_pager_end_time*viene **int**, il valore predefinito è **180000**, ovvero le 18.00 nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @pager_days = ] pager_days` È un numero che indica i giorni in cui l'operatore è disponibile per rintracciato tramite cercapersone (all'ora di inizio e fine specificata). *pager_days*viene **tinyint**, il valore predefinito è **0** che indica l'operatore non è mai disponibile per la ricezione di una pagina. I valori validi sono compresi **0** attraverso **127**. *pager_days*viene calcolato sommando i singoli valori dei giorni necessari. Ad esempio, da lunedì a venerdì viene **2**+**4**+**8**+**16** + **32** = **62**. Nella tabella seguente vengono elencati i valori disponibili per ogni giorno della settimana.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Domenica|  
|**2**|Lunedì|  
|**4**|Martedì|  
|**8**|Mercoledì|  
|**16**|Giovedì|  
|**32**|Venerdì|  
|**64**|Sabato|  
  
`[ @netsend_address = ] 'netsend_address'` L'indirizzo di rete dell'operatore a cui viene inviato il messaggio di rete. *netsend_address*viene **nvarchar(100)** , con un valore predefinito è NULL.  
  
`[ @category_name = ] 'category'` Il nome della categoria per questo operatore. *categoria* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **sp_add_operator** deve essere eseguita la **msdb** database.  
  
 L'invio di messaggi sul cercapersone è supportato dal sistema di posta elettronica, in cui deve essere disponibile la funzionalità per il trasferimento di messaggi su cercapersone.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_add_operator**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono impostate e attivate le informazioni per l'operatore `danwi`. L'operatore è abilitato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent invia notifiche tramite cercapersone da lunedì a venerdì, dalle 8.00 alle 17.00.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

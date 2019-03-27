---
title: sp_addmessage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addmessage
- sp_addmessage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addmessage
ms.assetid: 54746d30-f944-40e5-a707-f2d9be0fb9eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63d206e6b6f32aeb12e2e04b9edc2ef1d84599b2
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494233"
---
# <a name="spaddmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia un nuovo messaggio di errore definito dall'utente in un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. I messaggi archiviati tramite **sp_addmessage** possono essere visualizzati usando la **Sys. Messages** vista del catalogo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ \@msgnum = ] msg_id` È l'ID del messaggio. *msg_id* viene **int** con valore predefinito è NULL. *msg_id* per errore definiti dall'utente dei messaggi possono essere un numero intero compreso tra 50.001 e 2.147.483.647. La combinazione delle *msg_id* e *language* deve essere univoco; viene restituito un errore se l'ID esiste già per la lingua specificata.  
  
`[ \@severity = ]severity` È il livello di gravità dell'errore. *livello di gravità* viene **smallint** con valore predefinito è NULL. I livelli validi sono compresi tra 1 e 25. Per altre informazioni sui livelli di gravità, vedere [Gravità degli errori del Motore di database](../../relational-databases/errors-events/database-engine-error-severities.md).  
  
`[ \@msgtext = ] 'msg'` È il testo del messaggio di errore. *MSG* viene **nvarchar(255** con valore predefinito è NULL.  
  
`[ \@lang = ] 'language'` È il linguaggio per questo messaggio. *linguaggio* viene **sysname** con valore predefinito è NULL. Poiché nello stesso server, è possono installare più lingue *linguaggio* specifica la lingua in cui viene scritto ogni messaggio. Quando *linguaggio* viene omesso, il linguaggio è la lingua predefinita per la sessione.  
  
`[ \@with_log = ] { 'TRUE' | 'FALSE' }` È se il messaggio deve essere scritto nel registro applicazioni di Windows quando si verifica. **\@WITH_LOG** viene **varchar (5)** con valore predefinito è FALSE. Se è TRUE, l'errore viene sempre scritto nel registro applicazioni di Windows. Se è FALSE, l'errore viene scritto nel registro applicazioni di Windows a seconda della modalità con cui è stato generato. Solo i membri del **sysadmin** ruolo del server può usare questa opzione.  
  
> [!NOTE]  
>  Se un messaggio viene scritto nel registro applicazioni di Windows, viene registrato inoltre nel file di log degli errori di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
`[ \@replace = ] 'replace'` Se specificato come stringa *sostituire*, un messaggio di errore esistente viene sovrascritto con il nuovo livello di testo e la gravità messaggio. *Sostituire* viene **varchar(7)** con valore predefinito è NULL. Questa opzione deve essere specificata se *msg_id* esiste già. Se viene sostituito un messaggio in inglese Messaggio in inglese, il livello di gravità viene sostituito per i messaggi in tutte le altre lingue che presentano lo stesso *msg_id*.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Per le versioni non in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario che un messaggio sia disponibile nella versione inglese (Stati Uniti) per poterlo aggiungere in un'altra lingua. La gravità delle due versioni del messaggio devono corrispondere.  
  
 Quando vengono localizzati messaggi che includono parametri, utilizzare i numeri di parametro che corrispondono ai parametri del messaggio originale e inserire un punto esclamativo (!) dopo ogni numero di parametro.  
  
|Messaggio originale|Messaggio localizzato|  
|----------------------|-----------------------|  
|'Original message param 1: %s,<br /><br /> param 2: %d'|'Messaggio localizzato param 1: %1!<br /><br /> param 2: %2!'|  
  
 A causa delle differenze nella sintassi delle varie lingue, i numeri di parametro nel messaggio localizzato potrebbero non essere nella stessa sequenza del messaggio originale.  
  
## <a name="permissions"></a>Permissions  
Richiede l'appartenenza al **sysadmin** oppure **serveradmin** ruoli predefiniti del server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-defining-a-custom-message"></a>A. Definizione di un messaggio personalizzato  
 L'esempio seguente aggiunge un messaggio personalizzato per **Sys. Messages**.  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>b. Aggiunta di un messaggio in due lingue  
 Nell'esempio seguente viene innanzitutto aggiunto un messaggio in inglese (Stati Uniti) e quindi viene aggiunto lo stesso messaggio in francese`.`  
  
```  
USE master;  
GO  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'The item named %s already exists in %s.',   
   @lang = 'us_english';  
  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'L''élément nommé %1! existe déjà dans %2!',   
   @lang = 'French';  
GO  
```  
  
### <a name="c-changing-the-order-of-parameters"></a>C. Modifica dell'ordine dei parametri  
 Nell'esempio seguente viene innanzitutto aggiunto un messaggio in inglese (Stati Uniti) e quindi viene aggiunto un messaggio localizzato in cui è stato modificato l'ordine dei parametri.  
  
```  
USE master;  
GO  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        N'This is a test message with one numeric  
        parameter (%d), one string parameter (%s),   
        and another string parameter (%s).',  
    @lang = 'us_english';  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        -- In the localized version of the message,  
        -- the parameter order has changed. The   
        -- string parameters are first and second  
        -- place in the message, and the numeric   
        -- parameter is third place.  
        N'Dies ist eine Testmeldung mit einem   
        Zeichenfolgenparameter (%3!),  
        einem weiteren Zeichenfolgenparameter (%2!),   
        und einem numerischen Parameter (%1!).',  
    @lang = 'German';  
GO    
  
-- Changing the session language to use the U.S. English  
-- version of the error message.  
SET LANGUAGE us_english;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2') -- error, severity, state,  
GO                                       -- parameters.  
  
-- Changing the session language to use the German  
-- version of the error message.  
SET LANGUAGE German;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2'); -- error, severity, state,   
GO                                       -- parameters.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

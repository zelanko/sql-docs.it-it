---
title: sp_addmessage (Transact-SQL) Documenti Microsoft
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
ms.openlocfilehash: d040fa0ccfe9b962f8847db0a841b95a534326fa
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531030"
---
# <a name="sp_addmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia un nuovo messaggio di errore definito dall'utente in un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. I messaggi archiviati utilizzando **sp_addmessage** possono essere visualizzati utilizzando la visualizzazione del catalogo **sys.messages.**  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @msgnum = ] msg_id`È l'ID del messaggio. *msg_id* è **int** con un valore predefinito NULL. *msg_id* per i messaggi di errore definiti dall'utente può essere un numero intero compreso tra 50.001 e 2.147.483.647.For user-defined error messages can be an integer between 50,001 and 2,147,483,647. La combinazione di *msg_id* e *lingua* deve essere unica; se l'ID esiste già per la lingua specificata, viene restituito un errore.  
  
`[ @severity = ]severity`È il livello di gravità dell'errore. *severity* è **smallint** con un valore predefinito null. I livelli validi sono compresi tra 1 e 25. Per altre informazioni sui livelli di gravità, vedere [Gravità degli errori del Motore di database](../../relational-databases/errors-events/database-engine-error-severities.md).  
  
`[ @msgtext = ] 'msg'`È il testo del messaggio di errore. *msg* è **di tipo nvarchar(255)** con un valore predefinito NULL.  
  
`[ @lang = ] 'language'`È la lingua per questo messaggio. *language* è **sysname** con un valore predefinito NULL. Poiché più lingue possono essere installate nello stesso server, *language* specifica la lingua in cui viene scritto ogni messaggio. Quando *la lingua* viene omessa, la lingua è la lingua predefinita per la sessione.  
  
`[ @with_log = ] { 'TRUE' | 'FALSE' }`È se il messaggio deve essere scritto nel registro applicazioni di Windows quando si verifica. with_log è **varchar(5)** con il valore predefinito FALSE. ** \@** Se è TRUE, l'errore viene sempre scritto nel registro applicazioni di Windows. Se è FALSE, l'errore viene scritto nel registro applicazioni di Windows a seconda della modalità con cui è stato generato. Solo i membri del ruolo del server **sysadmin** possono utilizzare questa opzione.  
  
> [!NOTE]  
>  Se un messaggio viene scritto nel registro applicazioni di Windows, viene registrato inoltre nel file di log degli errori di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
`[ @replace = ] 'replace'`Se specificato come stringa *replace*, un messaggio di errore esistente viene sovrascritto con il nuovo testo del messaggio e il livello di gravità. *replace* è **varchar(7)** con un valore predefinito di NULL. Questa opzione deve essere specificata se *msg_id* già esistente. Se si sostituisce un messaggio in inglese americano, il livello di gravità viene sostituito per tutti i messaggi in tutte le altre lingue che hanno lo stesso *msg_id*.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 Per le versioni non in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario che un messaggio sia disponibile nella versione inglese (Stati Uniti) per poterlo aggiungere in un'altra lingua. La gravità delle due versioni del messaggio devono corrispondere.  
  
 Quando vengono localizzati messaggi che includono parametri, utilizzare i numeri di parametro che corrispondono ai parametri del messaggio originale e inserire un punto esclamativo (!) dopo ogni numero di parametro.  
  
|Messaggio originale|Messaggio localizzato|  
|----------------------|-----------------------|  
|'Original message param 1: %s,<br /><br /> param 2: %d'|'Messaggio localizzato param 1: %1!<br /><br /> param 2: %2!'|  
  
 A causa delle differenze nella sintassi delle varie lingue, i numeri di parametro nel messaggio localizzato potrebbero non essere nella stessa sequenza del messaggio originale.  
  
## <a name="permissions"></a>Autorizzazioni  
Richiede l'appartenenza ai ruoli predefiniti del server **sysadmin** o **serveradmin.**  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-defining-a-custom-message"></a>R. Definizione di un messaggio personalizzato  
 Nell'esempio seguente viene aggiunto un messaggio personalizzato a **sys.messages**.  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. Aggiunta di un messaggio in due lingue  
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
 [sp_altermessage &#40;Transact-SQLTransact-&#41;SQL](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQLTransact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

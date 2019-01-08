---
title: sysmail_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe47df497b61d35c66bfebfb3ba5a75fad0e183
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588555"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le impostazioni di configurazione per Posta elettronica database. Le impostazioni di configurazione specificate con **sysmail_configure_sp** si applicano all'intera [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [**@parameter_name** =] **'**_parameter_name_**'**  
 Nome del parametro da modificare.  
  
 [**@parameter_value** =] **'**_parameter_value_**'**  
 Nuovo valore del parametro  
  
 [**@description** =] **'**_descrizione_**'**  
 Descrizione del parametro.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Posta elettronica database utilizza i parametri seguenti:  
  
||||  
|-|-|-|  
|Nome parametro|Descrizione|Valore predefinito|  
|*AccountRetryAttempts*|Numero di tentativi di invio del messaggio di posta elettronica da parte del processo di posta elettronica esterno, utilizzando ogni account nel profilo specificato.|**1**|  
|*AccountRetryDelay*|Tempo di attesa, in secondi, del processo di posta elettronica esterno tra tentativi di invio di un messaggio.|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|Periodo minimo di tempo, in secondi, durante il quale il processo di posta elettronica esterno resta attivo. Quando Posta elettronica database invia molti messaggi, aumentare questo valore per far restare Posta elettronica database attivo ed evitare l'overhead di avvii e arresti frequenti.|**600**|  
|*DefaultAttachmentEncoding*|Codifica predefinita per gli allegati di posta elettronica.|MIME|  
|*MaxFileSize*|Dimensioni massime di un allegato, in byte.|**1000000**|  
|*ProhibitedExtensions*|Elenco delimitato da virgole delle estensioni che non possono essere inviate come allegato a un messaggio di posta elettronica.|**file exe, dll, vbs e js**|  
|*LoggingLevel*|Consente di specificare i messaggi registrati nel log di Posta elettronica database. Uno dei valori numerici seguenti:<br /><br /> 1 - Modalità normale. Solo registrazione degli errori.<br /><br /> 2 - Modalità estesa. Registrazione di messaggi di errore, di avviso e informativi.<br /><br /> 3 - Modalità dettagliata. Registrazione di messaggi di errore, di avviso, informativi, di riuscita, nonché di messaggi interni aggiuntivi. Utilizzare questa modalità per la risoluzione dei problemi.|**2**|  
  
 La stored procedure **sysmail_configure_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 **A. Impostazione di posta elettronica Database per ritentare ogni account 10 volte**  
  
 Nell'esempio seguente viene illustrato come impostare Posta elettronica database per ritentare ogni account dieci volte prima di considerare l'account irraggiungibile.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B. Impostazione della dimensione massima degli allegati su 2 MB**  
  
 Nell'esempio seguente viene illustrato come impostare le dimensioni massime per gli allegati su 2 MB.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

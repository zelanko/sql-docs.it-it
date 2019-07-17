---
title: sp_helpmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e5f044482d3e46e4e20279a437b8d9459d1d3bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002646"
---
# <a name="sphelpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su una sottoscrizione, sia push che pull, di una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione di un Sottoscrittore di ripubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%** . È necessario che la pubblicazione esista già e che sia conforme alle regole per gli identificatori. Se è NULL oppure **%** , vengono restituite informazioni su tutte le pubblicazioni di tipo merge e le sottoscrizioni nel database corrente.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, il valore predefinito è **%** . Se è NULL o %, vengono restituite informazioni su tutte le sottoscrizioni della pubblicazione specificata.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db*viene **sysname**, il valore predefinito è **%** , che restituisce informazioni su tutti i database di sottoscrizione.  
  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. Il server di pubblicazione deve essere un server valido. *server di pubblicazione*viene **sysname**, il valore predefinito è **%** , che restituisce informazioni su tutti i server di pubblicazione.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del server di pubblicazione. *publisher_db*viene **sysname**, il valore predefinito è **%** , che restituisce informazioni su tutti i database di pubblicazione.  
  
`[ @subscription_type = ] 'subscription_type'` È il tipo di sottoscrizione. *subscription_type*viene **nvarchar(15)** , i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**push** (impostazione predefinita)|Sottoscrizione push|  
|**pull**|Sottoscrizione pull|  
|**both**|Sottoscrizione sia push che pull|  
  
`[ @found = ] 'found'OUTPUT` È un flag per indicare che restituisce righe. *trovato*viene **int** e un parametro di OUTPUT con valore predefinito è NULL. **1** indica la pubblicazione è stata trovata. **0** indica la pubblicazione non è stata trovata.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|Nome della sottoscrizione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore.|  
|**subscriber_db**|**sysname**|Nome del database di sottoscrizione.|  
|**status**|**int**|Stato della sottoscrizione:<br /><br /> **0** = tutti i processi sono in attesa dell'avvio<br /><br /> **1** = uno o più processi di avvio<br /><br /> **2** = tutti i processi sono stati eseguiti correttamente<br /><br /> **3** = almeno un processo è in esecuzione<br /><br /> **4** = tutti i processi sono pianificati e inattivi<br /><br /> **5** = almeno un processo sta tentando di eseguire dopo un precedente errore<br /><br /> **6** = almeno un processo non è stato eseguito correttamente|  
|**subscriber_type**|**int**|Tipo di Sottoscrittore.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push<br /><br /> **1** = Pull<br /><br /> **2** = entrambi|  
|**priority**|**float(8)**|Numero che indica il livello di priorità della sottoscrizione.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione della sottoscrizione.|  
|**description**|**nvarchar(255)**|Breve descrizione della sottoscrizione di tipo merge.|  
|**merge_jobid**|**binary(16)**|ID di processo dell'agente di merge.|  
|**full_publication**|**tinyint**|Specifica se la sottoscrizione si riferisce a una pubblicazione completa o filtrata.|  
|**offload_enabled**|**bit**|Specifica se per un agente di replica è impostata l'esecuzione con ripartizione del carico di lavoro nel Sottoscrittore. Se è NULL, l'agente viene eseguito nel server di pubblicazione.|  
|**offload_server**|**sysname**|Nome del server in cui è in esecuzione l'agente.|  
|**use_interactive_resolver**|**int**|Specifica se durante la fase di riconciliazione viene utilizzato il sistema di risoluzione dei conflitti interattivo. Se **0**, il sistema di risoluzione interattivo non viene utilizzato.|  
|**hostname**|**sysname**|Valore fornito durante una sottoscrizione filtrata in base al valore della [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) (funzione).|  
|**subscriber_security_mode**|**smallint**|Modalità di sicurezza del sottoscrittore, dove **1** indica l'autenticazione di Windows, e **0** significa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**subscriber_login**|**sysname**|Nome dell'account di accesso nel Sottoscrittore.|  
|**subscriber_password**|**sysname**|La password effettiva per il Sottoscrittore non viene mai restituita. Il risultato viene mascherato da una " **\*\*\*\*\*\*** " stringa.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpmergesubscription** viene utilizzata nella replica di tipo merge per restituire le informazioni sulla sottoscrizione archiviate nel server di pubblicazione o sottoscrittore di ripubblicazione.  
  
 Per le sottoscrizioni anonime, il *subscription_type*valore è sempre **1** (pull). Tuttavia, è necessario eseguire [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) nel Sottoscrittore per informazioni sulle sottoscrizioni anonime.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database o elenco di accesso alla pubblicazione per la pubblicazione a cui appartiene la sottoscrizione può eseguire **sp _ helpmergesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

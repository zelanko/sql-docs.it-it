---
title: sp_helpmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 899846e0868b6381c019281c432c014144e6354c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535333"
---
# <a name="sphelpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulle sottoscrizioni pull esistenti in un Sottoscrittore. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>Argomento  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**. Se *publication* viene **%**, vengono restituite informazioni su tutte le pubblicazioni di tipo merge e le sottoscrizioni nel database corrente.  
  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione*viene **sysname**, il valore predefinito è **%**.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del server di pubblicazione. *publisher_db*viene **sysname**, il valore predefinito è **%**.  
  
`[ @subscription_type = ] 'subscription_type'` Indica se visualizzare le sottoscrizioni pull. *subscription_type*viene **nvarchar(10)**, il valore predefinito è **'pull'**. I valori validi sono **'push'**, **'pull'**, o **'both'**.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|Nome della sottoscrizione.|  
|**publication**|**sysname**|Nome della pubblicazione.|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore.|  
|**subscription_db**|**sysname**|Nome del database di sottoscrizione.|  
|**status**|**int**|Stato della sottoscrizione:<br /><br /> **0** = sottoscrizione inattiva<br /><br /> **1** = sottoscrizione attiva<br /><br /> **2** = sottoscrizione eliminata<br /><br /> **3** = sottoscrizione scollegata<br /><br /> **4** = sottoscrizione collegata<br /><br /> **5** = sottoscrizione contrassegnata per la reinizializzazione al caricamento<br /><br /> **6** = collegamento della sottoscrizione non riuscito<br /><br /> **7** = sottoscrizione ripristinata dal backup|  
|**subscriber_type**|**int**|Tipo di Sottoscrittore:<br /><br /> **1** = Global<br /><br /> **2** = locale<br /><br /> **3** = anonima|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = Push<br /><br /> **1** = Pull<br /><br /> **2** = anonima|  
|**priority**|**float(8)**|Priorità della sottoscrizione. Il valore deve essere minore **100,00**.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione per la sottoscrizione:<br /><br /> **1** = automatica<br /><br /> **2** = non viene utilizzato uno snapshot.|  
|**description**|**nvarchar(255)**|Breve descrizione della sottoscrizione pull.|  
|**merge_jobid**|**binary(16)**|ID di processo dell'agente di merge.|  
|**enabled_for_syncmgr**|**int**|Indica se è possibile sincronizzare la sottoscrizione tramite Gestione sincronizzazione [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**last_updated**|**nvarchar(26)**|Ora in cui l'agente di merge ha eseguito l'ultima sincronizzazione della sottoscrizione.|  
|**publisher_login**|**sysname**|Nome dell'account di accesso del server di pubblicazione.|  
|**publisher_password**|**sysname**|Password del server di pubblicazione.|  
|**publisher_security_mode**|**int**|Modalità di sicurezza del server di pubblicazione:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1** = autenticazione di Windows|  
|**distributor**|**sysname**|Nome del server di distribuzione.|  
|**distributor_login**|**sysname**|Nome dell'account di accesso del server di distribuzione.|  
|**distributor_password**|**sysname**|Password per il server di distribuzione.|  
|**distributor_security_mode**|**int**|Modalità di sicurezza del server di distribuzione:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1** = autenticazione di Windows|  
|**ftp_address**|**sysname**|Disponibile per compatibilità con le versioni precedenti. Indirizzo di rete del servizio FTP per il server di distribuzione.|  
|**ftp_port**|**int**|Disponibile per compatibilità con le versioni precedenti. Numero di porta del servizio FTP per il database di distribuzione.|  
|**ftp_login**|**sysname**|Disponibile per compatibilità con le versioni precedenti. Nome utente utilizzato per la connessione al servizio FTP.|  
|**ftp_password**|**sysname**|Disponibile per compatibilità con le versioni precedenti. Password utente utilizzata per la connessione al servizio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Percorso di archiviazione della cartella snapshot, se diverso o aggiuntivo rispetto a quello predefinito.|  
|**working_directory**|**nvarchar(255)**|Percorso completo della directory in cui vengono trasferiti i file di snapshot tramite il servizio FTP, se l'opzione corrispondente è stata specificata.|  
|**use_ftp**|**bit**|Indica che la sottoscrizione viene inserita nella pubblicazione tramite Internet e che le proprietà di indirizzamento FTP sono configurate. Se **0**, sottoscrizione non utilizza il servizio FTP. Se **1**, sottoscrizione utilizza il servizio FTP.|  
|**offload_agent**|**bit**|Specifica se l'agente può essere attivato ed eseguito in remoto. Se **0**, l'agente non può essere attivato in remoto.|  
|**offload_server**|**sysname**|Nome del server utilizzato per l'attivazione remota.|  
|**use_interactive_resolver**|**int**|Specifica se durante la fase di riconciliazione viene utilizzato il sistema di risoluzione dei conflitti interattivo. Se **0**, il sistema di risoluzione interattivo non viene utilizzato.|  
|**subid**|**uniqueidentifier**|ID del Sottoscrittore.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Percorso della cartella in cui vengono salvati i file di snapshot.|  
|**last_sync_status**|**int**|Stato della sincronizzazione:<br /><br /> **1** = avvio in corso<br /><br /> **2** = ha avuto esito positivo<br /><br /> **3** = in corso<br /><br /> **4** = inattivo<br /><br /> **5** = nuovo tentativo dopo un precedente errore<br /><br /> **6** = non è riuscita<br /><br /> **7** = convalida non riuscita<br /><br /> **8** = convalida riuscita<br /><br /> **9** = richiesta di chiusura|  
|**last_sync_summary**|**sysname**|Descrizione dei risultati dell'ultima sincronizzazione.|  
|**use_web_sync**|**bit**|Specifica se la sottoscrizione può essere sincronizzata tramite HTTPS, dove il valore **1** indica che questa funzionalità è attivata.|  
|**internet_url**|**nvarchar(260)**|URL che rappresenta la posizione del listener per la replica per la sincronizzazione Web.|  
|**internet_login**|**nvarchar(128)**|Account di accesso utilizzato dall'agente di merge per la connessione al server Web che ospita la sincronizzazione Web tramite l'autenticazione di base.|  
|**internet_password**|**nvarchar(524)**|Password di accesso utilizzata dall'agente di merge per la connessione al server Web in cui viene eseguita la sincronizzazione Web tramite l'autenticazione di base.|  
|**internet_security_mode**|**int**|Modalità di autenticazione utilizzata per la connessione al server Web in cui viene eseguita la sincronizzazione Web. Un valore pari **1** significa che l'autenticazione di Windows e il valore **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**internet_timeout**|**int**|Periodo di tempo, espresso in secondi, al termine del quale una richiesta di sincronizzazione Web scade.|  
|**hostname**|**nvarchar(128)**|Specifica un valore di overload per [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) quando questa funzione viene utilizzata nella clausola WHERE di un filtro di riga con parametri.|  
|**job_login**|**nvarchar(512)**|L'account di Windows con cui viene eseguito l'agente di Merge, viene restituito nel formato *domain*\\*username*.|  
|**job_password**|**sysname**|Per motivi di sicurezza, un valore di "**\*\*\*\*\*\*\*\*\*\***" è sempre restituiti.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpmergepullsubscription** viene utilizzata nella replica di tipo merge. Nel set di risultati, la data restituita **last_updated** viene formattato come *aaaammgg fff*.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server e il **db_owner** ruolo predefinito del database possono eseguire **sp_helpmergepullsubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

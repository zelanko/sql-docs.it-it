---
title: MSsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc3e113ab9ace64cac0d41cb34bdec1c44355e48
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779773"
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsubscription_properties** tabella contiene le righe per le informazioni sui parametri necessari per eseguire gli agenti di replica nel Sottoscrittore. La tabella viene archiviata nel database di sottoscrizione nel Sottoscrittore per una sottoscrizione pull oppure nel database di distribuzione nel server di distribuzione per una sottoscrizione push.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**publication_type**|**int**|Tipo di pubblicazione:<br /><br /> **0** = transazionale.<br /><br /> **2** = unione nell'indice.|  
|**publisher_login**|**sysname**|ID dell'account di accesso utilizzato nel server di pubblicazione per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar(524**|Password (crittografata) utilizzata nel server di pubblicazione per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_security_mode**|**int**|Modalità di sicurezza implementata nel server di pubblicazione:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticazione di SQL Server.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows.<br /><br /> **2** = i trigger di sincronizzazione utilizzano un valore statico **sysservers** voce per eseguire una chiamata di procedura remota (RPC), e *server di pubblicazione* deve essere definito nel **sysservers**tabella come un server remoto o un server collegato.|  
|**server di distribuzione**|**sysname**|Nome del server di distribuzione.|  
|**distributor_login**|**sysname**|L'ID di accesso utilizzato nel server di distribuzione per l'autenticazione di SQL Server.|  
|**distributor_password**|**nvarchar(524**|Password (crittografata) utilizzata nel server di distribuzione per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_security_mode**|**int**|Modalità di sicurezza implementata nel server di distribuzione.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.<br /><br /> **1** = autenticazione di Windows.|  
|**ftp_address**|**sysname**|Indirizzo di rete del servizio File Transfer Protocol (FTP) per il server di distribuzione.|  
|**ftp_port**|**int**|Numero di porta del servizio FTP per il server di distribuzione.|  
|**ftp_login**|**sysname**|Nome utente utilizzato per la connessione al servizio FTP.|  
|**ftp_password**|**nvarchar(524**|Password per l'utente utilizzata per la connessione al servizio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|**working_directory**|**nvarchar(255)**|Nome della directory di lavoro utilizzata per archiviare i file di dati e di schema.|  
|**use_ftp**|**bit**|Specifica l'utilizzo di FTP anziché del protocollo normale per il recupero di snapshot. Se **1**, viene utilizzato il protocollo FTP.|  
|**dts_package_name**|**sysname**|Specifica il nome del pacchetto Data Transformation Services (DTS).|  
|**dts_package_password**|**nvarchar(524**|Specifica la password per il pacchetto.|  
|**dts_package_location**|**int**|Percorso di archiviazione del pacchetto DTS.|  
|**enabled_for_syncmgr**|**bit**|Specifica se è possibile sincronizzare la sottoscrizione tramite Gestione sincronizzazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> **0** = sottoscrizione non è registrata con Gestione sincronizzazione Microsoft.<br /><br /> **1** = sottoscrizione viene registrata con Gestione sincronizzazione Microsoft e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**offload_agent**|**bit**|Specifica se è possibile attivare l'agente in remoto. Se **0**, l'agente non può essere attivato in remoto.|  
|**offload_server**|**sysname**|Nome di rete del server utilizzato per l'attivazione remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Specifica il percorso della cartella in cui vengono salvati i file di snapshot.|  
|**use_web_sync**|**bit**|Specifica se è possibile sincronizzare la sottoscrizione mediante HTTP. Un valore pari **1** indica che questa funzionalità è attivata.|  
|**internet_url**|**nvarchar(260)**|URL che rappresenta il percorso del listener per la replica per la sincronizzazione tramite il Web.|  
|**internet_login**|**sysname**|L'account di accesso utilizzato dall'agente di Merge durante la connessione al server Web che ospita la sincronizzazione Web tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**internet_password**|**nvarchar(524**|La password per l'account di accesso utilizzato dall'agente di Merge durante la connessione al server Web che ospita la sincronizzazione Web tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**internet_security_mode**|**int**|La modalità di autenticazione utilizzata durante la connessione al server Web che ospita la sincronizzazione Web, dove il valore **1** significa che l'autenticazione di Windows e il valore **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticazione.|  
|**internet_timeout**|**int**|Intervallo di tempo, in secondi, prima della scadenza di una richiesta di sincronizzazione tramite il Web.|  
|**Nome host**|**sysname**|Specifica il valore per **HOST_NAME** quando questa funzione viene usata nel **in cui** clausola di un filtro join o di una relazione tra record logici.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  

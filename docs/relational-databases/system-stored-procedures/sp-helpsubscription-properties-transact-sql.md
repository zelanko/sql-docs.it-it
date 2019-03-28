---
title: sp_helpsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a39fe7efd35094330b6885094145b5340bd7f2b8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527473"
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera le informazioni di sicurezza dal [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabella. Questa stored procedure viene eseguita nel Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutti i server di pubblicazione.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del server di pubblicazione. *publisher_db* viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutti i database di pubblicazione.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutte le pubblicazioni.  
  
`[ @publication_type = ] publication_type` È il tipo di pubblicazione. *publication_type* viene **int**, con un valore predefinito è NULL. Se fornito, *publication_type* deve essere uno dei valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Pubblicazione transazionale|  
|**1**|Pubblicazione snapshot|  
|**2**|Pubblicazione di tipo merge|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**publication**|**sysname**|Nome della pubblicazione.|  
|**publication_type**|**int**|Tipo di pubblicazione:<br /><br /> **0** = transazionale<br /><br /> **1** = Snapshot<br /><br /> **2** = unione nell'indice|  
|**publisher_login**|**sysname**|ID dell'account di accesso utilizzato nel server di pubblicazione per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar(524)**|Password (crittografata) utilizzata nel server di pubblicazione per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_security_mode**|**int**|Modalità di sicurezza utilizzata nel server di pubblicazione:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1** = autenticazione di Windows|  
|**distributor**|**sysname**|Nome del server di distribuzione.|  
|**distributor_login**|**sysname**|Account di accesso per il server di distribuzione.|  
|**distributor_password**|**nvarchar(524)**|Password (crittografata) per il server di distribuzione.|  
|**distributor_security_mode**|**int**|Modalità di sicurezza utilizzata nel server di distribuzione:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1** = autenticazione di Windows|  
|**ftp_address**|**sysname**|Disponibile solo per compatibilità con le versioni precedenti. Indirizzo di rete del servizio FTP (File Transfer Protocol) per il server di distribuzione.|  
|**ftp_port**|**int**|Disponibile solo per compatibilità con le versioni precedenti. Numero di porta del servizio FTP per il server di distribuzione.|  
|**ftp_login**|**sysname**|Disponibile solo per compatibilità con le versioni precedenti. Nome utente utilizzato per la connessione al servizio FTP.|  
|**ftp_password**|**nvarchar(524)**|Disponibile solo per compatibilità con le versioni precedenti. Password utente utilizzata per la connessione al servizio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|**working_directory**|**nvarchar(255)**|Nome della directory di lavoro utilizzata per archiviare i file dei dati e di schema.|  
|**use_ftp**|**bit**|Specifica l'utilizzo di FTP anziché del protocollo normale per il recupero di snapshot. Se **1**, viene utilizzato il protocollo FTP.|  
|**dts_package_name**|**sysame**|Specifica il nome del pacchetto Data Transformation Services (DTS).|  
|**dts_package_password**|**nvarchar(524)**|Password del pacchetto, se è disponibile.|  
|**dts_package_location**|**int**|Posizione di archiviazione del pacchetto DTS.<br /><br /> **0** = il pacchetto si trova nel server di distribuzione.<br /><br /> **1** = il pacchetto si trova nel Sottoscrittore.|  
|**offload_agent**|**bit**|Specifica se l'agente può essere attivato in remoto. Se **0**, l'agente non può essere attivato in remoto.|  
|**offload_server**|**sysname**|Nome di rete del server utilizzato per l'attivazione remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Specifica il percorso della cartella in cui vengono salvati i file di snapshot.|  
|**use_web_sync**|**bit**|Specifica se la sottoscrizione può essere sincronizzata tramite HTTPS, dove il valore **1** indica che questa funzionalità è attivata.|  
|**internet_url**|**nvarchar(260)**|URL che rappresenta la posizione del listener per la replica per la sincronizzazione Web.|  
|**internet_login**|**nvarchar(128)**|Account di accesso utilizzato dall'agente di merge per la connessione al server Web che ospita la sincronizzazione Web tramite l'autenticazione di base.|  
|**internet_password**|**nvarchar(524)**|Password di accesso utilizzata dall'agente di merge per la connessione al server Web in cui viene eseguita la sincronizzazione Web tramite l'autenticazione di base.|  
|**internet_security_mode**|**int**|La modalità di autenticazione utilizzata durante la connessione al server Web che ospita la sincronizzazione Web, dove il valore **1** significa che l'autenticazione di Windows e il valore **0** significa che l'autenticazione di base.|  
|**internet_timeout**|**int**|Periodo di tempo, espresso in secondi, al termine del quale una richiesta di sincronizzazione Web scade.|  
|**hostname**|**nvarchar(128)**|Specifica il valore di HOST_NAME() se questa funzione viene utilizzata nella clausola WHERE di un filtro di riga con parametri.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpsubscription_properties** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_helpsubscription_properties**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

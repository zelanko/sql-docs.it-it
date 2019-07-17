---
title: sp_change_subscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6152e7f1c1b64cfdeafffe7d5d9eb021bfd4c4a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045785"
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna le informazioni per le sottoscrizioni pull. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del server di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @property = ] 'property'` È la proprietà da modificare. *proprietà* viene **sysname**.  
  
`[ @value = ] 'value'` È il nuovo valore della proprietà. *valore* viene **nvarchar(1000)** , non prevede alcun valore predefinito.  
  
`[ @publication_type = ] publication_type` Specifica il tipo di replica della pubblicazione. *publication_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Tipo di pubblicazione|  
|-----------|----------------------|  
|**0**|Transazionale|  
|**1**|Snapshot|  
|**2**|Merge|  
|NULL (predefinito)|Il tipo di pubblicazione è determinato dalla replica. Poiché la stored procedure deve analizzare più tabelle, questa opzione comporta un rallentamento delle prestazioni rispetto a quando viene specificato il tipo di pubblicazione esatto.|  
  
 Nella tabella seguente vengono descritte le proprietà degli articoli e i valori corrispondenti.  
  
|Proprietà|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Specifica la posizione della cartella alternativa per lo snapshot. Se il valore è NULL, i file di snapshot vengono prelevati dalla posizione predefinita specificata dal server di pubblicazione.|  
|**distrib_job_login**||Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente.|  
|**distrib_job_password**||Password dell'account di Windows utilizzato per l'esecuzione dell'agente.|  
|**distributor_login**||Account di accesso per il server di distribuzione.|  
|**distributor_password**||Password per il server di distribuzione.|  
|**distributor_security_mode**|**1**|Consente di utilizzare l'autenticazione di Windows per la connessione al server di distribuzione.|  
||**0**|Consente di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione al server di distribuzione.|  
|**dts_package_name**||Specifica il nome del pacchetto di SQL Server 2000 Data Transformation Services (DTS). Questo valore può essere specificato solo se la pubblicazione è di tipo transazionale o snapshot.|  
|**dts_package_password**||Specifica la password per il pacchetto. *dts_package_password* viene **sysname** con valore predefinito è NULL, che indica che la proprietà della password deve rimanere invariata.<br /><br /> Nota: A ogni pacchetto DTS deve essere associata una password.<br /><br /> Questo valore può essere specificato solo se la pubblicazione è di tipo transazionale o snapshot.|  
|**dts_package_location**||Posizione di archiviazione del pacchetto DTS. Questo valore può essere specificato solo se la pubblicazione è di tipo transazionale o snapshot.|  
|**dynamic_snapshot_location**||Specifica il percorso della cartella in cui vengono salvati i file di snapshot. Questo valore può essere specificato solo se la pubblicazione è di tipo merge.|  
|**ftp_address**||Disponibile solo per compatibilità con le versioni precedenti.|  
|**ftp_login**||Disponibile solo per compatibilità con le versioni precedenti.|  
|**ftp_password**||Disponibile solo per compatibilità con le versioni precedenti.|  
|**ftp_port**||Disponibile solo per compatibilità con le versioni precedenti.|  
|**hostname**||Nome host utilizzato per la connessione al server di pubblicazione.|  
|**internet_login**||Account di accesso utilizzato dall'agente di merge per la connessione al server Web che ospita la sincronizzazione Web tramite l'autenticazione di base.|  
|**internet_password**||Password utilizzata dall'agente di merge per la connessione al server Web in cui ha luogo la sincronizzazione Web mediante l'autenticazione di base.|  
|**internet_security_mode**|**1**|Consente di utilizzare l'autenticazione integrata di Windows per la sincronizzazione Web. È consigliabile utilizzare l'autenticazione di base per la sincronizzazione Web. Per altre informazioni, vedere [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Consente di utilizzare l'autenticazione di base per la sincronizzazione Web.<br /><br /> Nota: Sincronizzazione Web richiede una connessione SSL al server Web.|  
|**internet_timeout**||Periodo di tempo, espresso in secondi, al termine del quale una richiesta di sincronizzazione Web scade.|  
|**internet_url**||URL che rappresenta la posizione del listener per la replica per la sincronizzazione Web.|  
|**merge_job_login**||Account di accesso per l'account di Windows utilizzato per l'esecuzione dell'agente.|  
|**merge_job_password**||Password dell'account di Windows utilizzato per l'esecuzione dell'agente.|  
|**publisher_login**||Account di accesso per il server di pubblicazione. Modificando *publisher_login* è supportata solo per le sottoscrizioni a pubblicazioni di tipo merge.|  
|**publisher_password**||Password del server di pubblicazione. Modificando *publisher_password* è supportata solo per le sottoscrizioni a pubblicazioni di tipo merge.|  
|**publisher_security_mode**|**1**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di Windows. Modificando *publisher_security_mode* è supportata solo per le sottoscrizioni a pubblicazioni di tipo merge.|  
||**0**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**use_ftp**|**true**|Consente di utilizzare il protocollo FTP anziché il protocollo regolare per il recupero degli snapshot.|  
||**false**|Consente di utilizzare il protocollo regolare per il recupero degli snapshot.|  
|**use_web_sync**|**true**|Abilita la sincronizzazione Web.|  
||**false**|Disabilita la sincronizzazione Web.|  
|**working_directory**||Nome della directory di lavoro utilizzata per l'archiviazione temporanea dei file di dati e dello schema della pubblicazione quando per il trasferimento dei file di snapshot viene utilizzato il protocollo FTP (File Transfer Protocol).|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_change_subscription_properties** viene utilizzata in tutti i tipi di replica.  
  
 **sp_change_subscription_properties** viene usato per le sottoscrizioni pull.  
  
 Server di pubblicazione Oracle, il valore di *publisher_db* viene ignorato perché Oracle consente solo di un database per ogni istanza del server.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

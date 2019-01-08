---
title: Classe di evento Audit Add DB User | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Add DB User event class
ms.assetid: ac9ed573-c84d-444c-81fb-923a6240c1ef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36d9be6a759e2684602a20ed0c493818d5fe4cc4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775603"
---
# <a name="audit-add-db-user-event-class"></a>Audit Add DB User - classe di evento
  La classe di evento **Audit Add DB User** si verifica ogni volta che un account di accesso viene aggiunto o rimosso come utente database in un database. Questa classe di evento viene usata per le stored procedure **sp_grantdbaccess**, **sp_revokedbaccess**, **sp_adduser**e **sp_dropuser** .  
  
 Questa classe di evento verrà probabilmente rimossa in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile usare invece la classe di evento **Audit Database Principal Management** .  
  
## <a name="audit-add-db-user-event-class-data-columns"></a>Colonne di dati della classe di evento Audit Add DB User  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|**ColumnPermissions**|**int**|Indicatore dell'impostazione o meno di un'autorizzazione per la colonna. Analizzare il testo dell'istruzione per determinare con esattezza quali autorizzazioni sono state impostate per quali colonne.|44|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|**nvarchar**|Nome del database cui il nome utente viene aggiunto o dal quale viene rimosso.|35|Yes|  
|**DBUserName**|**nvarchar**|Nome dell'utente che ha eseguito l'istruzione nel database.|40|Yes|  
|**EventClass**|**int**|Tipo di evento = 109.|27|No|  
|**EventSequence**|**int**|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|**EventSubClass**|**int**|Tipo di sottoclasse di evento.<br /><br /> 1=Aggiungi<br /><br /> 2=Elimina<br /><br /> 3=Concedi accesso al database<br /><br /> 4=Revoca accesso al database|21|Yes|  
|**HostName**|**nvarchar**|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|**nvarchar**|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome utente di Windows.|6|Yes|  
|**OwnerName**|**nvarchar**|Nome utente del database per il proprietario dell'oggetto.|37|Yes|  
|**RequestID**|**int**|ID della richiesta contenente l'istruzione.|49|Yes|  
|**RoleName**|**nvarchar**|Nome del ruolo del database la cui appartenenza verrà modificata (se viene usato **sp_adduser**).|38|Yes|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26||  
|**SessionLoginName**|**Nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**Esito positivo**|**int**|1 = esito positivo. 0 = esito negativo. Ad esempio, il valore 1 indica che il controllo delle autorizzazioni ha avuto esito positivo e il valore 0 che il controllo ha avuto esito negativo.|23|Yes|  
|**TargetLoginName**|**nvarchar**|Nome dell'account di accesso il cui accesso al database viene modificato.|42|Yes|  
|**TargetLoginSid**|**image**|Per le azioni relative a un account di accesso (ad esempio l'aggiunta di un nuovo account di accesso), l'ID di sicurezza (SID) dell'account di accesso specifico.|43|Yes|  
|**TargetUserName**|**nvarchar**|Nome dell'utente database da aggiungere.|39|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
|**XactSequence**|**bigint**|Token usato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql)   
 [sp_adduser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adduser-transact-sql)   
 [sp_dropuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropuser-transact-sql)   
 [Classe di evento Audit Database Principal Management](audit-database-principal-management-event-class.md)  
  
  

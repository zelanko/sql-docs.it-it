---
title: 'TM: Eseguire il commit Tran Completed-classe di evento | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'TM: Commit Tran Completed event class'
ms.assetid: c102de15-f312-42a7-b52a-fc4879cc43aa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 224bfd47c31c94e19935a97c6ed1cc726e233bb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061301"
---
# <a name="tm-commit-tran-completed-event-class"></a>TM: Commit Tran Completed - classe di evento
  TM: Eseguire il commit Tran Completed-classe di evento indica che una richiesta COMMIT TRANSACTION è stata completata. La richiesta è stata inviata dal client tramite l'interfaccia di gestione delle transazioni. La colonna EventSubClass indica se, in seguito al commit della transazione corrente, verrà avviata una nuova transazione.  
  
## <a name="tm-commit-tran-completed-event-class-data-columns"></a>TM: Eseguire il commit Tran completato colonne di dati di classe di evento  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Yes|  
|----------------------|---------------|-----------------|---------------|---------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE database oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE database. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|Errore|`int`|Numero di errore di un evento specifico. Corrisponde spesso al numero di errore archiviato nella vista del catalogo sys.messages.|31|Yes|  
|EventClass|`int`|Tipo di evento = 186.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|EventSubClass|`int`|Tipo di sottoclasse di evento.<br /><br /> 1=Commit<br /><br /> 2=Commit e inizio|21|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|Riuscito|`int`|1 = esito positivo. 0 = esito negativo (ad esempio, 1 indica l'esito positivo di un controllo delle autorizzazioni e 0 indica l'esito negativo di tale controllo).|23|Yes|  
|TextData|`ntext`|Valore di testo che dipende dalla classe di evento acquisita nella traccia.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

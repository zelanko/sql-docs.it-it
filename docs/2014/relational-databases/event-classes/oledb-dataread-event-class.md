---
title: Classe di evento OLEDB DataRead | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB DataRead event class
ms.assetid: fb6869ba-3199-4e32-a650-60a5dda2571e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d12bf6f0e002b1f06bc96ff97608f88bd305b34b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960806"
---
# <a name="oledb-dataread-event-class"></a>OLEDB DataRead - classe di evento
  La classe di evento OLEDB DataRead viene generata quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chiama un provider OLE DB per query distribuite e stored procedure remote. Includere questa classe di evento nelle tracce che eseguono il monitoraggio quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue una chiamata per una richiesta di dati al provider OLE DB.  
  
 Quando la classe OLEDB DataRead viene inclusa in una traccia, l'overhead generato sarà elevato. È consigliabile limitare l'utilizzo di questa classe di evento alle tracce che eseguono il monitoraggio di problemi specifici per brevi periodi di tempo.  
  
## <a name="oledb-dataread-event-class-data-columns"></a>Colonne di dati della classe di evento OLEDB DataRead  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|Duration|`bigint`|Periodo di tempo necessario per completare l'evento OLE DB Call.|13|No|  
|EndTime|`datetime`|Ora di fine dell'evento.|15|Yes|  
|Errore|`int`|Numero di errore di un evento specifico. Corrisponde spesso al numero di errore archiviato nella vista del catalogo sys.messages.|31|Yes|  
|EventClass|`int`|Tipo di evento = 121.|27|No|  
|EventSequence|`int`|Sequenza della classe di evento OLE DB nel batch.|51|No|  
|EventSubClass|`int`|Tipo di sottoclasse di evento.<br /><br /> 0=Avvio in corso<br /><br /> 1=Completato|21|no|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LinkedServerName|`nvarchar`|Nome del server collegato.|45|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|MethodName|`nvarchar`|Nome del metodo chiamante.|47|No|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ProviderName|`nvarchar`|Nome del provider OLE DB.|46|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`Int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`nvarchar`|Parametri inviati e ricevuti nella chiamata OLE DB.|1|no|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Oggetti di automazione OLE in Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  

---
title: Classe di evento OLEDB QueryInterface | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4d02437d6faeb00b55771f7ef13725a23b3a1f92
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029046"
---
# <a name="oledb-queryinterface-event-class"></a>OLEDB QueryInterface - classe di evento
  La classe di evento **OLEDB QueryInterface** viene generata quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue una chiamata OLE DB **QueryInterface** per query distribuite e stored procedure remote. Includere questa classe di evento nelle tracce che eseguono il monitoraggio dei problemi associati a query distribuite e stored procedure remote.  
  
 Se si include la classe di evento **OLEDB QueryInterface** , l'overhead sarà elevato. Se tali eventi si verificano di frequente, la traccia potrebbe ridurre in modo significativo le prestazioni. Per ridurre al minimo l'overhead generato, limitare l'utilizzo di questa classe di evento alle tracce che eseguono il monitoraggio di problemi specifici per brevi periodi di tempo.  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>Colonne di dati della classe di evento OLEDB QueryInterface  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Sì|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE *database* oppure il database predefinito se non è stata eseguita alcuna istruzione USE *database* per una determinata istanza. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Sì|  
|Duration|`bigint`|Periodo di tempo necessario per completare l'evento OLE DB QueryInterface.|13|No|  
|EndTime|`datetime`|Ora di fine dell'evento.|15|Sì|  
|Errore|`int`|Numero di errore di un evento specifico. Corrisponde spesso al numero di errore archiviato nella vista del catalogo **sys.messages** .|31|Sì|  
|EventClass|`int`|Tipo di evento = 120.|27|No|  
|EventSequence|`int`|Sequenza della classe di evento OLE DB nel batch.|51|No|  
|EventSubClass|`int`|0=Avvio in corso<br /><br /> 1=Completato|21|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Sì|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Sì|  
|LinkedServerName|`nvarchar`|Nome del server collegato.|45|Sì|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Sì|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|MethodName|`nvarchar`|Nome del metodo chiamante.|47|No|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Sì|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Sì|  
|ProviderName|`nvarchar`|Nome del provider OLE DB.|46|Sì|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Sì|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se, ad esempio, si esegue la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, in `SessionLoginName` viene visualizzato Login1 e in `LoginName` viene visualizzato Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|TextData|`nvarchar`|Parametri inviati e ricevuti nella chiamata OLE DB.|1|No|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Oggetti di automazione OLE in Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  

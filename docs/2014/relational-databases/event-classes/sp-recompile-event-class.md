---
title: Classe di evento SP:Recompile | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9d894eb3f38248e1f7af2b1f693f87bdfebefa9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795672"
---
# <a name="sprecompile-event-class"></a>SP:Recompile - classe di evento
  La classe di evento SP:Recompile indica che una stored procedure, una funzione definita dall'utente o un trigger è stato ricompilato. Le ricompilazioni segnalate da questa classe di evento si verificano a livello di istruzione.  
  
 La strategia ottimale per tracciare ricompilazioni a livello di istruzione consiste nell'usare la classe di evento SQL:StmtRecompile. La classe di evento SP:Recompile è deprecata. Per altre informazioni, vedere [Classe di evento SQL:StmtRecompile](sql-stmtrecompile-event-class.md).  
  
## <a name="sprecompile-event-class-data-columns"></a>Colonne di dati della classe di evento SP:Recompile  
  
|Nome colonna di dati|`Data type`|Descrizione|ID colonna|Filtrabile|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se il client fornisce l'ID del processo.|9|Yes|  
|DatabaseID|`int`|ID del database nel quale viene eseguita la stored procedure. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita la stored procedure.|35|Yes|  
|EventClass|`int`|Tipo di evento = 37.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|EventSubClass|`int`|Tipo di sottoclasse di evento. Indica il motivo della ricompilazione.<br /><br /> 1 = Schema modificato<br /><br /> 2 = Statistiche modificate<br /><br /> 3 = DNR ricompilazione<br /><br /> 4 = Opzione impostata modificata<br /><br /> 5 = Tabella temporanea modificata<br /><br /> 6 = Set di righe remoto modificato<br /><br /> 7 = Autorizzazioni FOR BROWSE modificate<br /><br /> 8 = Ambiente di notifica query modificato<br /><br /> 9 = Vista MPI modificata<br /><br /> 10 = Opzioni cursore modificate<br /><br /> 11 = Con opzione di ricompilazione|21|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IntegerData2|`int`|Offset finale dell'istruzione nella stored procedure o nel batch che ha provocato la ricompilazione. L'offset finale è -1 se l'istruzione rappresenta l'ultima istruzione nel batch.|55|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NestLevel|`int`|Livello di nidificazione della stored procedure.|29|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID della stored procedure assegnato dal sistema.|22|Yes|  
|ObjectName|`nvarchar`|Nome dell'oggetto che ha attivato la ricompilazione.|34|Yes|  
|ObjectType|`int`|Valore che rappresenta il tipo di oggetto coinvolto nell'evento. Per altre informazioni, vedere [Colonna ObjectType per gli eventi di traccia](objecttype-trace-event-column.md).|28|Yes|  
|Offset|`int`|Offset iniziale dell'istruzione nella stored procedure o nel batch che ha provocato la ricompilazione.|61|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|SqlHandle|`varbinary`|Hash a 64 bit basato sul testo di una query ad hoc oppure ID del database e dell'oggetto di un oggetto SQL. È possibile passare questo valore a sys.dm_exec_sql_text per recuperare il testo SQL associato.|63|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Testo dell'istruzione Transact-SQL che ha provocato una ricompilazione a livello di istruzione.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token usato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Classe di evento SQL:StmtRecompile](sql-stmtrecompile-event-class.md)  
  
  

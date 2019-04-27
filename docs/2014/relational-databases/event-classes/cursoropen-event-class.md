---
title: Classe di evento CursorOpen | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- CursorOpen event class
ms.assetid: d39262c0-0035-42fc-b989-7a16ae0c7345
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9cdb7fbddd53eb9e2dfbc36d7a86b6bac2619bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62663454"
---
# <a name="cursoropen-event-class"></a>CursorOpen - classe di evento
  La classe di evento **CursorOpen** descrive gli eventi di apertura di cursore che si verificano nei cursori API. Gli eventi di apertura di cursore si verificano quando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] definisce l'istruzione SQL da associare al cursore e le opzioni di cursore e quindi popola il cursore.  
  
 Includere la classe di evento **CursorOpen** nelle tracce che registrano le prestazioni dei cursori. Quando si include in una traccia la classe di evento **CursorOpen** , l'overhead generato dipende dalla frequenza di utilizzo dei cursori nel database durante l'esecuzione della traccia. Se si utilizzano diffusamente i cursori, l'esecuzione della traccia potrebbe ridurre in modo significativo le prestazioni.  
  
## <a name="cursoropen-event-class-data-columns"></a>Colonne di dati della classe di evento CursorOpen  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|**nvarchar**|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|**EventClass**|**int**|Tipo di evento registrato = 53.|27|no|  
|**EventSequence**|**int**|Sequenza della classe di evento **CursorOpen** nel batch.|51|no|  
|**GroupID**|**int**|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|**Handle**|**int**|Valore intero, utilizzato da ODBC, OLE DB o DB-Library per il coordinamento dell'esecuzione con il server.|33|Yes|  
|**HostName**|**nvarchar**|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|**int**|Tipo di cursore. I valori possibili sono:<br /><br /> 1 = Keyset<br /><br /> 2 = Dinamico<br /><br /> 4 = Forward-only<br /><br /> 8 = Statico<br /><br /> 16 = Fast forward|25|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|**nvarchar**|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome utente di Windows.|6|Yes|  
|**RequestID**|**int**|Identificatore della richiesta che ha aperto il cursore.|49|Yes|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
|**XactSequence**|**bigint**|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Cursori](../cursors.md)  
  
  

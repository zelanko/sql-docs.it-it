---
title: Classe di evento CursorImplicitConversion | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- CursorImplicitConversion event class
ms.assetid: 44d12e23-146a-42e6-bb38-1f2f6a035bad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: efc615e9aa873a322ef9a31b2c293e6c5c4793da
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795053"
---
# <a name="cursorimplicitconversion-event-class"></a>CursorImplicitConversion - classe di evento
  La classe di evento **CursorImplicitConversion** descrive gli eventi di conversione implicita dei cursori generati nelle API o nei cursori [!INCLUDE[tsql](../../includes/tsql-md.md)] . Gli eventi di conversione implicita dei cursori vengono generati quando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] esegue un'istruzione Transact-SQL non supportata dai cursori del server del tipo richiesto. [!INCLUDE[ssDE](../../includes/ssde-md.md)] restituisce un errore indicante che il tipo di cursore è stato modificato.  
  
 Includere la classe di evento **CursorImplicitConversion** nelle tracce in cui vengono registrate le prestazioni dei cursori.  
  
 Quando questa classe di evento viene inclusa in una traccia, la quantità di overhead dipende dalla frequenza di utilizzo dei cursori che richiedono la conversione implicita nel database durante la traccia. Se si utilizzano diffusamente i cursori, l'esecuzione della traccia potrebbe ridurre in modo significativo le prestazioni.  
  
## <a name="cursorimplicitconversion-event-class-data-columns"></a>Colonne di dati della classe di evento CursorImplicitConversion  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**BinaryData**|**image**|Tipo di cursore risultante. I valori possibili sono:<br /><br /> 1 = Keyset<br /><br /> 2 = Dinamico<br /><br /> 4 = Forward-only<br /><br /> 8 = Statico<br /><br /> 16 = Fast forward|2|Yes|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|**nvarchar**|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|**EventClass**|**int**|Tipo di evento registrato = 76.|27|No|  
|**EventSequence**|**int**|Sequenza della classe di evento **CursorClose** nel batch.|51|No|  
|**GroupID**|**int**|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|**Handle**|**int**|Handle dell'oggetto a cui si fa riferimento nell'evento.|33|Yes|  
|**HostName**|**nvarchar**|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|**int**|Tipo di cursore richiesto. I valori possibili sono:<br /><br /> 1 = Keyset<br /><br /> 2 = Dinamico<br /><br /> 4 = Forward-only<br /><br /> 8 = Statico<br /><br /> 16 = Fast forward|25|No|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|**nvarchar**|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome utente di Windows.|6|Yes|  
|**RequestID**|**int**|Identificatore della richiesta di conversione implicita.|49|Yes|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
|**XactSequence**|**bigint**|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

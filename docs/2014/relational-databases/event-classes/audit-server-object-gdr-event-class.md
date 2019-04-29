---
title: Classe di evento Audit Server Object GDR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Server Object GDR event class
ms.assetid: 117fedca-c1c4-469a-929a-9ea332c83d25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2a08a594694e9aac30620837f2a324da5a4d6fe4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012521"
---
# <a name="audit-server-object-gdr-event-class"></a>Audit Server Object GDR - classe di evento
  La classe di evento **Audit Server Object GDR** si verifica ogni volta che viene generata un'istruzione GRANT, REVOKE o DENY per l'autorizzazione di un oggetto server da parte di qualsiasi utente di Microsoft SQL Server.  
  
## <a name="audit-server-object-gdr-event-class-data-columns"></a>Colonne di dati della classe di evento Audit Server Object GDR  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|**nvarchar**|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del client.|40|Yes|  
|**EventClass**|**int**|Tipo di evento=171|27|No|  
|**EventSequence**|**int**|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|**EventSubClass**|**int**|Tipo di sottoclasse di evento.<br /><br /> 1=Concedi<br /><br /> 2=Revoca<br /><br /> 3=Nega|21|Yes|  
|**HostName**|**nvarchar**|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|**nvarchar**|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome utente di Windows.|6|Yes|  
|**ObjectName**|**nvarchar**|Nome dell'oggetto a cui si fa riferimento.|34|Yes|  
|**ObjectType**|**int**|Valore che rappresenta il tipo di oggetto coinvolto nell'evento. Questo valore corrisponde alla colonna type nella vista del catalogo **sys.objects** . Per i valori, vedere [Colonna ObjectType per gli eventi di traccia](objecttype-trace-event-column.md).|28|Yes|  
|**OwnerName**|**nvarchar**|Nome utente del database per il proprietario dell'oggetto.|37|Yes|  
|**Autorizzazioni**|**bigint**|Valore intero che rappresenta il tipo di autorizzazioni controllato.<br /><br /> 1 = SELECT ALL<br /><br /> 2 = UPDATE ALL<br /><br /> 4 = REFERENCES ALL<br /><br /> 8 = INSERT<br /><br /> 16 = DELETE<br /><br /> 32 = EXECUTE (solo procedure)<br /><br /> 4096 = SELECT ANY (almeno una colonna)<br /><br /> 8192 = UPDATE ANY|19|Yes|  
|**RequestID**|**int**|ID della richiesta contenente l'istruzione.|49|Yes|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**Esito positivo**|**int**|1 = esito positivo. 0 = esito negativo. Ad esempio, il valore 1 indica che il controllo delle autorizzazioni ha avuto esito positivo e il valore 0 che il controllo ha avuto esito negativo.|23|Yes|  
|**TargetLoginName**|**nvarchar**|Per le azioni relative a un account di accesso (ad esempio l'aggiunta di un nuovo account di accesso), il nome dell'account di accesso specifico.|42|Yes|  
|**TargetLoginSid**|**image**|Per le azioni relative a un account di accesso (ad esempio l'aggiunta di un nuovo account di accesso), l'ID di sicurezza (SID) dell'account di accesso specifico.|43|Yes|  
|**TextData**|**ntext**|Valore di testo che dipende dalla classe di evento acquisita nella traccia.|1|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
|**XactSequence**|**bigint**|Token usato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)  
  
  

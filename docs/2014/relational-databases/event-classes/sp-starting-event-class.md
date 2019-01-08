---
title: Classe di evento SP:Starting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:Starting event class
ms.assetid: ef55e579-080d-4650-a7fc-4dd03ed8e391
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaa44fe3a5b6e7009057f351d06258b5ab809aa5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801283"
---
# <a name="spstarting-event-class"></a>SP:Starting - classe di evento
  La classe di evento SP:Starting indica l'avvio dell'esecuzione di una stored procedure.  
  
## <a name="spstarting-event-class-data-columns"></a>Colonne di dati della classe di evento SP:Starting  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database nel quale viene eseguita la stored procedure. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita la stored procedure.|35|Yes|  
|EventClass|`int`|Tipo di evento = 42.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LineNumber|`int`|Viene visualizzato il numero di riga dell'istruzione di esecuzione tramite cui è stata chiamata la stored procedure.|5|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NestLevel|`int`|Livello di nidificazione della stored procedure.|29|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID della stored procedure assegnato dal sistema.|22|Yes|  
|ObjectName|`nvarchar`|Nome della stored procedure avviata.|34|Yes|  
|ObjectType|`int`|Tipo di stored procedure avviata. Questo valore corrisponde alla colonna type nella vista del catalogo sys.objects. Per i valori, vedere [Colonna ObjectType per gli eventi di traccia](objecttype-trace-event-column.md).|28|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SourceDatabaseID|`int`|ID del database che contiene l'oggetto.|62|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Testo della chiamata di procedura.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

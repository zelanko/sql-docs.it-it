---
title: Classe di evento Showplan XML Statistics Profile | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan XML Statistics Profile event class
ms.assetid: 77e8ca69-d98a-4acd-9d6a-f825bf079d84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ea60aef999f871f28e21839ce0d7808aad0727b4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356119"
---
# <a name="showplan-xml-statistics-profile-event-class"></a>Showplan XML Statistics Profile - classe di evento
  La classe di evento Showplan XML Statistics Profile viene generata quando in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguita un'istruzione SQL. Tale classe di evento consente di identificare gli operatori Showplan in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La classe di evento Showplan XML Statistics Profile visualizza informazioni complete sulla fase di compilazione e pertanto è possibile che per le tracce che la contengono si verifichi un overhead di prestazioni significativo. Per ridurre al minimo l'overhead generato, limitare l'utilizzo di questa classe di evento alle tracce che eseguono il monitoraggio di problemi specifici per brevi periodi di tempo.  
  
 Ai documenti creati tramite Showplan XML è associato uno schema. È possibile trovare questo schema nel [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkId=41740)o come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="showplan-xml-statistics-profile-event-class-data-columns"></a>Colonne di dati della classe di evento Showplan XML Statistics Profile  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|BinaryData|`image`|Costo stimato della query.|2|No|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|Event Class|`int`|Tipo di evento = 146.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IntegerData|`int`|Numero stimato di righe restituite.|25|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LineNumber|`int`|Visualizza il numero della riga contenente l'errore.|5|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSID|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|No|  
|NestLevel|`int`|Valore intero che rappresenta i dati restituiti da @@NESTLEVEL.|29|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|ObjectID|`int`|ID dell'oggetto assegnato dal sistema.|22|Yes|  
|ObjectName|`nvarchar`|Nome dell'oggetto a cui si fa riferimento.|34|Yes|  
|ObjectType|`int`|Valore che rappresenta il tipo di oggetto coinvolto nell'evento. Questo valore corrisponde alla colonna type nella vista del catalogo sys.objects. Per i valori, vedere [Colonna ObjectType per gli eventi di traccia](objecttype-trace-event-column.md).|28|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna vengono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Valore di testo che dipende dalla classe di evento acquisita nella traccia.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token usato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Guida di riferimento a operatori Showplan logici e fisici](../showplan-logical-and-physical-operators-reference.md)  
  
  

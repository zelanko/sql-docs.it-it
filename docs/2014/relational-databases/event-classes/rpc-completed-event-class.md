---
title: Classe di evento RPC:Completed | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- RPC:Completed event class
ms.assetid: 0d526201-94c9-4e4c-afb1-4213df1815ba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c4b427047aeba970ad65a6bd2ac31a219978ea71
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775783"
---
# <a name="rpccompleted-event-class"></a>RPC:Completed - classe di evento
  La classe di evento RPC:Completed indica il completamento di una chiamata di procedura remota.  
  
## <a name="rpccompleted-event-class-data-columns"></a>Colonne di dati della classe di evento RPC:Completed  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|BinaryData|`image`|Valore binario che dipende dalla classe di evento acquisita nella traccia.|2|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|CPU|`int`|Quantità di tempo della CPU usata dall'evento. In microsecondi a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. In millisecondi nelle versioni precedenti.|18|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|Duration|`bigint`|Quantità di tempo richiesta dall'evento. In microsecondi a partire da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. In millisecondi nelle versioni precedenti.|13|Yes|  
|EndTime|`datetime`|Ora di fine della chiamata di procedura remota.|15|Yes|  
|Errore|`int`|Numero di errore di un evento specifico.<br /><br /> 0=OK<br /><br /> 1=Errore<br /><br /> 2=Interrompi<br /><br /> 3 = Ignorato|31|Yes|  
|EventClass|`int`|Tipo di evento = 10.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectName|`nvarchar`|Nome dell'oggetto a cui si fa riferimento.|34|Yes|  
|Reads|`bigint`|Numero di letture di pagine eseguite dalla chiamata di procedura remota.|16|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|RowCounts|`bigint`|Numero di righe del batch della chiamata di procedura remota.|48|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26||  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Testo della chiamata di procedura remota.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|Writes|`bigint`|Numero di scritture di pagine eseguite dalla chiamata di procedura remota.|17|Yes|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

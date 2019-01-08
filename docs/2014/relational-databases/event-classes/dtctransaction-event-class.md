---
title: Classe di evento DTCTransaction | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- DTCTransaction event class
ms.assetid: 9a2d358e-5b8f-4d0b-8b93-6705c009ad57
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26da2a16462b9853489c6430a6c80e1ab2a6f3b8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770633"
---
# <a name="dtctransaction-event-class"></a>DTCTransaction - classe di evento
  Usare la classe di evento **DTCTransaction** per monitorare lo stato delle transazioni di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] coordinate con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (DTC). Sono incluse le transazioni che interessano due o più database nella stessa istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]e le transazioni distribuite che interessano due o più istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="dtctransaction-event-class-data-columns"></a>Colonne di dati della classe di evento DTCTransaction  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**BinaryData**|`image`|Rappresentazione binaria dell'ID dell'unità di lavoro (UOW) che identifica univocamente la transazione all'interno di DTC.|2|Yes|  
|**ClientProcessID**|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|`int`|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|**EventClass**|`int`|Tipo di evento = 19.|27|No|  
|**EventSequence**|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|**EventSubClass**|`int`|Tipo di sottoclasse di evento.<br /><br /> 0=Recupero indirizzo<br /><br /> 1=Propagazione transazione<br /><br /> 3=Chiusura connessione<br /><br /> 6=Creazione di una nuova transazione DTC<br /><br /> 7=Integrazione in una transazione DTC<br /><br /> 9=Commit interno<br /><br /> 10=Interruzione interna<br /><br /> 14=Preparazione transazione<br /><br /> 15=Transazione preparata<br /><br /> 16=Chiusura transazione in corso<br /><br /> 17=Commit transazione in corso<br /><br /> 22=Errore del gestore delle transazioni nello stato PREPARED<br /><br /> 23=Sconosciuta|21|Yes|  
|**GroupID**|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|**HostName**|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|`int`|Livello di isolamento della transazione.|25|Yes|  
|**IsSystem**|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|`nvarchar`|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|`nvarchar`|Nome utente di Windows.|6|Yes|  
|**RequestID**|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|**ServerName**|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SessionLoginName**|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TextData**|`ntext`|Rappresentazione testuale della UOW che identifica univocamente la transazione all'interno di DTC.|1|Yes|  
|**TransactionID**|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|**XactSequence**|`bigint`|Token usato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

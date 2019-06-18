---
title: Classe di evento Hash Warning | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc2b6d2ba25ee487053a7f9f711c499356a5ec59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662345"
---
# <a name="hash-warning-event-class"></a>Hash Warning - classe di evento
  È possibile utilizzare la classe di evento Hash Warning per monitorare il momento in cui si verifica una ricorsione di hash o l'interruzione dell'hashing (hash bailout) durante un'operazione di hashing.  
  
 La ricorsione di hash si verifica quando la memoria disponibile non è sufficiente per l'input di compilazione, che viene quindi suddiviso in più partizioni elaborate separatamente. Se la memoria disponibile non è sufficiente per una delle partizioni, la partizione viene suddivisa ulteriormente in sottopartizioni che vengono elaborate separatamente. Il processo di suddivisione continua fino a quando non vengono inserite nella memoria disponibile tutte le partizioni o non viene raggiunto il livello massimo di ricorsione (visualizzato nella colonna di dati IntegerData).  
  
 L'evento hash bailout si verifica quando un'operazione di hashing raggiunge il livello massimo di ricorsione e ricorre a un piano alternativo per l'elaborazione dei dati partizionati rimanenti. È in genere causato da dati asimmetrici.  
  
 Ricorsione di hash e hash bailout provocano una riduzione delle prestazioni del server. Per eliminare ricorsioni di hash e hash bailout o ridurne la frequenza, eseguire una delle operazioni seguenti:  
  
-   Verificare che siano disponibili statistiche per le colonne da unire in join o raggruppare.  
  
-   Se esistono statistiche per le colonne, aggiornarle.  
  
-   Utilizzare un tipo di join diverso. Ad esempio, utilizzare un join MERGE o LOOP, se appropriato.  
  
-   Aumentare la memoria disponibile nel computer. Ricorsione di hash e hash bailout si verificano quando non è disponibile memoria sufficiente per l'elaborazione delle query e si rende necessaria la scrittura su disco.  
  
 La creazione o l'aggiornamento delle statistiche per le colonne interessate dall'operazione di join è la procedura più efficace per ridurre il numero di ricorsioni di hash e hash bailout.  
  
> [!NOTE]  
>  Per descrivere l'hash bailout vengono usati anche i termini *grace hash join* e *hash join ricorsivo* .  
  
> [!IMPORTANT]  
>  Per determinare la posizione in cui si verifica l'evento Hash Warning quando Query Optimizer genera un piano di esecuzione, è inoltre consigliabile acquisire una classe di evento Showplan nella traccia. È possibile scegliere qualsiasi classe di evento Showplan ad eccezione delle classi Showplan Text e Showplan Text (Unencoded) che non restituiscono alcun ID nodo. Nelle classi Showplan gli ID nodo identificano ogni operazione eseguita da Query Optimizer quando genera un piano di esecuzione della query. Queste operazioni sono denominate *operatori*e a ogni operatore presente in una classe Showplan è associato un ID nodo. La colonna ObjectID relativa agli eventi Hash Warning corrisponde così all'ID nodo nelle classi Showplan, in modo che sia possibile determinare l'operatore o l'operazione che sta provocando l'errore.  
  
## <a name="hash-warning-event-class-data-columns"></a>Colonne di dati della classe di evento Hash Warning  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione anziché con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se il client fornisce l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|EventClass|`int`|Tipo di evento = 55.|27|no|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|EventSubClass|`int`|Tipo di sottoclasse di evento.<br /><br /> 0=Ricorsione<br /><br /> 1=Bailout|21|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IntegerData|`int`|Livello di ricorsione (solo ricorsione di hash).|25|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di sicurezza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di Windows nel formato *\<DOMINIO>\\<nomeutente\>* ).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID del nodo radice del gruppo di hash coinvolto nella ripartizione, Corrisponde al nodo di ID nelle classi di evento Showplan.|22|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26||  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

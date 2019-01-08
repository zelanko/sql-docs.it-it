---
title: Classe di evento Lock:Escalation | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Escalation event class
- lock escalation [SQL Server], event class
ms.assetid: d253b44c-7600-4afa-a3a7-03cc937c6a4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c85b6983cbff901ae39c365503a6ab1ae0fcede1
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980177"
---
# <a name="lockescalation-event-class"></a>Classe di evento Lock:Escalation
  La classe di evento **Lock:Escalation** indica che un blocco con granularità fine è stato convertito in un blocco con granularità grossolana, ad esempio un blocco di riga è stato convertito in blocco di oggetto. La classe di evento dell'escalation è l'ID evento 60.  
  
## <a name="lockescalation-event-class-data-columns"></a>Colonne di dati della classe di evento Lock:Escalation  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|`int`|ID del database in cui è stato acquisito il blocco. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|`nvarchar`|Nome del database in cui si è verificata l'escalation.|35|Yes|  
|**EventClass**|`int`|Tipo di evento = 60.|27|No|  
|**EventSubClass**|`int`|Causa dell'escalation dei blocchi:<br /><br /> **0 - LOCK_THRESHOLD** indica che l'istruzione supera la soglia del blocco.<br /><br /> **1 - MEMORY_THRESHOLD** indica che l'istruzione supera la soglia di memoria.|21|Yes|  
|**EventSequence**|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|**GroupID**|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|**HostName**|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|`int`|Conteggio dei blocchi HoBT. Numero di blocchi HoBT al momento dell'escalation dei blocchi.|25|Yes|  
|**IntegerData2**|`int`|Conteggio dei blocchi alzati di livello. Numero totale di blocchi convertiti. Queste strutture di blocco vengono deallocate poiché già coperte dal blocco alzato di livello.|55|Yes|  
|**IsSystem**|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LineNumber**|`int`|Numero di riga dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] .|5|Yes|  
|**LoginName**|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**Mode**|`int`|Modalità di blocco risultante dopo l'escalation:<br /><br /> 0=NULL - Compatibile con tutte le altre modalità di blocco (LCK_M_NL)<br /><br /> 1=Blocco di stabilità dello schema (LCK_M_SCH_S)<br /><br /> 1=Blocco di modifica dello schema (LCK_M_SCH_M)<br /><br /> 3=Blocco condiviso (LCK_M_S)<br /><br /> 4=Blocco di aggiornamento (LCK_M_U)<br /><br /> 5=Blocco esclusivo (LCK_M_X)<br /><br /> 6=Blocco condiviso preventivo (LCK_M_IS)<br /><br /> 7=Blocco di aggiornamento preventivo (LCK_M_IU)<br /><br /> 8=Blocco esclusivo preventivo (LCK_M_IX)<br /><br /> 9=Condiviso-Preventivo-Aggiornamento (LCK_M_SIU)<br /><br /> 10=Condiviso-Preventivo-Esclusivo (LCK_M_SIX)<br /><br /> 10=Aggiornamento-Preventivo-Esclusivo (LCK_M_SIX)<br /><br /> 12=Blocco aggiornamenti bulk (LCK_M_BU)<br /><br /> 13=Intervalli di chiavi-Condiviso/Condiviso (LCK_M_RS_S)<br /><br /> 14=Intervalli di chiavi-Condiviso/Aggiornamento (LCK_M_RS_U)<br /><br /> 15=Intervalli di chiavi-Inserimento-NULL (LCK_M_RI_NL)<br /><br /> 16=Intervalli di chiavi-Inserimento-Condiviso (LCK_M_RI_S)<br /><br /> 17=Intervalli di chiavi-Inserimento-Aggiornamento (LCK_M_RI_U)<br /><br /> 18=Intervalli di chiavi-Inserimento-Esclusivo (LCK_M_RI_X)<br /><br /> 19=Intervalli di chiavi-Esclusivo-Condiviso (LCK_M_RX_S)<br /><br /> 20=Intervalli di chiavi-Esclusivo-Aggiornamento (LCK_M_RX_U)<br /><br /> 21=Intervalli di chiavi-Esclusivo-Esclusivo (LCK_M_RX_X)|32|Yes|  
|**NTDomainName**|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**NTUserName**|`nvarchar`|Nome utente di Windows.|6|Yes|  
|**ObjectID**|`int`|ID assegnato dal sistema della tabella per la quale è stata generata l'escalation dei blocchi.|22|Yes|  
|**ObjectID2**|`bigint`|ID dell'entità o dell'oggetto correlato. (ID HoBT per il quale è stata generata l'escalation dei blocchi).|56|Yes|  
|**Offset**|`int`|Offset iniziale dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] .|61|Yes|  
|**OwnerID**|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE<br /><br /> 6=WAITFOR_QUERY|58|Yes|  
|**RequestID**|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|**ServerName**|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SessionLoginName**|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TextData**|`ntext`|Testo dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che provoca l'escalation dei blocchi.|1|Yes|  
|**TransactionID**|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|**Tipo**|`int`|Granularità dell'escalation dei blocchi:<br /><br /> 1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT (livello della tabella)<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=HOBT<br /><br /> 13=ALLOCATION_UNIT|57|Yes|  
  
## <a name="examples"></a>Esempi  
 Nel seguente esempio viene utilizzata la procedura `sp_trace_create` per creare una traccia, viene utilizzato `sp_trace_setevent` per aggiungere colonne dell'escalation dei blocchi alla traccia, quindi `sp_trace_setstatus` per avviare la traccia. In istruzioni come `EXEC sp_trace_setevent @TraceID, 60, 22, 1`, il numero `60` indica la classe di evento dell'escalation, `22` indica la colonna **ObjectID** e `1` imposta l'evento di traccia su ON.  
  
```  
DECLARE @RC int, @TraceID int;  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\TraceResults';  
-- Set the events and data columns you need to capture.  
EXEC sp_trace_setevent @TraceID, 60,  1, 1; --  1 = TextData  
EXEC sp_trace_setevent @TraceID, 60, 12, 1; -- 12 = SPID  
EXEC sp_trace_setevent @TraceID, 60, 21, 1; -- 21 = EventSubClass  
EXEC sp_trace_setevent @TraceID, 60, 22, 1; -- 22 = ObjectID  
EXEC sp_trace_setevent @TraceID, 60, 25, 1; -- 25 = IntegerData  
EXEC sp_trace_setevent @TraceID, 60, 55, 1; -- 25 = IntegerData2  
EXEC sp_trace_setevent @TraceID, 60, 57, 1; -- 57 = Type  
-- Set any filter  by using sp_trace_setfilter.  
-- Start the trace.  
EXEC sp_trace_setstatus @TraceID, 1;  
GO  
```  
  
 Dal momento che la traccia è in esecuzione, eseguire le istruzioni che si desidera creare una traccia. Una volta terminato, eseguire il seguente codice per arrestare e chiudere la traccia. Nell'esempio seguente viene utilizzata la funzione `fn_trace_getinfo` affinché `traceid` venga utilizzato nelle istruzioni `sp_trace_setstatus` .  
  
```  
-- After the trace is complete.  
DECLARE @TraceID int;  
-- Find the traceid of the current trace.  
SELECT @TraceID = traceid   
FROM ::fn_trace_getinfo(default)   
WHERE value = N'C:\TraceResults.trc';  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0;  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  

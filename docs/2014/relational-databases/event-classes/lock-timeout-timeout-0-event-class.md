---
title: Classe di evento Lock:Timeout (timeout &gt; 0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Timeout event class
ms.assetid: d755833a-d7eb-4973-9352-67a2fba2442a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 312cda4fd588336d8be42c82a20392c8d0b80664
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63023496"
---
# <a name="locktimeout-timeout-gt-0-event-class"></a>Classe di evento Lock:Timeout (timeout &gt; 0)
  La classe di evento **Lock:Timeout (timeout > 0)** indica che una richiesta di blocco su una risorsa, ad esempio una pagina, è scaduta perché la risorsa è bloccata da un'altra transazione. Il funzionamento di questa classe di evento è identico a quello della classe **Lock:Timeout**, con l'eccezione che non vengono inclusi gli eventi con valore di timeout pari a 0.  
  
 Includere la classe di evento **Lock:Timeout (timeout > 0)** nelle tracce in cui si usano probe per i blocchi o altri processi con valori di timeout pari a 0. In questo modo è possibile individuare solo gli effettivi timeout escludendo quelli con valore pari a zero.  
  
## <a name="locktimeout-timeout--0-event-class-data-columns"></a>Colonne di dati della classe di evento Lock:Timeout (timeout > 0)  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|BinaryData|`image`|Identificatore della risorsa blocco.|2|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database in cui si è verificato il timeout. Se la colonna di dati `ServerName` viene catturata nella traccia e il server è disponibile [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database in cui si è verificato il timeout.|35|Yes|  
|Duration|`bigint`|Durata dell'evento in microsecondi.|13|Yes|  
|EndTime|`datetime`|Ora di fine dell'evento. Questa colonna non viene popolata per le classi degli eventi di avvio, come **SQL:BatchStarting** o **SP:Starting**.|15|Yes|  
|EventClass|`int`|Tipo di evento=189.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|Modalità|`int`|Stato richiesto o ricevuto dall'evento.<br /><br /> 0=NULL<br /><br /> 1=Sch-S<br /><br /> 2=Sch-M<br /><br /> 3=S<br /><br /> 4=U<br /><br /> 5=X<br /><br /> 6=IS<br /><br /> 7=IU<br /><br /> 8=IX<br /><br /> 9=SIU<br /><br /> 10=SIX<br /><br /> 11=UIX<br /><br /> 12=BU<br /><br /> 13=RangeS-S<br /><br /> 14=RangeS-U<br /><br /> 15=RangeI-N<br /><br /> 16=RangeI-S<br /><br /> 17=RangeI-U<br /><br /> 18=RangeI-X<br /><br /> 19=RangeX-S<br /><br /> 20=RangeX-U<br /><br /> 21=RangeX-X|32|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID dell'oggetto, se disponibile e applicabile.|22|Yes|  
|ObjectID2|`bigint`|ID dell'entità o dell'oggetto correlato, se disponibile e applicabile.|56|Yes|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se, ad esempio, si esegue la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, in `SessionLoginName` viene visualizzato Login1 e in `LoginName` viene visualizzato Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Valore di testo che dipende dalla classe di evento acquisita nella traccia.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|Tipo|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe di evento Lock:Timeout](lock-timeout-event-class.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  

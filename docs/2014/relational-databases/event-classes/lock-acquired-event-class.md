---
title: Classe di evento Lock:Acquired | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Acquired event class
ms.assetid: a6b1df2a-06ed-4fc3-8a84-f0becd5810d5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a49ddbbbff88ca0ae33caf4230954df710f29365
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665323"
---
# <a name="lockacquired-event-class"></a>Classe Lock:Acquired Event
  La classe di evento Lock:Acquiredevent indica l'acquisizione di un blocco su una risorsa, ad esempio una pagina di dati.  
  
 Le classi di evento Lock:Acquired e Lock:Released consentono di monitorare i blocchi acquisiti sugli oggetti, il tipo di blocco applicato e la durata del blocco. I blocchi mantenuti per lunghi periodi di tempo possono causare problemi di contesa. Per questo è necessario esaminarli. Ad esempio, è possibile che un'applicazione acquisisca i blocchi sulle righe di una tabella e quindi rimanga in attesa dell'input utente. L'attesa dell'input utente può essere prolungata e pertanto bloccare altri utenti. In tal caso, sarà necessario riprogettare l'applicazione in modo che le richieste di blocco vengano attivate soltanto quando necessario e che al momento dell'acquisizione dei blocchi non venga richiesto l'input utente.  
  
## <a name="lockacquired-event-class-data-columns"></a>Colonne di dati della classe di evento Lock:Acquired  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|BigintData1|`bigint`|ID partizione se la risorsa di blocco è partizionata.|52|Yes|  
|BinaryData|`image`|Identificatore della risorsa blocco.|2|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database in cui è stato acquisito il blocco. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|Duration|`bigint`|Tempo, espresso in microsecondi, tra la generazione della richiesta di blocco e l'acquisizione del blocco.|13|Yes|  
|EndTime|`datetime`|Ora di fine dell'evento.|15|Yes|  
|EventClass|`int`|Tipo di evento = 24.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|Modalità|`int`|Modalità risultante dopo l'acquisizione del blocco.<br /><br /> 0=NULL - Compatibile con tutte le altre modalità di blocco (LCK_M_NL)<br /><br /> 1=Blocco di stabilità dello schema (LCK_M_SCH_S)<br /><br /> 1=Blocco di modifica dello schema (LCK_M_SCH_M)<br /><br /> 3=Blocco condiviso (LCK_M_S)<br /><br /> 4=Blocco di aggiornamento (LCK_M_U)<br /><br /> 5=Blocco esclusivo (LCK_M_X)<br /><br /> 6=Blocco condiviso preventivo (LCK_M_IS)<br /><br /> 7=Blocco di aggiornamento preventivo (LCK_M_IU)<br /><br /> 8=Blocco esclusivo preventivo (LCK_M_IX)<br /><br /> 9=Condiviso-Preventivo-Aggiornamento (LCK_M_SIU)<br /><br /> 10=Condiviso-Preventivo-Esclusivo (LCK_M_SIX)<br /><br /> 10=Aggiornamento-Preventivo-Esclusivo (LCK_M_SIX)<br /><br /> 12=Blocco aggiornamenti bulk (LCK_M_BU)<br /><br /> 13=Intervalli di chiavi-Condiviso/Condiviso (LCK_M_RS_S)<br /><br /> 14=Intervalli di chiavi-Condiviso/Aggiornamento (LCK_M_RS_U)<br /><br /> 15=Intervalli di chiavi-Inserimento-NULL (LCK_M_RI_NL)<br /><br /> 16=Intervalli di chiavi-Inserimento-Condiviso (LCK_M_RI_S)<br /><br /> 17=Intervalli di chiavi-Inserimento-Aggiornamento (LCK_M_RI_U)<br /><br /> 18=Intervalli di chiavi-Inserimento-Esclusivo (LCK_M_RI_X)<br /><br /> 19=Intervalli di chiavi-Esclusivo-Condiviso (LCK_M_RX_S)<br /><br /> 20=Intervalli di chiavi-Esclusivo-Aggiornamento (LCK_M_RX_U)<br /><br /> 21=Intervalli di chiavi-Esclusivo-Esclusivo (LCK_M_RX_X)|32|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID dell'oggetto sul quale è stato acquisito il blocco, se disponibile e applicabile.|22|Yes|  
|ObjectID2|`bigint`|ID dell'entità o dell'oggetto correlato, se disponibile e applicabile.|56|Yes|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Valore di testo che dipende dal tipo di blocco acquisito. Corrisponde al valore della colonna resource_description in sys.dm_tran_locks.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|Type|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe di evento Lock:Released](lock-released-event-class.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  

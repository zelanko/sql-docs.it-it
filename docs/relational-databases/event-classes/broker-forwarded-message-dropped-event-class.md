---
title: Classe di evento Broker:Forwarded Message Dropped | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2fb2e65589e8cec209eb1d7336ec83da3b14737
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265521"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped - classe di evento

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento Broker:Forwarded Message Dropped quando Service Broker elimina un messaggio di cui è previsto l'inoltro.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Colonne di dati della classe di evento Broker:Forwarded Message Dropped  
  
|Colonna di dati|Tipo|Descrizione|Numero colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|BigintData1|**bigint**|Numero di sequenza del messaggio.|52|no|  
|ClientProcessID|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Sì|  
|DatabaseID|**int**|ID del database specificato dall'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita alcuna istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] viene visualizzato il nome del database se la colonna di dati ServerName viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|DatabaseName|**nvarchar**|Nome del database in cui viene eseguita l'istruzione dell'utente.|35|Sì|  
|DBUserName|**nvarchar**|Identificatore dell'istanza di Service broker da cui proviene il messaggio.|40|no|  
|Errore|**int**|Numero di ID del messaggio in sys.messages per il testo dell'evento.|31|no|  
|EventClass|**int**|Tipo di classe di evento acquisita. Per Broker:Forwarded Message Dropped, corrisponde sempre a 191.|27|no|  
|EventSequence|**int**|Numero di sequenza dell'evento.|51|no|  
|FileName|**nvarchar**|Nome del servizio a cui è destinato il messaggio.|36|no|  
|GUID|**uniqueidentifier**|ID di conversazione del dialogo. Questo identificatore viene trasmesso come parte del messaggio e viene condiviso da entrambi i lati della conversazione.|54|no|  
|HostName|**nvarchar**|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|IndexID|**int**|Numero di hop rimanenti per il messaggio inoltrato.|24|no|  
|IntegerData|**int**|Numero di frammento del messaggio inoltrato.|25|no|  
|LoginSid|**image**|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|NTDomainName|**nvarchar**|Dominio di Windows a cui appartiene l'utente.|7|Sì|  
|NTUserName|**nvarchar**|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Sì|  
|ObjectId|**int**|Valore di durata (TTL) del messaggio inoltrato.|22|no|  
|ObjectName|**nvarchar**|ID del messaggio inoltrato.|34|no|  
|OwnerName|**nvarchar**|Identificatore dell'istanza di Service Broker che rappresenta la destinazione del messaggio.|37|no|  
|RoleName|**nvarchar**|Ruolo dell'handle di conversazione. I possibili valori sono i seguenti:<br /><br /> - Iniziatore. Istanza di Service Broker che ha iniziato la conversazione.<br /><br /> - Destinazione. Istanza di Service Broker che funge da destinazione della conversazione.|38|no|  
|ServerName|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|Severity|**int**|Numero di gravità per il testo dell'evento.|29|no|  
|SPID|**int**|ID del processo server assegnato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo associato al client.|12|Sì|  
|StartTime|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|State|**int**|Indica la posizione che ha generato l'evento all'interno del codice sorgente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni punto che può generare questo evento è contraddistinto da un codice di stato diverso. Questo codice di stato consente al supporto tecnico Microsoft di individuare la posizione in cui è stato generato l'evento.|30|no|  
|Esito positivo|**int**|Intervallo di tempo in cui il messaggio è stato attivo. Quando questo valore è uguale o maggiore a quello della durata (TTL), il messaggio viene eliminato.|23|no|  
|TargetLoginName|**nvarchar**|Indirizzo di rete a cui doveva essere inoltrato il messaggio.|42|no|  
|TargetUserName|**nvarchar**|Nome del servizio di origine per il messaggio.|39|no|  
|TextData|**ntext**|Descrizione del motivo per cui il messaggio è stato eliminato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|1|Sì|  
|TransactionID|**bigint**|ID della transazione assegnato dal sistema.|4|no|  
  
 La colonna TextData dell'evento contiene una descrizione del motivo per cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha eliminato il messaggio.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  

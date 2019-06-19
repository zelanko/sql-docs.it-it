---
title: Classe di evento Broker:Message Classify | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bf9029a72ab1d02f02c5d1e7f51ffb85b76d93e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66265506"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify - classe di evento

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Message Classify** quando Service Broker stabilisce la modalità di recapito di un messaggio.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Colonne di dati della classe di evento Broker:Message Classify  
  
|Colonna di dati|Tipo di dati|Descrizione|Numero colonna|Filtrabile|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Sì|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|**EventClass**|**int**|Tipo di classe di evento acquisita. Per **Broker:Message Classify** , corrisponde sempre a **141**.|27|no|  
|**EventSequence**|**int**|Numero di sequenza dell'evento.|51|no|  
|**EventSubClass**|**nvarchar**|Tipo di sottoclasse di evento in cui sono disponibili informazioni aggiuntive su ogni classe di evento. Questa colonna può contenere i valori seguenti:<br /><br /> **Local**: la route scelta ha l'indirizzo LOCAL.<br /><br /> **Remote**:                 la route scelta ha un indirizzo diverso da LOCAL.<br /><br /> **Delayed**:                 il messaggio viene posticipato perché l'inoltro è disabilitato o non è disponibile alcuna route corrispondente.|21|Sì|  
|**FileName**|**nvarchar**|Nome del servizio a cui è indirizzato il messaggio.|36|no|  
|**GUID**|**uniqueidentifier**|ID di conversazione del dialogo. Questo identificatore viene trasmesso come parte del messaggio e viene condiviso da entrambi i lati della conversazione.|54|no|  
|**HostName**|**nvarchar**|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|no|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|**NTDomainName**|**nvarchar**|Dominio di Windows a cui appartiene l'utente.|7|Sì|  
|**NTUserName**|**nvarchar**|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Sì|  
|**OwnerName**|**nvarchar**|Identificatore dell'istanza di Service Broker a cui è indirizzato il messaggio.|37|no|  
|**RoleName**|**nvarchar**|Indica se il messaggio è stato ricevuto dalla rete o ha avuto origine in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|38|no|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|**SPID**|**int**|ID del processo server assegnato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo associato al client.|12|Sì|  
|**Start Time**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|**TargetUserName**|**nvarchar**|Indirizzo di rete dell'istanza di Service Broker che include l'hop successivo.|39|no|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|no|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  

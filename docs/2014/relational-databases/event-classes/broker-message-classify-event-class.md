---
title: Classe di evento Broker:Message Classify | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4398085227952f30e4df7d54ac78c1aef1355173
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664050"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify - classe di evento
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Message Classify** quando Service Broker stabilisce la modalità di recapito di un messaggio.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Colonne di dati della classe di evento Broker:Message Classify  
  
|Colonna di dati|Tipo di dati|Descrizione|Numero colonna|Filtrabile|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**EventClass**|**int**|Tipo di classe di evento acquisita. Per **Broker:Message Classify** , corrisponde sempre a **141**.|27|No|  
|**EventSequence**|**int**|Numero di sequenza dell'evento.|51|no|  
|**EventSubClass**|**nvarchar**|Tipo di sottoclasse di evento in cui sono disponibili informazioni aggiuntive su ogni classe di evento. Questa colonna può contenere i valori seguenti:<br /><br /> **Locale**: La route scelta ha l'indirizzo LOCAL.<br /><br /> **Remoto**: La route scelta ha un indirizzo diverso da LOCAL.<br /><br /> **Ritardo**: Il messaggio viene posticipato perché l'inoltro è disabilitato o perché non vi è alcuna route corrispondente.|21|Yes|  
|**FileName**|**nvarchar**|Nome del servizio a cui è indirizzato il messaggio.|36|No|  
|**GUID**|**uniqueidentifier**|ID di conversazione del dialogo. Questo identificatore viene trasmesso come parte del messaggio e viene condiviso da entrambi i lati della conversazione.|54|no|  
|**HostName**|**nvarchar**|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|No|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio di Windows a cui appartiene l'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Yes|  
|**OwnerName**|**nvarchar**|Identificatore dell'istanza di Service Broker a cui è indirizzato il messaggio.|37|no|  
|**RoleName**|**nvarchar**|Indica se il messaggio è stato ricevuto dalla rete o ha avuto origine in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|38|no|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SPID**|**int**|ID del processo server assegnato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo associato al client.|12|Yes|  
|**Start Time**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TargetUserName**|**nvarchar**|Indirizzo di rete dell'istanza di Service Broker che include l'hop successivo.|39|no|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|No|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  

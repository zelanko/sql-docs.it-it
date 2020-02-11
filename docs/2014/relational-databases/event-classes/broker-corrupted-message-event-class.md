---
title: Classe di evento Broker:Corrupted Message | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Corrupted Message event class
ms.assetid: 084bf198-2138-438e-bdc7-4ff1e04300f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a49f10826496e9e8fea46b1846b74535a173f821
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62664086"
---
# <a name="brokercorrupted-message-event-class"></a>Broker:Corrupted Message - classe di evento
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un evento **Broker:Corrupted Message** quando Service Broker riceve un messaggio danneggiato.  
  
## <a name="brokercorrupted-message-event-class-data-columns"></a>Colonne di dati della classe di evento Broker:Corrupted Message  
  
|Colonna di dati|Type|Descrizione|Numero di colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|**BigintData1**|**bigint**|Numero di sequenza del messaggio.|52|No|  
|**BinaryData**|**image**|Corpo del messaggio.|2|Sì|  
|**ClientProcessID**|**int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Sì|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|**Error (Errore) (Error (Errore)e)**|**int**|Numero di ID del messaggio in **sys.messages** relativo al testo dell'evento.|31|No|  
|**EventClass**|**int**|Tipo di classe di evento acquisita. Corrisponde sempre a **161** per **Broker:Corrupted Message**.|27|No|  
|**EventSequence**|**int**|Numero di sequenza dell'evento.|51|No|  
|**FileName**|**nvarchar**|Indirizzo di rete dell'endpoint remoto.|36|No|  
|**GUID**|**uniqueidentifier**|ID della conversazione alla quale appartiene il messaggio. Questo identificatore viene trasmesso come parte del messaggio e viene condiviso da entrambi i lati della conversazione.|54|No|  
|**Host Name**|**nvarchar**|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|**IntegerData**|**int**|Numero di frammento del messaggio.|25|Sì|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|No|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|**NTDomainName**|**nvarchar**|Dominio di Windows a cui appartiene l'utente.|7|Sì|  
|**NTUserName**|**nvarchar**|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Sì|  
|**ObjectName**|**nvarchar**|Nome del servizio dell'altro lato della conversazione e stringa di connessione utilizzata dal database remoto per connettersi al database.|34|No|  
|**RoleName**|**nvarchar**|Ruolo dell'endpoint che riceve il messaggio. I possibili valori sono i seguenti.<br /><br /> **iniziatore**:<br />                  L'endpoint che riceve il messaggio è l'initiator della conversazione.<br /><br /> **destinazione**:<br />                  L'endpoint che riceve il messaggio è la destinazione della conversazione.|38|No|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**Gravità**|**int**|Gravità dell'errore che ha determinato l'eliminazione del messaggio in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|29|No|  
|**SPID**|**int**|ID del processo server assegnato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo associato al client.|12|Sì|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|**Stato**|**int**|Indica la posizione che ha generato l'evento all'interno del codice sorgente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni punto che può generare questo evento è contraddistinto da un codice di stato diverso. Questo codice di stato consente al supporto tecnico Microsoft di individuare la posizione in cui è stato generato l'evento.|30|No|  
|**TextData**|**ntext**|Descrizione del danneggiamento rilevato.|1|Sì|  
|**ID transazione**|**bigint**|ID della transazione assegnato dal sistema.|4|No|  
  
 La colonna **TextData** dell'evento contiene un messaggio che descrive il problema correlato al messaggio.  
  
  

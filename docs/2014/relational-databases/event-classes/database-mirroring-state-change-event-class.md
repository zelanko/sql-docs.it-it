---
title: Classe di evento Database Mirroring State Change | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f81b196ee1b686fbe2dd3563f694411a0e00d962
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62663045"
---
# <a name="database-mirroring-state-change-event-class"></a>Database Mirroring State Change - classe di evento
  La classe di evento **database mirroring State Change** indica quando cambia lo stato di un database con mirroring. Includere questa classe di evento nelle tracce che eseguono il monitoraggio delle condizioni dei database con mirroring.  
  
 Quando la classe di evento **Database Mirroring State Change** viene inclusa in una traccia, il relativo overhead è ridotto. L'overhead può essere maggiore se il valore dello stato dei database con mirroring aumenta.  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Colonne di dati della classe di evento Database Mirroring State Change  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione USE *database* oppure il database predefinito se non è stata eseguita alcuna istruzione USE *database* per una determinata istanza. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]consente di visualizzare il nome del database se la colonna di dati **ServerName** viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|**DatabaseName**|**nvarchar**|Nome del database con mirroring.|35|Sì|  
|**EventClass**|**int**|Tipo di evento = 167.|27|No|  
|**EventSequence**|**int**|Sequenza della classe di evento nel batch.|51|No|  
|**IntegerData**|**int**|ID di stato precedente.|25|Sì|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Sì|  
|**LoginSid**|**immagine**|ID di sicurezza (SID) dell'utente connesso. È possibile trovare queste informazioni nella vista del catalogo **sys. server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|**RequestID**|**int**|ID della richiesta contenente l'istruzione.|49|Sì|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|**Stato**|**int**|Nuovo ID dello stato di mirroring:<br /><br /> 0 = Notifica Null<br /><br /> 1 = Server principale sincronizzato con il server di controllo del mirroring<br /><br /> 2 = Server principale sincronizzato senza il server di controllo del mirroring<br /><br /> 3 = Server mirror sincronizzato con il server di controllo del mirroring<br /><br /> 4 = Server mirror sincronizzato senza il server di controllo del mirroring<br /><br /> 5 = Perdita di connessione con il server principale<br /><br /> 6 = Perdita di connessione con il server mirror<br /><br /> 7 = Failover manuale<br /><br /> 8 = Failover automatico<br /><br /> 9 = Mirroring sospeso<br /><br /> 10 = Nessun quorum<br /><br /> 11 = Sincronizzazione del server mirror in corso<br /><br /> 12 = Server principale in esecuzione esposto|30|Sì|  
|**TextData**|**ntext**|Descrizione della variazione di stato.|1|Sì|  
|**ID transazione**|**bigint**|ID della transazione assegnato dal sistema.|4|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

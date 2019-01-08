---
title: Classe di evento FT:Crawl Started | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Crawl Started event class
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b249aff99abbe692e1515397c493109c54c86713
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772613"
---
# <a name="ftcrawl-started-event-class"></a>Classe di evento FT:Crawl Started
  La classe di evento **FT:Crawl Started** indica l'avvio di una ricerca per indicizzazione (popolamento) full-text. Utilizzare questa classe di evento per verificare che una richiesta di ricerca per indicizzazione venga effettivamente accolta dalle attività di lavoro.  
  
## <a name="ft-crawl-started-event-class-data-columns"></a>FULL-TEXT: Colonne di dati di classe di evento di avvio di ricerca per indicizzazione  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID del database in cui è stata avviata la ricerca per indicizzazione full-text. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**EventClass**|**int**|Tipo di evento = 155.|27|No|  
|**EventSequence**|**int**|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**ObjectID**|**int**|ID dell'oggetto assegnato dal sistema. La ricerca per indicizzazione full-text è stata avviata sull'indice full-text in questo oggetto.|22|Yes|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna vengono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**TextData**|**ntext**|Tipo di ricerca per indicizzazione full-text. I valori possibili sono Completa, Incrementale, Manuale o Automatica.|1|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

---
title: Classe di evento FT:Crawl Aborted | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Crawl Aborted event class
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba7914456e4ffcf19a52c6e7f7206a390147cc2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662424"
---
# <a name="ftcrawl-aborted-event-class"></a>Classe di evento FT:Crawl Aborted
  La classe di evento **FT:Crawl Aborted** indica che si è verificata un'eccezione durante una ricerca per indicizzazione full-text. In genere, l'errore causa l'arresto della ricerca. Per ulteriori informazioni sull'errore, controllare il registro eventi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows o il log di tipo ricerca per indicizzazione.  
  
## <a name="ftcrawl-aborted-event-class-data-columns"></a>Colonne di dati della classe di evento FT:Crawl Aborted  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID del database nel quale viene eseguita la ricerca per indicizzazione full-text. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**Errore**|**int**|Numero di errore di un evento specifico. Corrisponde spesso al numero di errore archiviato nella tabella **sysmessages** .|31|Yes|  
|**EventClass**|**int**|Tipo di evento = 157.|27|No|  
|**EventSequence**|**int**|Sequenza di un determinato evento all'interno della richiesta.|51|no|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**ObjectID**|**int**|ID assegnato dal sistema all'oggetto sul quale viene eseguita la ricerca per indicizzazione full-text quando si verifica l'errore.|22|Yes|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**State**|**int**|Equivalente a un codice di stato dell'errore.|30|Yes|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  

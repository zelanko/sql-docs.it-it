---
title: Classe di evento Database Suspect Data Page | Microsoft Docs
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
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78e6a175ce7757a9e9808a5a993bec6a44a3db2a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62662993"
---
# <a name="database-suspect-data-page-event-class"></a>classe di evento Database Suspect Data Page
  La classe di evento **Database Suspect Data Page** indica quando una pagina viene aggiunta alla tabella [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) in [msdb](../databases/msdb-database.md). Includere questa classe di evento nelle tracce che eseguono il monitoraggio dell'occorrenza di pagine sospette.  
  
> [!NOTE]  
>  Questo evento viene generato in modo asincrono dall'inserimento di una riga corrispondente nella tabella **suspect_pages** . Quindi un processo in ascolto per tale evento potrebbe non trovare immediatamente la voce **suspect_pages** corrispondente.  
  
 Quando la classe di evento **Database Suspect Data Page** viene inclusa in una traccia, il relativo overhead è ridotto. L'overhead potrebbe essere maggiore se il numero di pagine sospette aumenta, ad esempio se si stanno verificando problemi in un'unità disco.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Colonne di dati della classe di evento Database Suspect Data Page  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID del database per il quale è stato generato l'evento della pagina sospetta. Corrisponde alla colonna **database_id** della tabella **suspect_pages** .|3|Yes|  
|**EventClass**|**int**|Il tipo di evento è 213.|27|No|  
|**EventSequence**|**int**|Sequenza della classe di evento nel batch.|51|No|  
|**SPID**|**int**|ID dell'attività [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha rilevato la pagina sospetta.|12|Yes|  
|**StartTime**|**datetime**|Ora in cui si è verificato l'evento.|14|Yes|  
|**ObjectID**|**int**|ID del file di database contenente la pagina sospetta. Corrisponde alla colonna **file_id** della tabella **suspect_pages** .|22|Yes|  
|**ObjectID2**|**int**|ID della pagina sospetta nel file. Corrisponde alla colonna **page_id** della tabella **suspect_pages** .|56|Yes|  
|**Errore**|**int**|Tipo di errore rilevato. Questo valore corrisponde al valore **event_type** per la pagina nella tabella **suspect_pages** .|31|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

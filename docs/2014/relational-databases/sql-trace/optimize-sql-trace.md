---
title: Ottimizzare l'uso di Traccia SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3b29965c33270bbf8d9173c55e96af48b9c4f749
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799723"
---
# <a name="optimize-sql-trace"></a>Ottimizzare l'utilizzo di Traccia SQL
  Sebbene l'esecuzione di Traccia SQL comporti costi di prestazioni significativi, in quanto la funzionalità utilizza le risorse di sistema per raccogliere dati, è possibile adottare numerosi accorgimenti per ridurre tali costi. Per ridurre i costi di prestazioni provocati dall'utilizzo di una traccia, provare le soluzioni seguenti:  
  
-   Utilizzare il prompt dei comandi per eseguire tracce. L'utilizzo di un'interfaccia utente grafica influisce sulle prestazioni. Per altre informazioni, vedere [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql).  
  
-   Evitare di includere eventi generati di frequente. Se possibile, limitare la traccia tramite classi di evento e filtri specifici. Se viene raccolta una quantità minore di eventi di traccia, sarà minore anche la quantità di risorse di sistema necessarie per eseguire la traccia.  
  
-   Concentrare la traccia per raccogliere solo gli eventi che forniscono dati pertinenti. Se, ad esempio, la traccia consiste nell'identificare deadlock, includere la classe di evento **Lock:Deadlock** , ma non **Lock:Acquired** . Se si includono entrambe le classi di evento, la traccia dovrà rispondere a ogni blocco acquisito e i costi di esecuzione risulteranno raddoppiati.  
  
-   Evitare di raccogliere dati duplicati. Se, ad esempio, si raccolgono le classi di evento **SQL:BatchStarted** e **SQL:BatchCompleted**, è possibile ridurre le dimensioni dei set di risultati raccogliendo i dati di testo solo per la classe di evento **SQL:BatchStarted** .  
  
-   Utilizzare filtri nella definizione di traccia. Se, ad esempio, un utente segnala prestazioni rallentate durante l'esecuzione di query ad hoc, creare un filtro in **LoginName**. Impostare il filtro in modo da includere solo gli eventi in cui **LoginName** corrisponde al nome dell'utente.  
  
 Se è necessario eseguire una traccia per eventi che comportano un impatto significativo sulle prestazioni, provare a limitare tale impatto nel server utilizzando uno dei modi seguenti:  
  
-   Eseguire tracce per periodi di tempo inferiori. È possibile controllare la quantità di tempo impiegata per l'esecuzione di una traccia abilitando un'ora di arresto. Si tratta di un aspetto particolarmente importante se non è possibile limitare le classi di evento o filtrare un evento. L'abilitazione di un'ora di arresto garantisce che l'impatto sulle prestazioni non duri all'infinito.  
  
-   Limitare le dimensioni dei risultati della traccia. È possibile limitare le dimensioni dei risultati della traccia impostando dimensioni file massime. Questa strategia assicura l'azzeramento dei costi di prestazioni dopo che sono state raggiunte le dimensioni limite per il file, a condizione che non sia abilitato il rollover dei file.  
  
-   Limitare il numero di eventi restituiti. Tramite [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] è possibile limitare il numero di eventi restituiti salvando la traccia in una tabella e impostando il numero massimo di righe. I risultati della traccia verranno comunque restituiti nella schermata di [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] dopo il raggiungimento del numero massimo di righe, ma sarà possibile azzerare i costi correlati alla registrazione dei risultati in una tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Filtrare una traccia](../sql-trace/filter-a-trace.md)  
  
  

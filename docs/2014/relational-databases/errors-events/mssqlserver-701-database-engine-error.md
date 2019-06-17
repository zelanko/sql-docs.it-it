---
title: MSSQLSERVER_701 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 701 (Database Engine error)
ms.assetid: 3b975000-63a1-43c2-a40f-89d0a8a36bef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c52c1d38e115e4064e106175bb49d0a3ecb4318d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913781"
---
# <a name="mssqlserver701"></a>MSSQLSERVER_701
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|701|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NOSYSMEM|  
|Testo del messaggio|Memoria di sistema insufficiente per l'esecuzione della query.|  
  
## <a name="explanation"></a>Spiegazione  
 Non è stato possibile allocare memoria sufficiente per eseguire la query in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le cause possono essere varie, tra cui impostazioni del sistema operativo, disponibilità della memoria fisica o limiti di memoria nel carico di lavoro corrente. Nella maggior parte dei casi la transazione che ha avuto esito negativo non è la causa dell'errore.  
  
 Le query di diagnostica, ad esempio le istruzioni DBCC, possono avere esito negativo perché il server non dispone di memoria sufficiente.  
  
 Timeout durante l'attesa di risorse di memoria per l'esecuzione della query nel pool di risorse 'predefinito'.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se non si utilizza Resource Governor, si consiglia di verificare lo stato generale del server e di caricare o controllare il pool di risorse o le impostazioni del gruppo del carico di lavoro.  
  
 Nell'elenco seguente viene illustrata la procedura generale per la risoluzione degli errori di memoria:  
  
1.  Verificare se altre applicazioni o servizi utilizzano la memoria nel server specificato. Riconfigurare le applicazioni o i servizi meno critici per utilizzare una quantità di memoria inferiore.  
  
2.  Avviare la raccolta dei contatori di performance monitor per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **: Buffer Manager**, **SQL Server: Gestore della memoria**.  
  
3.  Verificare i seguenti parametri di configurazione della memoria di SQL Server:  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     Valutare eventuali impostazioni non comuni e, se necessario, correggerle. Considerare i requisiti di memoria aggiuntivi. Le impostazioni predefinite sono elencate nell'argomento "Impostazione delle opzioni di configurazione del server" nella documentazione online di SQL Server.  
  
4.  Osservare l'output di DBCC MEMORYSTATUS e il modo in cui viene modificato quando vengono visualizzati questi messaggi di errore.  
  
5.  Verificare il carico di lavoro (ad esempio, numero di sessioni simultanee, query attualmente in esecuzione).  
  
 Per aumentare la quantità di memoria disponibile per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], effettuare le operazioni seguenti:  
  
-   Se le risorse vengono utilizzate da altre applicazioni oltre a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], provare ad arrestarne l'esecuzione oppure a eseguirle in un server distinto. In questo modo sarà possibile eliminare le richieste di memoria esterne.  
  
-   Se è stata configurata l'opzione **max server memory,** , aumentarne il valore impostato.  
  
 Eseguire i comandi DBCC seguenti per liberare diverse cache in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 Se il problema persiste, sarà necessario analizzarlo in modo più dettagliato e cercare di ridurre il carico di lavoro.  
  
  

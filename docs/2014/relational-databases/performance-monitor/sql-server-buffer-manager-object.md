---
title: Oggetto Buffer Manager di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed9c8ff90798205f9db02ae4b4b47eb4310d4b06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250755"
---
# <a name="sql-server-buffer-manager-object"></a>Oggetto di Gestione buffer di SQL Server
  L'oggetto di **Gestione buffer** fornisce contatori che consentono di monitorare l'utilizzo degli elementi seguenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Memoria per archiviare pagine di dati.  
  
-   Contatori per il monitoraggio dell'attività di I/O fisico quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue la lettura e la scrittura delle pagine del database.  
  
-   Estensione del pool di buffer per estendere la cache del buffer utilizzando risorse di archiviazione non volatili veloci quali le unità SSD.  
  
 Il monitoraggio della memoria e dei contatori utilizzati da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di determinare:  
  
-   Se vi sono colli di bottiglia dovuti a una quantità di memoria fisica inadeguata. Se la quantità di memoria fisica non è tale da consentire di memorizzare in cache i dati a cui si accede con maggiore frequenza, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve recuperare i dati dal disco.  
  
-   Se è possibile migliorare le prestazioni delle query aggiungendo memoria o rendendo disponibile una maggiore quantità di memoria per la cache dei dati o le strutture interne di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La frequenza con cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ricorrere alla lettura dei dati dal disco. Rispetto agli altri tipi di operazioni, ad esempio l'accesso alla memoria, l'I/O fisico richiede una maggiore quantità di tempo. Riducendo al minimo le operazioni di I/O fisico è possibile migliorare le prestazioni delle query.  
  
## <a name="buffer-manager-performance-objects"></a>Oggetti prestazioni di Gestione buffer  
 Nella tabella seguente vengono descritti gli oggetti prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Gestione buffer** .  
  
|Contatori di Gestione buffer di SQL Server|Descrizione|  
|----------------------------------------|-----------------|  
|**Percentuale riscontri cache buffer**|Indica la percentuale di pagine trovate nella cache del buffer senza dover ricorrere a una lettura dal disco. La percentuale è data dal rapporto tra il totale dei riscontri nella cache e il totale di ricerche nella cache eseguite considerate alcune migliaia dei più recenti accessi alla pagina. La variazione della percentuale su lunghi periodi di tempo è limitata. Poiché la lettura dalla cache richiede una quantità di risorse molto minore rispetto alla lettura dal disco, è auspicabile che il valore della percentuale sia elevato. È generalmente possibile aumentare la percentuale di riscontri nella cache del buffer aumentando la quantità di memoria disponibile per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utilizzando la funzionalità estensione del pool di buffer.|  
|**Pagine checkpoint/sec**|Indica il numero di pagine al secondo scaricate nel disco tramite checkpoint o altre operazioni che richiedono lo scaricamento di tutte le pagine dirty.|  
|**Pagine di database**|Indica il numero di pagine con contenuto di database nel pool di buffer.|  
|**Pagine di estensione allocate**|Numero totale di pagine memorizzate nella cache non disponibili nel file di estensione del pool di buffer.|  
|**Pagine di estensione disponibili**|Numero totale di pagine memorizzate nella cache disponibili nel file di estensione del pool di buffer.|  
|**Estensione utilizzata in percentuale**|Percentuale del file di paging dell'estensione del pool di buffer occupato dalle pagine di Gestione buffer.|  
|**Contatore IO di estensione in attesa**|Lunghezza della coda di I/O per il file di estensione del pool di buffer.|  
|**Eliminazioni pagine di estensione/sec**|Numero di pagine eliminate dal file dell'estensione del pool di buffer al secondo.|  
|**Letture pagine di estensione/sec**|Numero di pagine lette dal file dell'estensione del pool di buffer al secondo.|  
|**Tempo senza riferimenti pagina di estensione**|Numero medio di secondi durante i quali una pagina viene mantenuta nell'estensione del pool di buffer senza riferimenti.|  
|**Scritture pagine di estensione/sec**|Numero di pagine scritte nel file dell'estensione del pool di buffer al secondo.|  
|**Blocchi elenco di disponibilità/sec**|Indica il numero di richieste al secondo per cui è stata necessaria l'attesa di una pagina disponibile.|  
|**Scritture Lazywriter/sec**|Indica il numero di buffer scritti al secondo da Lazywriter di Gestione buffer. *Lazywriter* è un processo di sistema che scarica batch di buffer dirty e obsoleti (buffer contenenti modifiche che devono essere riscritte su disco prima che il buffer possa essere riutilizzato per un'altra pagina) e li rende disponibili per i processi utente. Lazywriter elimina la necessità di eseguire checkpoint frequenti per la creazione di buffer disponibili.|  
|**Permanenza presunta delle pagine**|Indica il numero di secondi durante il quale una pagina viene mantenuta nel pool di buffer senza riferimenti.|  
|**Ricerche di pagina/sec**|Indica il numero di richieste al secondo per la ricerca di una pagina nel pool di buffer.|  
|**Letture di pagina/sec**|Indica il numero di letture fisiche di pagine del database eseguite al secondo. Il valore indica il totale di letture fisiche di pagine eseguite in tutti i database. Poiché l'I/O fisico richiede una notevole quantità di risorse, potrebbe essere possibile ridurre i costi utilizzando una cache dei dati di dimensioni maggiori, indici intelligenti e query più efficienti oppure modificando la progettazione del database.|  
|**Scritture di pagina/sec**|Indica il numero di scritture fisiche di pagine del database eseguite al secondo.|  
|**Pagine read-ahead/sec**|Indica il numero di pagine lette al secondo prima di essere utilizzate.|  
  
## <a name="see-also"></a>Vedere anche  
 [Nodo SQLServer:Buffer](sql-server-buffer-node.md)   
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Oggetto Plan Cache di SQL Server](sql-server-plan-cache-object.md)   
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Estensione pool di buffer](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  

---
title: OLTP in memoria (ottimizzazione in memoria) | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ebb953132e28a3ea0766f7d9d7cd40f3f620659
ms.sourcegitcommit: 20d24654e056561fc33cadc25eca8b4e7f214b1b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67351662"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>OLTP in memoria (ottimizzazione per la memoria)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] può migliorare significativamente le prestazioni di elaborazione delle transazioni, di inserimento e caricamento dei dati e di scenari di dati temporanei.  Per ottenere il codice di base e le informazioni necessarie per verificare rapidamente la tabella ottimizzata per la memoria e la stored procedure compilata in modo nativo, vedere
 -  [Avvio rapido 1: Tecnologie OLTP in memoria per migliorare le prestazioni di Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md).  
 
Video di 17 minuti che descrive OLTP in memoria e i vantaggi per le prestazioni:

-  [In-Memory OLTP in SQL Server 2016](https://www.youtube.com/watch?v=l5l5eophmK4)(OLTP in memoria in SQL Server 2016)

Per scaricare la demo sulle prestazioni per OLTP in memoria usata nel video: 

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

Per una panoramica più dettagliata di OLTP in memoria e un'analisi degli scenari che esaminano i vantaggi derivanti dalla tecnologia per le prestazioni:

- [Panoramica e scenari di utilizzo](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 Si noti che [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è la tecnologia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per migliorare le prestazioni dell'elaborazione delle transazioni. Per la tecnologia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che migliora la creazione di report e le prestazioni di query di analisi, vedere [Guida agli indici columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
 Sono stati apportati diversi miglioramenti a OLTP in memoria in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], nonché in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La superficie di attacco Transact-SQL è stata aumentata per semplificare la migrazione delle applicazioni di database. È stato aggiunto il supporto per l'esecuzione di operazioni ALTER per le tabelle ottimizzate per la memoria e le stored procedure compilate in modo nativo per semplificare la gestione delle applicazioni.
  
> [!NOTE]  
>  **Per provarlo**  
>   
>  OLTP in memoria è disponibile nei database SQL di Azure dei livelli Premium e Business Critical e nei pool elastici. Per iniziare a usare OLTP in memoria nonché columnstore nel database SQL di Azure, vedere [Introduzione alle tecnologie in memoria (anteprima) in database SQL](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  

## <a name="in-this-section"></a>Contenuto della sezione  
 In questa sezione vengono trattati gli argomenti seguenti:  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Avvio rapido 1: tecnologie OLTP in memoria per migliorare le prestazioni di Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|Analizza in maniera approfondita OLTP in memoria|
|[Panoramica e scenari di utilizzo](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|Panoramica delle informazioni su OLTP in memoria e degli scenari che ne esaminano i vantaggi.|
|[Requisiti per l'utilizzo di tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|Vengono descritti i requisiti hardware e software e le linee guida per l'utilizzo di tabelle ottimizzate per la memoria.|  
|[Esempi di codice di OLTP in memoria](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|Sono contenuti esempi di codice che illustrano come creare e usare una tabella ottimizzata per la memoria.|  
|[Tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|Vengono introdotte le tabelle ottimizzate per la memoria.|  
|[Variabili di tabella con ottimizzazione per la memoria](https://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|Esempio di codice in cui viene mostrato come usare una variabile di tabella ottimizzata per la memoria anziché una variabile di tabella tradizionale per ridurre l'utilizzo di tempdb.|  
|[Indici in tabelle con ottimizzazione per la memoria](https://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|Vengono introdotti indici ottimizzati per la memoria.|  
|[Stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|Vengono illustrate le stored procedure compilate in modo nativo.|  
|[Gestione della memoria per OLTP in memoria](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|Informazioni e gestione dell'utilizzo della memoria nel sistema.|  
|[Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|Vengono illustrati i file di dati e differenziali in cui vengono archiviate le informazioni sulle transazioni nelle tabelle ottimizzate per la memoria.|  
|[Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|Descrive le operazioni di backup, ripristino e recupero delle tabelle ottimizzate per la memoria.|  
|[Supporto di Transact-SQL per OLTP in memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|Descrive il supporto di [!INCLUDE[tsql](../../includes/tsql-md.md)] per [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Supporto della disponibilità elevata per i database OLTP in memoria](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|Descrive i gruppi di disponibilità e il clustering di failover in [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Supporto di SQL Server per OLTP in memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|Elenco della sintassi e delle funzionalità nuove e aggiornate per il supporto di tabelle ottimizzate per la memoria.|  
|[Migrazione a OLTP in memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|Viene illustrato come eseguire la migrazione di tabelle basate su disco in tabelle ottimizzate per la memoria.|  
  
 Altre informazioni su [!INCLUDE[hek_2](../../includes/hek-2-md.md)] sono disponibili in:  

- [Video che descrive OLTP in memoria e i vantaggi per le prestazioni](https://www.youtube.com/watch?v=l5l5eophmK4).

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [White paper tecnico su OLTP in memoria di SQL Server](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [Confronto tra le funzionalità di OLTP in memoria di SQL Server e columnstore](https://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   Novità di OLTP in memoria di SQL Server 2016 [Parte 1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) e [Parte 2](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [OLTP in memoria: considerazioni sulla migrazione e sui modelli di carico di lavoro comuni](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [Blog di OLTP in memoria](https://go.microsoft.com/fwlink/?LinkId=311696)  
  
## <a name="see-also"></a>Vedere anche  
 [Caratteristiche del database](../../relational-databases/database-features.md)  
  
  

---
title: OLTP in memoria (ottimizzazione in memoria) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87ad093d5be6f4fa394e934e6c0d88796a22e196
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401648"
---
# <a name="in-memory-oltp-and-memory-optimization"></a>OLTP in memoria e ottimizzazione per la memoria

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] può migliorare significativamente le prestazioni di elaborazione delle transazioni, di inserimento e caricamento dei dati e di scenari di dati temporanei.  Per ottenere il codice di base e le informazioni necessarie per verificare rapidamente la tabella ottimizzata per la memoria e la stored procedure compilata in modo nativo, vedere
 -  [Avvio rapido 1: Tecnologie OLTP in memoria per migliorare le prestazioni di Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md).  
 
In YouTube è stato caricato un [**video di 17 minuti**](#anchorname-17minute-video) che descrive OLTP in memoria in SQL Server, illustrandone i vantaggi per le prestazioni.

Per una panoramica più dettagliata di OLTP in memoria e un'analisi degli scenari che esaminano i vantaggi derivanti dalla tecnologia per le prestazioni:

- [Panoramica e scenari di utilizzo](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 Si noti che [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è la tecnologia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per migliorare le prestazioni dell'elaborazione delle transazioni. Per la tecnologia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che migliora la creazione di report e le prestazioni di query di analisi, vedere [Guida agli indici columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
 Sono stati apportati diversi miglioramenti a OLTP in memoria in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], nonché in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La superficie di attacco Transact-SQL è stata aumentata per semplificare la migrazione delle applicazioni di database. È stato aggiunto il supporto per l'esecuzione di operazioni ALTER per le tabelle ottimizzate per la memoria e le stored procedure compilate in modo nativo per semplificare la gestione delle applicazioni.
  
> [!NOTE]  
>  **Provare il servizio**  
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
|[Tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|Vengono introdotte le tabelle ottimizzate per la memoria.|  
|[Variabili di tabella con ottimizzazione per la memoria](https://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|Esempio di codice in cui viene mostrato come usare una variabile di tabella ottimizzata per la memoria anziché una variabile di tabella tradizionale per ridurre l'utilizzo di tempdb.|  
|[Indici in tabelle con ottimizzazione per la memoria](https://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|Vengono introdotti indici ottimizzati per la memoria.|  
|[Stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|Vengono illustrate le stored procedure compilate in modo nativo.|  
|[Gestione della memoria per OLTP in memoria](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|Informazioni e gestione dell'utilizzo della memoria nel sistema.|  
|[Creazione e gestione dell'archiviazione per gli oggetti ottimizzati per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|Vengono illustrati i file di dati e differenziali in cui vengono archiviate le informazioni sulle transazioni nelle tabelle ottimizzate per la memoria.|  
|[Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|Descrive le operazioni di backup, ripristino e recupero delle tabelle ottimizzate per la memoria.|  
|[Supporto di Transact-SQL per OLTP in memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|Descrive il supporto di [!INCLUDE[tsql](../../includes/tsql-md.md)] per [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Supporto della disponibilità elevata per i database OLTP in memoria](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|Descrive i gruppi di disponibilità e il clustering di failover in [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Supporto di SQL Server per OLTP in memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|Elenco della sintassi e delle funzionalità nuove e aggiornate per il supporto di tabelle ottimizzate per la memoria.|  
|[Migrazione a OLTP in memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|Viene illustrato come eseguire la migrazione di tabelle basate su disco in tabelle ottimizzate per la memoria.|  
| &nbsp; | &nbsp; |

## <a name="links-to-other-websites"></a>Collegamenti ad altri siti Web

Questa sezione include collegamenti ad altri siti Web che contengono informazioni su OLTP in memoria in SQL Server.

- [**Video** che descrive OLTP in memoria e i vantaggi per le prestazioni](#anchorname-17minute-video)

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [White paper tecnico su OLTP in memoria di SQL Server](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [Confronto tra le funzionalità di OLTP in memoria di SQL Server e columnstore](https://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   Novità di OLTP in memoria di SQL Server 2016, [Parte 1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) e [Parte 2](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [OLTP in memoria: considerazioni sulla migrazione e sui modelli di carico di lavoro comuni](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [Blog di OLTP in memoria](https://go.microsoft.com/fwlink/?LinkId=311696)  

## <a name="anchorname-17minute-video"></a>Video di 17 minuti, indicizzato

- _Titolo del video:_ &nbsp; **In-Memory OLTP in SQL Server 2016** (OLTP in memoria in SQL Server 2016)
- _Data di pubblicazione:_ &nbsp; 10-03-2019 su `YouTube.com`.
- _Durata:_ &nbsp; 17:32 &nbsp; &nbsp; (per i collegamenti al video, vedere il seguente [**indice**](#anchorname-index-17minute-video)).
- _Condotto da:_ &nbsp; Jos de Bruijn, Senior Program Manager per SQL Server

### <a name="demo-can-be-downloaded"></a>È possibile scaricare una demo

In corrispondenza del contrassegno temporale 08:09, il video esegue una dimostrazione due volte. È possibile scaricare il codice sorgente per la demo sulle prestazioni eseguibile usata nel video dal collegamento seguente:

- [In-Memory OLTP Performance Demo v1.0, code source](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

I passaggi generali illustrati nel video sono i seguenti:

1. Prima di tutto la demo viene eseguita con una tabella normale.
2. Viene quindi visualizzata un'edizione ottimizzata per la memoria della tabella che viene creata e popolata con pochi clic in SQL Server Management Studio (SSMS.exe).
3. La demo viene quindi rieseguita con la tabella ottimizzata per la memoria. Il miglioramento della velocità misurato è enorme.

### <a name="anchorname-index-17minute-video"></a>Indice per ogni sezione del video

| Collegamento al contrassegno temporale | Titolo della sezione |
| :------------- | :------------ |
| A.&nbsp; [00:00](https://www.youtube.com/watch?v=l5l5eophmK4&t=0) | Inizio. |
| <br/>B.&nbsp; [00:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=56) | <br/>Motivi per cui i clienti devono prendere in considerazione OLTP in memoria. |
| &nbsp; &nbsp; [01:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=63) | L'hardware moderno richiede un'architettura moderna del sistema di database. |
| &nbsp; &nbsp; [02:10](https://www.youtube.com/watch?v=l5l5eophmK4&t=130) | Esplosione nei dati generati; le operazioni devono essere immediate (bassa latenza). |
| &nbsp; &nbsp; [03:19](https://www.youtube.com/watch?v=l5l5eophmK4&t=199) | Ridurre il TCO: fare di più con le risorse disponibili. |
| <br/>C.&nbsp; [03:33](https://www.youtube.com/watch?v=l5l5eophmK4&t=213) | <br/>Che cos'è OLTP in memoria.<br/>Prestazioni ottimizzate grazie alla tecnologia ottimizzata per la memoria. |
| &nbsp; &nbsp; [05:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=303) | Elaborazione delle transazioni fino a 30 volte più veloce. |
| &nbsp; &nbsp; [05:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=322) | Completamente durevole: i dati sopravvivono agli errori del server. |
| &nbsp; &nbsp; [06:15](https://www.youtube.com/watch?v=l5l5eophmK4&t=375) | Integrazione completa in SQL Server. Non occorre imparare nuovi linguaggi o strumenti. |
| &nbsp; &nbsp; [07:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=442) | Primo rilascio in SQL Server 2014, ma con notevoli miglioramenti nella versione 2016. |
| &nbsp; &nbsp; [07:58](https://www.youtube.com/watch?v=l5l5eophmK4&t=558) | Disponibile anche nel database SQL di Azure (nel cloud). |
| <br/>D.&nbsp; [08:09](https://www.youtube.com/watch?v=l5l5eophmK4&t=489) | <br/>Dimostrazione delle prestazioni.<br/> Eseguire la demo con una tabella normale. |
| &nbsp; &nbsp; [09:11](https://www.youtube.com/watch?v=l5l5eophmK4&t=551) | Menu di scelta rapida di SSMS: **Report** &gt; **Analisi delle prestazioni delle transazioni** |
| &nbsp; &nbsp; [10:38](https://www.youtube.com/watch?v=l5l5eophmK4&t=638) | Menu di scelta rapida di SSMS: **Ottimizzazione guidata per la memoria**<br/> &nbsp; &nbsp; Creare effettivamente una tabella ottimizzata per la memoria da una tabella normale e inoltre eseguire la migrazione dei dati. |
| &nbsp; &nbsp; [11:28](https://www.youtube.com/watch?v=l5l5eophmK4&t=688) | Eseguire nuovamente la demo, notando un miglioramento della velocità di 45 volte. |
| <br/>E.&nbsp; [12:17](https://www.youtube.com/watch?v=l5l5eophmK4&t=737) | <br/>OLTP in memoria più facile da usare in SQL Server 2016 (rispetto alla versione 2014). |
| &nbsp; &nbsp; [12:43](https://www.youtube.com/watch?v=l5l5eophmK4&t=763) | Analisi semplificata per semplificare la migrazione delle app. |
| &nbsp; &nbsp; [13:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=783) | Minore complessità della migrazione delle app grazie a un maggiore supporto del linguaggio Transact-SQL, ad esempio con chiavi esterne e trigger. |
| &nbsp; &nbsp; [13:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=836) | Gestibilità migliorata.<br/> &nbsp; &nbsp; Ad esempio, modificare schema e indici, aggiornamento automatico delle statistiche. |
| <br/>F.&nbsp; [14:46](https://www.youtube.com/watch?v=l5l5eophmK4&t=886) | <br/>Maggiore scalabilità. |
| &nbsp; &nbsp; [15:12](https://www.youtube.com/watch?v=l5l5eophmK4&t=912) | Tabelle ottimizzate per la memoria di grandi dimensioni (fino a 2 TB per database). |
| &nbsp; &nbsp; [15:34](https://www.youtube.com/watch?v=l5l5eophmK4&t=934) | Scalabilità ancora migliore. |
| &nbsp; &nbsp; [16:41](https://www.youtube.com/watch?v=l5l5eophmK4&t=1001) | Fare di più con le risorse già disponibili. |
| <br/>G.&nbsp; [16:53](https://www.youtube.com/watch?v=l5l5eophmK4&t=1013) | <br/>Commenti finali. (Termina alle 17:32.) |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche  
 [Caratteristiche del database](../../relational-databases/database-features.md)  
  
  

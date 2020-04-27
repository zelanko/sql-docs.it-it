---
title: Database tempdb | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b1265d3ef58f6ef0946937b15411b0cb79a3c20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916883"
---
# <a name="tempdb-database"></a>Database tempdb
  Il database di sistema **tempdb** è una risorsa globale disponibile a tutti gli utenti connessi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene usata per contenere gli elementi seguenti:  
  
-   Oggetti utente temporanei creati in modo esplicito, ad esempio tabelle temporanee globali o locali, stored procedure temporanee, variabili di tabella o cursori.  
  
-   Oggetti interni creati dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], ad esempio tabelle di lavoro in cui archiviare i risultati intermedi delle operazioni di spooling o di ordinamento.  
  
-   Versioni di riga generate dalle transazioni di modifica dei dati in un database in cui viene usato il Read committed tramite isolamento del controllo delle versioni delle righe o transazioni di isolamento dello snapshot.  
  
-   Versioni di riga generate dalle transazioni di modifica dei dati per le caratteristiche, ad esempio le operazioni sugli indici online, la caratteristica MARS (Multiple Active Result Set) e i trigger AFTER.  
  
 In **tempdb** viene registrato un numero minimo di operazioni Consente il rollback delle transazioni. **tempdb** viene ricreato ogni volta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che viene avviato in modo che il sistema inizi sempre con una copia pulita del database. Poiché le tabelle e le stored procedure temporanee vengono eliminate automaticamente al momento della disconnessione e poiché al momento della chiusura del sistema non vi sono connessioni attive, Pertanto, non c'è mai niente in **tempdb** da salvare da una sessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra. Le operazioni di backup e ripristino non sono consentite in **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Proprietà fisiche di tempdb  
 Nella tabella seguente sono elencati i valori iniziali di configurazione dei dati e dei file di log di **tempdb** . Le dimensioni di questi file possono variare leggermente a seconda dell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Aumento di dimensioni del file|  
|----------|------------------|-------------------|-----------------|  
|Dati primari|tempdev|tempdb.mdf|Crescita automatica del 10% fino a quando il disco risulta pieno|  
|File di log|templog|templog.ldf|Aumento automatico delle dimensioni del 10% fino a un massimo di 2 TB|  
  
 Le dimensioni di **tempdb** possono influire sulle prestazioni di un sistema. Se, ad esempio, le dimensioni di **tempdb** sono troppo ridotte, è possibile che l'elaborazione del sistema sia troppo occupata con l'aumento automatico del database per supportare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]requisiti del carico di lavoro ogni volta che si avvia. Per evitare questo overhead, è possibile aumentare le dimensioni di **tempdb**.  
  
## <a name="performance-improvements-in-tempdb"></a>Miglioramenti delle prestazioni in tempdb  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]le prestazioni di **tempdb** sono state migliorate come segue:  
  
-   È possibile memorizzare nella cache tabelle temporanee e variabili di tabella. La memorizzazione nella cache consente di eseguire molto rapidamente le operazioni di eliminazione e creazione degli oggetti temporanei e di ridurre i problemi di contesa nell'allocazione delle pagine.  
  
-   Il protocollo di latch delle pagine di allocazione è stato migliorato. In questo modo è possibile ridurre il numero di latch di aggiornamento (UP) usati.  
  
-   L'overhead di registrazione per il database **tempdb** è stato ridotto. In questo modo si riduce l'utilizzo di banda per operazioni di I/O su disco nel file di log di **tempdb** .  
  
-   È stato migliorato l'algoritmo per l'allocazione di pagine miste in **tempdb** .  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Spostamento dei dati e dei file di log di tempdb  
 Per spostare i file di dati e di log di **tempdb** , vedere [spostare i database di sistema](system-databases.md).  
  
### <a name="database-options"></a>Opzioni di database  
 Nella tabella seguente sono elencati i valori predefiniti per ogni opzione di database del database **tempdb** e viene indicato se è possibile modificare l'opzione. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sì|  
|ANSI_NULL_DEFAULT|OFF|Sì|  
|ANSI_NULLS|OFF|Sì|  
|ANSI_PADDING|OFF|Sì|  
|ANSI_WARNINGS|OFF|Sì|  
|ARITHABORT|OFF|Sì|  
|AUTO_CLOSE|OFF|No|  
|AUTO_CREATE_STATISTICS|ON|Sì|  
|AUTO_SHRINK|OFF|No|  
|AUTO_UPDATE_STATISTICS|ON|Sì|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sì|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sì|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sì|  
|CURSOR_DEFAULT|GLOBAL|Sì|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> No<br /><br /> No|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sì|  
|DB_CHAINING|ON|No|  
|ENCRYPTION|OFF|No|  
|NUMERIC_ROUNDABORT|OFF|Sì|  
|PAGE_VERIFY|CHECKSUM per nuove installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE per aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sì|  
|PARAMETERIZATION|SEMPLICE|Sì|  
|QUOTED_IDENTIFIER|OFF|Sì|  
|READ_COMMITTED_SNAPSHOT|OFF|No|  
|RECOVERY|SEMPLICE|No|  
|RECURSIVE_TRIGGERS|OFF|Sì|  
|Opzioni relative a Service Broker|ENABLE_BROKER|Sì|  
|TRUSTWORTHY|OFF|No|  
  
 Per una descrizione di queste opzioni di database, vedere [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="restrictions"></a>Restrizioni  
 Nel database **tempdb** non è possibile eseguire le operazioni seguenti:  
  
-   Aggiunta di filegroup.  
  
-   Backup o ripristino del database.  
  
-   Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server.  
  
-   Modifica del proprietario del database. **tempdb** è di proprietà di **sa**.  
  
-   Creazione di uno snapshot del database.  
  
-   Eliminazione del database.  
  
-   Eliminazione dell'utente **Guest** dal database.  
  
-   Abilitazione dell'acquisizione dei dati delle modifiche.  
  
-   Partecipazione al mirroring del database.  
  
-   Rimozione del filegroup primario, del file di dati primario o del file di log.  
  
-   Ridenominazione del filegroup primario o del database.  
  
-   Esecuzione di DBCC CHECKALLOC.  
  
-   Esecuzione di DBCC CHECKCATALOG.  
  
-   Impostazione del database su OFFLINE.  
  
-   Impostazione del database o del filegroup primario su READ_ONLY.  
  
## <a name="permissions"></a>Autorizzazioni  
 Qualsiasi utente può creare oggetti temporanei in tempdb. Gli utenti possono accedere solo ai propri oggetti, a meno che non ottengano ulteriori autorizzazioni. È possibile revocare l'autorizzazione per la connessione a tempdb per impedire a un utente di utilizzarlo, tuttavia questa operazione non è consigliabile poiché in alcune operazioni di routine è richiesto l'utilizzo di tempdb.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Opzione SORT_IN_TEMPDB per gli indici](../indexes/indexes.md)  
  
 [Database di sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Spostare file del database](move-database-files.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Utilizzo di tempdb in SQL Server 2005](https://chresandro.wordpress.com/2014/09/29/working-with-tempdb-in-sql-server-2005/)  
  
  

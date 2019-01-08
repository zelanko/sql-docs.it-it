---
title: Tutte le funzionalità SQL Server supportate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 660515f10797e1f11fac22c1baf4ed74e9f67c0c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375033"
---
# <a name="supported-sql-server-features"></a>Funzionalità di SQL Server supportate
  In questo argomento vengono illustrate le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate o non supportate per l'utilizzo con oggetti ottimizzati per la memoria.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-supported-for-in-memory-oltp"></a>Funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate per OLTP in memoria  
 Le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicate di seguito sono supportate in un database contenente oggetti ottimizzati per la memoria, incluso un filegroup ottimizzato per la memoria.  
  
 Per informazioni sui tipi di dati supportati, vedere [Supported Data Types](supported-data-types-for-in-memory-oltp.md).  
  
-   Opzioni e operazioni supportate in tabelle ottimizzate per la memoria. Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
-   Opzioni e operazioni supportate in stored procedure compilate in modo nativo. Per altre informazioni, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
-   Capacità di accedere alle tabelle ottimizzate per la memoria utilizzando codice [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretato. Il codice [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretato fornisce la superficie di attacco equivalente all'accesso alle tabelle senza ottimizzazione per la memoria tramite stored procedure non compilate in modo nativo e utilizzando [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Per altre informazioni, vedere [Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
-   Controllo di più versioni e controllo della concorrenza ottimistica. Per altre informazioni, vedere [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
-   Backup e ripristino di un database che contiene filegroup di dati ottimizzati per la memoria. Per altre informazioni, vedere [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
-   Viste del catalogo, viste a gestione dinamica (DMV) ed eventi estesi per il supporto. Per altre informazioni, vedere [Viste di sistema, stored procedure, tipi di attesa e DMV per OLTP in memoria](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects. Per altre informazioni, vedere [Supporto di SQL Server Management Objects per OLTP in memoria](sql-server-management-objects-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (Indici per tabelle con ottimizzazione per la memoria). Per altre informazioni, vedere [Supporto di SQL Server Management Studio per OLTP in memoria](sql-server-management-studio-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Per ulteriori informazioni, vedere [Panoramica di SQL Server PowerShell](https://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx).  
  
-   Importazione ed esportazione dei dati per operazioni bulk tramite l'utilità bcp. Per altre informazioni, vedere [Importare ed esportare dati per operazioni bulk usando l'utilità bcp &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md).  
  
-   Recupero a seguito dell'arresto anomalo del sistema.  
  
-   Più contenitori in un filegroup di dati ottimizzato per la memoria per archiviare oggetti di OLTP in memoria e ridurre il tempo necessario per il pieno recupero dell'operatività (RTO, Recovery Time Objective).  
  
-   Calcolo del checksum e convalida tramite i blocchi del log delle transazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Nuovo hint di tabella SNAPSHOT. Per altre informazioni, vedere [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
-   Livello DB COMPAT.  
  
-   Database parzialmente indipendente. L'autenticazione di database indipendenti è supportata, Tuttavia, tutti gli oggetti OLTP in memoria sono contrassegnati come entità che interrompono l'indipendenza nel file DMV dm_db_uncontained_entities.  
  
-   Service Broker, con limitazioni. Non è possibile accedere a una coda da una stored procedure compilata in modo nativo, né a una coda in un database remoto in una transazione che accede a tabelle ottimizzate per la memoria.  
  
-   Clustering di failover: Come parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn, che offre le istanze del Cluster di Failover AlwaysOn usano la funzionalità di Windows Server Failover Clustering (WSFC) per fornire disponibilità elevata locale tramite ridondanza al cluster di failover di un livello di istanza del server istanza di (file FCI). Per altre informazioni, vedere [Istanze del cluster di failover Always On (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Integrazione con AlwaysOn: in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili diverse opzioni per creare la disponibilità elevata per un server o un database, incluso AlwaysOn. Per altre informazioni, vedere [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).  
  
-   Log shipping: Il log shipping di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di inviare automaticamente i backup del log delle transazioni da un database primario in un'istanza del server primario a uno o più database secondari in istanze separate del server secondario. Per altre informazioni, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
-   La replica transazionale in tabelle ottimizzate per la memoria nei sottoscrittori è supportata con alcune restrizioni. Per altre informazioni, vedere [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../replication/replication-to-memory-optimized-table-subscribers.md).  
  
-   Resource Governor: La funzionalità Resource Governor di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permette di gestire il carico di lavoro e l'utilizzo delle risorse di sistema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Resource Governor permette di specificare i limiti sulla quantità di CPU, I/O fisico e memoria che le richieste dell'applicazione in ingresso possono utilizzare. Per ulteriori informazioni, vedere [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) e [Resource Governor](../resource-governor/resource-governor.md).  
  
-   In OLTP in memoria sono presenti restrizioni per le tabelle codici supportate per le colonne di tipo (var)char nelle tabelle ottimizzate per la memoria e nelle regole di confronto supportate utilizzate negli indici e nelle stored procedure compilate in modo nativo. Per altre informazioni, vedere [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).  
  
-   Supporto BACPAC.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funzionalità non supportate per OLTP in memoria  
 Le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicate di seguito non sono supportate in un database contenente oggetti ottimizzati per la memoria, incluso un filegroup di dati ottimizzato per la memoria.  
  
|Funzionalità non supportata|Descrizione della funzionalità|  
|-------------------------|-------------------------|  
|Compressione dei dati per tabelle ottimizzate per la memoria.|È possibile utilizzare la funzionalità di compressione dei dati per comprimere i dati in un database e ridurre le dimensioni del database. Per altre informazioni, vedere [Data Compression](../data-compression/data-compression.md).|  
|Partizionamento di tabelle ottimizzate per la memoria e di indici HASH.|I dati di tabelle e indici partizionati vengono divisi in unità distribuibili tra più filegroup in un database. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).|  
|Transparent Data Encryption (TDE) sul filegroup di dati ottimizzato per la memoria di un database.|Transparent Data Encryption (TDE) esegue la crittografia e la decrittografia I/O in tempo reale dei file di dati e di log. Per altre informazioni sulla crittografia trasparente del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md).<br /><br /> È possibile abilitare TDE in un database contenente oggetti di OLTP in memoria. Se la funzionalità TDE è abilitata, i record del log di OLTP in memoria vengono crittografati. I file del checkpoint per le tabelle durevoli non vengono crittografati, anche se TDE è abilitata nel database.|  
|Replica|Le configurazioni di replica diverse dalla replica transazionale in tabelle ottimizzate per la memoria nei sottoscrittori non sono compatibili con tabelle o viste che fanno riferimento a tabelle ottimizzate per la memoria. La replica tramite sync_mode = 'database snapshot' non è supportata se è presente un filegroup ottimizzato per la memoria. Per altre informazioni, vedere [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../replication/replication-to-memory-optimized-table-subscribers.md).|  
|MARS (Multiple Active Result Sets)|MARS (Multiple Active Result Set) non è supportato con le tabelle ottimizzate per la memoria. L'errore può inoltre indicare l'utilizzo di un server collegato. Il server collegato può usare MARS. I server collegati non sono supportati con le tabelle ottimizzate per la memoria. Connettersi direttamente al server e al database che ospita le tabelle ottimizzate per la memoria.|  
|Mirroring|Il mirroring del database è una soluzione che consente di aumentare la disponibilità di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Ricompilazione del log|La ricompilazione del log, tramite il comando attach o l'istruzione ALTER DATABASE, non è supportata per i database che contengono un filegroup MEMORY_OPTIMIZED_DATA.|  
|Server collegato|Per altre informazioni, vedere [Server collegati &#40;Motore di database&#41;](../linked-servers/linked-servers-database-engine.md).|  
|Registrazione bulk|Indipendentemente dal modello di recupero del database, tutte le operazioni nelle tabelle durevoli ottimizzate per la memoria vengono sempre registrate completamente.|  
|Registrazione minima|La registrazione minima non è supportata dalle tabelle ottimizzate per la memoria. Per altre informazioni sulla registrazione minima, vedere [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md) e [Prerequisiti per la registrazione minima nell'importazione in blocco](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|Rilevamento modifiche|È possibile abilitare il rilevamento delle modifiche in un database con oggetti di OLTP in memoria, tuttavia le modifiche nelle tabelle ottimizzate per la memoria non vengono rilevate.|  
|trigger DDL|I trigger DDL a livello di database non sono supportati con tabelle di OLTP in memoria e stored procedure compilate in modo nativo.|  
|Change Data Capture (CDC)|Evitare di abilitare CDC in un database che include oggetti di OLTP in memoria, poiché impedisce determinate operazioni, ad esempio DROP.|  
|Indipendenza del database|L'indipendenza del database non è supportata in un database che include stored procedure compilate in modo nativo e tabelle ottimizzate per la memoria. Per altre informazioni, vedere [Contained Databases](../databases/contained-databases.md)|  
|Connessione di contesto:|L'accesso a tabelle ottimizzate per la memoria che usano la connessione del contesto dall'interno di stored procedure CLR non è supportato.|  
|Cursori|Keyset e cursori dinamici sulle query che accedono a tabelle ottimizzate per la memoria. Tali query diventano statiche e quindi di sola lettura.|  
|TABLESTAMP|TABLESTAMP non è supportato. Per altre informazioni, vedere [FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql).|  
|AUTO_CLOSE|AUTO_CLOSE non è supportato. Per altre informazioni, vedere [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md).|  
|Snapshot di database|Gli snapshot del database non sono supportati. Per altre informazioni, vedere [Snapshot del database &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md).|  
|DDL transazionale|La DDL transazionale non è supportata nella funzionalità OLTP in memoria.|  
|Notifiche degli eventi|Le notifiche degli eventi non sono supportate. Per altre informazioni, vedere [Event Notifications](../service-broker/event-notifications.md).|  
|Modalità fiber|La modalità fiber non è supportata con OLTP in memoria.|  
|Gestione basata su criteri.|Le modalità "impedisci esecuzione" e "solo log" della funzionalità di gestione basata su criteri non sono supportate. La presenza di tali criteri nel server può impedire la corretta esecuzione della DDL di OLTP in memoria. Le modalità Su richiesta e Su pianificazione sono supportate.|  
|Distribuzione/estrazione con DACFx.|La distribuzione/estrazione DAC Framework non è supportata nella funzionalità OLTP in memoria.|  
  
 Salvo alcune eccezioni, le transazioni tra database non sono supportate. Nella tabella seguente vengono descritti i casi supportati e le relative restrizioni. Vedere anche [Query tra database](cross-database-queries.md).  
  
|Database|Allowed|Descrizione|  
|---------------|-------------|-----------------|  
|Database utente, model e msdb|No|Query e transazioni tra database non sono supportate.<br /><br /> Query e transazioni che accedono a tabelle ottimizzate per la memoria o a stored procedure compilate in modo nativo non possono accedere ad altri database, ad eccezione del master del database di sistema (accesso in sola lettura) e di tempdb.|  
|Database delle risorse e tempdb|Yes|Non vi sono restrizioni per le transazioni tra database che, oltre a un singolo database utente, utilizzano solo un database delle risorse e tempdb.|  
|master|Sola lettura|Il commit delle transazioni tra database che riguardano OLTP in memoria e il database master non viene eseguito se sono incluse scritture nel database master. Le transazioni tra database che eseguono solo letture dal master e utilizzano un solo database utente sono consentite.|  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di SQL Server per OLTP in memoria](sql-server-support-for-in-memory-oltp.md)  
  
  

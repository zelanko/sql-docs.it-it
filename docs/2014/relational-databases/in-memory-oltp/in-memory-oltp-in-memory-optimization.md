---
title: OLTP in memoria (ottimizzazione in memoria) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: rothja
ms.author: jroth
ms.openlocfilehash: 22faed7d9505c1ad487b5300a46a565379512091
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050158"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>OLTP in memoria (ottimizzazione per la memoria)

  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], una novità di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] , può migliorare significativamente le prestazioni delle applicazioni di database OLTP. [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] è un motore di database ottimizzato per la memoria integrato nel motore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ottimizzato per OLTP.

|||
|-|-|
|![Macchina virtuale di Azure](../../master-data-services/media/azure-virtual-machine.png "Macchina virtuale di Azure")|Per provare SQL Server 2016, Iscriversi a Microsoft Azure e quindi fare clic **[qui](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2017-ws2019?tab=Overview)** per creare rapidamente una macchina virtuale con SQL Server 2016 già installato. Al termine, è possibile eliminare la macchina virtuale.|

 Per usare [!INCLUDE[hek_2](../../../includes/hek-2-md.md)], definire una tabella usata molto frequentemente come tabella con ottimizzazione per la memoria. Le tabelle con ottimizzazione per la memoria sono completamente transazionali, durevoli e sono accessibili tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)] allo stesso modo delle tabelle basate su disco. Una query può fare riferimento sia alle tabelle ottimizzate per la memoria che alle tabelle basate su disco. Una transazione può aggiornare i dati nelle tabelle ottimizzate per la memoria e in quelle basate su disco. Le stored procedure che fanno riferimento solo alle tabelle ottimizzate per la memoria possono essere compilate in modo nativo nel codice macchina per migliorare ulteriormente le prestazioni. Il motore di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] è progettato per una concorrenza delle sessioni estremamente alta per il tipo di transazioni OLTP supportate da un livello intermedio con elevata scalabilità orizzontale. Per ottenere ciò, vengono usati strutture di dati prive di latch e un controllo della concorrenza ottimistica con più versioni. Il risultato è prevedibile, una bassa latenza inferiore a un millisecondo e una velocità effettiva elevata con scalabilità lineare per le transazioni di database. Il miglioramento effettivo delle prestazioni dipende da molti fattori, ma in genere si possono ottenere miglioramenti delle prestazioni da 5 a 20 volte.

 La seguente tabelle riepiloga i modelli di carico di lavoro che potrebbero trarre enorme vantaggio dall'uso di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]:

|Scenario di implementazione|Scenario di implementazione|Vantaggi di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]|
|-----------------------------|-----------------------------|-------------------------------------|
|Elevata frequenza di inserimento dati da più connessioni simultanee.|Principalmente archiviazione di operazioni solo di accodamento.<br /><br /> Non è possibile far fronte al carico di lavoro di inserimento.|Eliminare i conflitti.<br /><br /> Ridurre la registrazione.|
|Prestazioni di lettura e scalabilità con inserimenti e aggiornamenti di batch periodici.|Operazioni di lettura a elevate prestazioni, soprattutto quando ogni richiesta del server ha più operazioni di lettura da eseguire.<br /><br /> Non è possibile soddisfare i requisiti di scalabilità verticale.|Eliminare i conflitti all'arrivo di nuovi dati.<br /><br /> Recupero di dati con latenza più bassa.<br /><br /> Ridurre il tempo di esecuzione del codice.|
|Elaborazione intensa della logica di business nel server di database.|Carico di lavoro di inserimento, aggiornamento ed eliminazione.<br /><br /> Calcolo intenso all'interno delle stored procedure.<br /><br /> Conflitti di lettura e scrittura.|Eliminare i conflitti.<br /><br /> Ridurre il tempo di esecuzione del codice in modo da ottenere una riduzione della latenza e un miglioramento della velocità effettiva.|
|Bassa latenza.|Richiedere transazioni aziendali a bassa latenza che le tipiche soluzioni di database non riescono a ottenere.|Eliminare i conflitti.<br /><br /> Ridurre il tempo di esecuzione del codice.<br /><br /> Esecuzione del codice a bassa latenza.<br /><br /> Recupero di dati efficiente.|
|Gestione dello stato delle sessioni.|Operazioni di inserimento e aggiornamento e ricerche di punti frequenti.<br /><br /> Caricamento a elevata scalabilità da numerosi server Web senza stato.|Eliminare i conflitti.<br /><br /> Recupero di dati efficiente.<br /><br /> Riduzione o rimozione di operazioni I/O facoltative quando si usano tabelle non durevoli.|

 Per ulteriori informazioni sugli scenari [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] in cui si otterranno i maggiori vantaggi in termini di prestazioni, vedere [OLTP in memoria: considerazioni sulla migrazione e sui modelli di carico di lavoro comuni](https://msdn.microsoft.com/library/dn673538.aspx).

 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] migliora le prestazioni in modo ottimale in OLTP con transazioni con esecuzione rapida.

 I modelli di programmazione migliorati da [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] includono gli scenari di concorrenza, le ricerche di punti, i carichi di lavoro con molti inserimenti e aggiornamenti e la logica di business nelle stored procedure.

 Grazie all'integrazione con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è possibile avere sia tabelle ottimizzate per la memoria sia tabelle basate su disco nello stesso database e query in entrambi i tipi di tabelle.

 In [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] sono presenti limitazioni nella superficie di attacco di [!INCLUDE[tsql](../../../includes/tsql-md.md)] supportata per [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].

 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] consente di ottenere miglioramenti significativi di scalabilità e delle prestazioni usando gli elementi seguenti:

-   Algoritmi ottimizzati per accedere ai dati residenti in memoria.

-   Controllo della concorrenza ottimistica che elimina i blocchi logici.

-   Oggetti senza blocco che eliminano tutti i latch e i blocchi fisici. I thread che eseguono lavoro transazionale non usano blocchi o latch per il controllo della concorrenza.

-   Stored procedure compilate in modo nativo che comportano un miglioramento significativo delle prestazioni rispetto alle stored procedure interpretate quando si accede a una tabella ottimizzata per la memoria.

> [!IMPORTANT]
>  Alcune modifiche di sintassi alle tabelle e alle stored procedure verranno richieste per usare [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]. Per altre informazioni, vedere [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md). Prima di eseguire la migrazione di una tabella basata su disco in una tabella ottimizzata per la memoria, leggere [Determinare se una tabella o una stored procedure deve essere trasferita a OLTP in memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) per verificare quali tabelle e stored procedure trarranno beneficio da [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].

## <a name="in-this-section"></a>Contenuto della sezione
 In questa sezione vengono fornite informazioni sui seguenti concetti:

|Argomento|Descrizione|
|-----------|-----------------|
|[Requisiti per l'utilizzo di tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)|Vengono descritti i requisiti hardware e software e le linee guida per l'utilizzo di tabelle ottimizzate per la memoria.|
|[Uso di OLTP in memoria in un ambiente di VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|Illustra l'uso di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] in un ambiente virtualizzato.|
|[Esempi di codice di OLTP in memoria](in-memory-oltp-code-samples.md)|Sono contenuti esempi di codice che illustrano come creare e usare una tabella ottimizzata per la memoria.|
|[Tabelle ottimizzate per la memoria](memory-optimized-tables.md)|Vengono introdotte le tabelle ottimizzate per la memoria.|
|[Variabili di tabella con ottimizzazione per la memoria](../../database-engine/memory-optimized-table-variables.md)|Esempio di codice in cui viene mostrato come usare una variabile di tabella ottimizzata per la memoria anziché una variabile di tabella tradizionale per ridurre l'utilizzo di tempdb.|
|[Indici in tabelle con ottimizzazione per la memoria](../../database-engine/indexes-on-memory-optimized-tables.md)|Vengono introdotti indici ottimizzati per la memoria.|
|[stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)|Vengono illustrate le stored procedure compilate in modo nativo.|
|[Gestione della memoria per OLTP in memoria](../../database-engine/managing-memory-for-in-memory-oltp.md)|Informazioni e gestione dell'utilizzo della memoria nel sistema.|
|[Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)|Vengono illustrati i file di dati e differenziali in cui vengono archiviate le informazioni sulle transazioni nelle tabelle ottimizzate per la memoria.|
|[Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](restore-and-recovery-of-memory-optimized-tables.md)|Descrive le operazioni di backup, ripristino e recupero delle tabelle ottimizzate per la memoria.|
|[Supporto di Transact-SQL per OLTP in memoria](transact-sql-support-for-in-memory-oltp.md)|Descrive il supporto di [!INCLUDE[tsql](../../../includes/tsql-md.md)] per [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|
|[Supporto della disponibilità elevata per i database OLTP in memoria](high-availability-support-for-in-memory-oltp-databases.md)|Descrive i gruppi di disponibilità e il clustering di failover in [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|
|[Supporto di SQL Server per OLTP in memoria](sql-server-support-for-in-memory-oltp.md)|Elenco della sintassi e delle funzionalità nuove e aggiornate per il supporto di tabelle ottimizzate per la memoria.|
|[Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)|Viene illustrato come eseguire la migrazione di tabelle basate su disco in tabelle ottimizzate per la memoria.|

 Altre informazioni su [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] sono disponibili in:

-   [Microsoft? SQL Server?? Guida del prodotto 2014](https://www.microsoft.com/download/confirmation.aspx?id=39269)

-   [Blog di OLTP in memoria](https://cloudblogs.microsoft.com/sqlserver/2013/06/26/sql-server-2014-in-memory-technologies-blog-series-introduction/)

-   [OLTP in memoria: considerazioni sulla migrazione e sui modelli di carico di lavoro comuni](https://msdn.microsoft.com/library/dn673538.aspx)

-   [Panoramica dei meccanismi interni OLTP in memoria di SQL Server](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
    <!--
         (https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
         (/sql/relational-databases/in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016?view=sql-server-2016)
    -->

## <a name="see-also"></a>Vedere anche
 [Funzionalità di database](../database-features.md)



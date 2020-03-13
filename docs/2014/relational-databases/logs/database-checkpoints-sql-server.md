---
title: Checkpoint di database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33f85b2f1cd8b259e46851aab818b258a6d78291
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289399"
---
# <a name="database-checkpoints-sql-server"></a>Checkpoint di database (SQL Server)
  In questo argomento viene fornita una panoramica dei checkpoint del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un *Checkpoint* crea un punto valido noto da cui [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] può iniziare ad applicare le modifiche contenute nel log durante il recupero dopo un arresto imprevisto o un arresto anomalo.  
  
  
##  <a name="Overview"></a>Panoramica dei checkpoint  
 Per motivi correlati alle prestazioni, tramite il [!INCLUDE[ssDE](../../includes/ssde-md.md)] vengono apportate modifiche alle pagine del database in memoria, nella cache buffer, ma queste pagine non vengono scritte su disco dopo ogni modifica. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] pubblica periodicamente un checkpoint su ogni database. Un *checkpoint* scrive le pagine modificate in memoria correnti, note come pagine *dirty*e le informazioni sul log delle transazioni dalla memoria sul disco e registra le informazioni sul log delle transazioni.  
  
 Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] supporta molti tipi di checkpoint: automatici, indiretti, manuali e interni. Nella tabella seguente vengono riepilogati i tipi di checkpoint.  
  
|Nome|[!INCLUDE[tsql](../../includes/tsql-md.md)] Interfaccia|Descrizione|  
|----------|----------------------------------|-----------------|  
|Automatico|EXEC sp_configure **'`recovery interval`','*`seconds`*'**|Emesso automaticamente in background per rispettare il limite di tempo superiore suggerito dall'opzione `recovery interval` di configurazione del server. I checkpoint automatici vengono eseguiti fino al completamento.  I checkpoint automatici sono limitati in base al numero di scritture in sospeso e al fatto che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] rilevi o meno un aumento della latenza di scrittura superiore ai 20 millisecondi.<br /><br /> Per altre informazioni, vedere [Configurare l'opzione di configurazione del server recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).|  
|Indiretto|ALTER DATABASE... Imposta TARGET_RECOVERY_TIME **=** _TARGET_RECOVERY_TIME_ {secondi &#124; minuti}|Emesso in background per rispettare un tempo di recupero di destinazione specificato dall'utente per un determinato database. Il tempo di recupero di destinazione predefinito è 0 che comporta l'utilizzo di un approccio euristico dei checkpoint automatici nel database. Se si utilizza ALTER DATABASE per impostare TARGET_RECOVERY_TIME su >0, viene utilizzato questo valore e non l'intervallo di recupero specificato per l'istanza del server.<br /><br /> Per altre informazioni, vedere [Modificare il tempo di recupero di riferimento di un database &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md).|  
|Manuale|CHECKPOINT [ *checkpoint_duration* ]|Emesso quando si esegue un comando CHECKPOINT [!INCLUDE[tsql](../../includes/tsql-md.md)] . Il checkpoint manuale si verifica nel database corrente per la connessione. Per impostazione predefinita, i checkpoint manuali vengono eseguiti fino al completamento. La limitazione funziona come per i checkpoint automatici.  Facoltativamente, il parametro *checkpoint_duration* specifica una quantità di tempo richiesta, in secondi, per il completamento del checkpoint.<br /><br /> Per altre informazioni, vedere [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql).|  
|Interno|No.|Emesso da varie operazioni del server quali backup e creazione dello snapshot del database per garantire che le immagini del disco corrispondano allo stato corrente del log.|  
  
> [!NOTE]  
>  L'opzione di impostazione avanzata `-k` di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente a un amministratore del database di limitare il comportamento di I/O del checkpoint in base alla velocità effettiva del sottosistema di I/O per alcuni tipi di checkpoint. L' `-k` opzione di installazione si applica ai checkpoint automatici ed eventuali checkpoint manuali e interni altrimenti non limitati.  
  
 Per i checkpoint automatici, manuali e interni, solo le modifiche apportate dopo l'ultimo checkpoint devono essere sottoposte a rollforward durante il recupero del database. Ne consegue una riduzione del tempo necessario per recuperare un database.  
  
> [!IMPORTANT]  
>  Le transazioni di cui non è stato eseguito il commit con esecuzione prolungata aumentano il tempo di recupero per tutti i tipi di checkpoint.  
  
  
  
###  <a name="InteractionBwnSettings"></a>Interazione tra le opzioni di TARGET_RECOVERY_TIME è intervallo di recuperò  
 Nella tabella seguente viene riepilogata l'interazione tra l'impostazione del **sp_configure "`recovery interval`"** a livello di server e il database ALTER database... Impostazione TARGET_RECOVERY_TIME.  
  
|target_recovery_time|'intervallo di recupero'|Tipo di checkpoint utilizzato|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|checkpoint automatici il cui intervallo di recupero di destinazione è pari a 1 minuto.|  
|0|>0|Checkpoint automatici il cui intervallo di recupero di destinazione è specificato dall'impostazione definita dall'utente dell'opzione **sp_configure intervallo di recupero**.|  
|>0|Non applicabile.|Checkpoint indiretti il cui tempo di recupero di destinazione è determinato dall'impostazione TARGET_RECOVERY_TIME, espresso in secondi.|  
  
###  <a name="AutomaticChkpt"></a>Checkpoint automatici  
 Viene eseguito un checkpoint automatico ogni volta che il numero di record di log raggiunge il [!INCLUDE[ssDE](../../includes/ssde-md.md)] numero di stime che può elaborare durante il periodo di tempo `recovery interval` specificato nell'opzione di configurazione del server. In ogni database senza un tempo di recupero di destinazione definito dall'utente, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera checkpoint automatici. La frequenza di checkpoint automatici dipende dall'opzione di configurazione `recovery interval` avanzata del server, che specifica il tempo massimo che una determinata istanza del server deve utilizzare per recuperare un database durante un riavvio del sistema. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] valuta il numero massimo di record di log che può elaborare nell'intervallo di recupero. Quando un database che utilizza i checkpoint automatici raggiunge il numero massimo specificato di record di log, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] pubblica un checkpoint sul database. L'intervallo di tempo tra checkpoint automatici può essere estremamente variabile. In un database con un considerevole carico di lavoro di transazioni si verificheranno checkpoint più frequenti rispetto a un database utilizzato principalmente per le operazioni in sola lettura.  
  
 Inoltre, in base al modello di recupero con registrazione minima, viene messo in coda un checkpoint automatico se il log è pieno al 70 percento.  
  
 In base al modello di recupero con registrazione minima, a meno che alcuni fattori non ritardino il troncamento del log, un checkpoint automatico tronca la sezione inutilizzata del log delle transazioni. Al contrario, in base ai modelli di recupero con registrazione minima delle operazioni bulk e con registrazione completa, dopo avere stabilito una catena di backup del log, i checkpoint automatici non causano il troncamento del log. Per altre informazioni, vedere [Log delle transazioni &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 Dopo un arresto anomalo del sistema, la quantità di tempo necessaria per recuperare un database dipende in larga misura dalla quantità di I/O casuale necessario per ripristinare le pagine dirty al momento dell'arresto anomalo del sistema. Ciò significa che l' `recovery interval` impostazione non è affidabile. Non è in grado di determinare una durata accurata del recupero. Inoltre, quando è in corso un checkpoint automatico, l'attività di I/O generale per i dati aumenta in modo significativo e imprevedibile.  
  
  
####  <a name="PerformanceImpact"></a>Conseguenze dell'intervallo di recupero sulle prestazioni di ripristino  
 Per un sistema di elaborazione delle transazioni online (OLTP) che utilizza `recovery interval` transazioni brevi, rappresenta il fattore principale che determina il tempo di recupero. Tuttavia, l' `recovery interval` opzione non influisce sul tempo necessario per annullare una transazione con esecuzione prolungata. Il ripristino di un database con una transazione con esecuzione prolungata può richiedere molto più tempo rispetto `recovery interval` a quello specificato nell'opzione. Se, ad esempio, una transazione con esecuzione prolungata impiega due ore per eseguire gli aggiornamenti prima che l'istanza del server venga disabilitata, il `recovery interval` recupero effettivo richiede molto più tempo del valore per recuperare la transazione lunga. Per informazioni sull'impatto di una transazione con esecuzione prolungata sul tempo di recupero, vedere [Log delle transazioni &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 In genere, i valori predefiniti forniscono prestazioni di recupero ottimali. Tuttavia, la modifica dell'intervallo di recupero potrebbe migliorare le prestazioni nelle circostanze seguenti:  
  
-   Se il recupero richiede regolarmente più di 1 minuto quando non viene eseguito il rollback delle transazioni con esecuzione prolungata.  
  
-   Se si nota che checkpoint frequenti riducono le prestazioni su un database.  
  
 Se si decide di aumentare l'impostazione `recovery interval`, è consigliabile aumentarla gradualmente di piccoli incrementi e valutare l'effetto di ogni aumento incrementale sulle prestazioni del recupero. Questo approccio è importante perché man mano `recovery interval` che l'impostazione aumenta, il recupero del database richiede molto più tempo per il completamento. Se, ad esempio, si `recovery interval` modifica 10, il recupero richiede circa 10 volte più tempo del `recovery interval` completamento rispetto a quando è impostato su zero.  
  
  
###  <a name="IndirectChkpt"></a>Checkpoint indiretti  
 I checkpoint indiretti, nuovi in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], offrono un'alternativa a livello di database configurabile ai checkpoint automatici. In caso di un arresto anomalo del sistema, i checkpoint indiretti consentono un tempo di recupero potenzialmente più veloce e più prevedibile rispetto ai checkpoint automatici. I checkpoint indiretti offrono i vantaggi riportati di seguito:  
  
-   Un carico di lavoro transazionale online su un database configurato per i checkpoint indiretti potrebbe subire un calo delle prestazioni. I checkpoint indiretti assicurano che il numero di pagine dirty è inferiore a una determinata soglia, in modo che il recupero del database viene completato entro il tempo di recupero di riferimento. A differenza dei checkpoint indiretti che usano il numero di pagine dirty, l'opzione di configurazione recovery interval usa il numero di transazioni per determinare il tempo di recupero. Quando i checkpoint indiretti sono abilitati per un database che riceve un numero elevato di operazioni DML, il writer in background può iniziare a scaricare i buffer dirty su disco in modo intensivo per garantire che il tempo necessario per eseguire il recupero non superi il tempo di recupero di riferimento impostato per il database. Questo può causare in determinati sistemi ulteriore attività di I/O che può comportare un collo di bottiglia delle prestazioni se il sottosistema del disco opera al di sopra o in prossimità della soglia di I/O.  
  
-   I checkpoint indiretti consentono di controllare in modo affidabile il tempo di recupero del database tramite factoring del costo di operazioni di I/O casuali durante REDO. In questo modo si consente a un'istanza del server di rimanere entro il limite superiore per i tempi di recupero per un determinato database, tranne quando una transazione con esecuzione prolungata causa tempi UNDO eccessivi.  
  
-   I checkpoint indiretti riducono i picchi di I/O correlati ai checkpoint scrivendo continuamente pagine dirty su disco in background.  
  
 Tuttavia, un carico di lavoro transazionale online su un database configurato per i checkpoint indiretti potrebbe subire un calo delle prestazioni. Questo perché il writer in background utilizzato dai checkpoint indiretti aumenta talvolta il carico di scrittura totale di un'istanza del server.  
  
  
###  <a name="EventsCausingChkpt"></a>Checkpoint interni  
 I checkpoint interni vengono generati da vari componenti server per garantire che le immagini sul disco corrispondano allo stato corrente del log. I checkpoint interni vengono generati in risposta agli eventi seguenti:  
  
-   Vengono aggiunti o rimossi file di database utilizzando l'istruzione ALTER DATABASE.  
  
-   Viene eseguito un backup del database.  
  
-   Viene creato uno snapshot del database, in modo esplicito o internamente per CHECK DBCC.  
  
-   Viene eseguita un'attività che richiede la chiusura di un database. Ad esempio, AUTO_CLOSE è impostata su ON e la connessione al database dell'ultimo utente viene chiusa, oppure viene eseguita una modifica a un'opzione di database che richiede un riavvio del database.  
  
-   Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene arrestata in seguito all'arresto del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER). Entrambe le azioni causano un checkpoint in ogni database dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Impostazione della modalità offline per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per modificare l'intervallo di recupero in un'istanza del server**  
  
-   [Configurare l'opzione di configurazione del server recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **Per configurare checkpoint indiretti su un database**  
  
-   [Modificare il tempo di recupero di riferimento di un database &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **Per emettere un checkpoint manuale su un database**  
  
-   [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)  
  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Architettura fisica del log delle transazioni](https://technet.microsoft.com/library/ms179355.aspx) (in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] libri oline)  
  
  
## <a name="see-also"></a>Vedere anche  
 [Log delle transazioni &#40;SQL Server&#41;](the-transaction-log-sql-server.md)  
  
  

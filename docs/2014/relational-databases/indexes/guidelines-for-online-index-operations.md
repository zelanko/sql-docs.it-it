---
title: Linee guida per le operazioni sugli indici online | Microsoft Docs
ms.custom: ''
ms.date: 11/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2f7a25a4a6a4bb6b8f153a8b04b47aeb542265c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356198"
---
# <a name="guidelines-for-online-index-operations"></a>Linee guida per operazioni di indice online
  Quando si eseguono operazioni sugli indici online sono da ritenersi valide le linee guida seguenti:  
  
-   Gli indici cluster devono essere creati, ricompilati o eliminati offline se la tabella sottostante contiene i seguenti tipi di dati LOB (large object): `image`, **ntext**, e `text`.  
  
-   Non è possibile creare, ricompilare o eliminare online indici su tabelle temporanee locali. Questa limitazione non è valida per gli indici su tabelle temporanee globali.  
  
> [!NOTE]  
>  Le operazioni sugli indici online sono disponibili solo in alcune edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Nella tabella seguente sono riportate le operazioni sugli indici che è possibile eseguire online e gli indici che sono esclusi da queste operazioni online. Sono inoltre incluse ulteriori limitazioni.  
  
|Operazione su indice online|Indici esclusi|Altre limitazioni|  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|Indice cluster disabilitato o vista indicizzata disabilitata<br /><br /> Indice XML <br /><br />Indice columnstore<br /><br /> Indice di una tabella temporanea locale|L'operazione può avere esito negativo se la tabella contiene un indice escluso e si utilizza la parola chiave ALL.<br /><br /> Sono applicabili ulteriori restrizioni nella ricompilazione di indici disabilitati. Per altre informazioni, vedere [Disabilitazione di indici e vincoli](disable-indexes-and-constraints.md).|  
|CREATE INDEX|Indice XML<br /><br /> Indice cluster univoco iniziale su una vista<br /><br /> Indice di una tabella temporanea locale||  
|CREATE INDEX WITH DROP_EXISTING|Indice cluster disabilitato o vista indicizzata disabilitata<br /><br /> Indice di una tabella temporanea locale<br /><br /> Indice XML||  
|DROP INDEX|Indice disabilitato<br /><br /> Indice XML<br /><br /> Indice non cluster<br /><br /> Indice di una tabella temporanea locale|Non è possibile specificare più indici in una singola istruzione.|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY o UNIQUE)|Indice di una tabella temporanea locale<br /><br /> Indice cluster|È consentito l'utilizzo di una sola clausola secondaria alla volta. Ad esempio, non è possibile aggiungere ed eliminare vincoli PRIMARY KEY o UNIQUE nella stessa istruzione ALTER TABLE.|  
||||  
  
 Non è possibile modificare, troncare o eliminare la tabella sottostante mentre è in corso un'operazione su un indice online.  
  
 L'impostazione di un'opzione online (ON oppure OFF) specificata durante la creazione o l'eliminazione di un indice cluster viene applicata a tutti gli indici non cluster che devono essere ricompilati. Ad esempio, se l'indice cluster viene compilato online utilizzando CREATE INDEX WITH DROP_EXISTING, ONLINE=ON, anche tutti gli indici non cluster associati vengono ricreati online.  
  
 Quando si crea o si ricompila un indice UNIQUE online, il generatore dell'indice e una transazione utente simultanea potrebbero tentare di inserire la stessa chiave, causando una violazione di univocità. Se una riga immessa da un utente viene inserita nel nuovo indice (destinazione) prima che la riga originale della tabella di origine venga spostata nel nuovo indice, l'operazione sull'indice online avrà esito negativo.  
  
 Un'operazione su un indice online può in rari casi provocare un deadlock quando interagisce con aggiornamenti al database a causa di attività dell'utente o dell'applicazione. In questi rari casi, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selezionerà l'attività dell'utente o dell'applicazione come vittima del deadlock.  
  
 È possibile eseguire operazioni DDL sugli indici online simultanee sulla stessa tabella o vista solo quando si stanno creando più indici nuovi non cluster oppure si stanno riorganizzando indici non cluster. Qualsiasi altra operazione sugli indici online eseguita nello stesso istante avrà esito negativo. Ad esempio, non è possibile creare un nuovo indice online durante la ricompilazione di un indice online esistente sulla stessa tabella.  
  
 Non è possibile eseguire un'operazione online se un indice contiene una colonna di tipo di oggetti di grandi dimensioni e nella stessa transazione sono presenti operazioni di aggiornamento prima di questa operazione online. Per risolvere questo problema, posizionare l'operazione online all'esterno della transazione o prima degli aggiornamenti all'interno della transazione.  
  
## <a name="disk-space-considerations"></a>Considerazioni sullo spazio su disco  
 I requisiti dello spazio su disco sono generalmente gli stessi per operazioni sugli indici online e offline. Un'eccezione è costituita dallo spazio su disco aggiuntivo richiesto dall'indice di mapping temporaneo. Questo indice temporaneo è utilizzato nelle operazioni sugli indici online che creano, ricompilano o eliminano un indice cluster. L'eliminazione di un indice cluster online richiede lo stesso spazio che è necessario per la creazione di un indice cluster online. Per altre informazioni, vedere [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni  
 Sebbene le operazioni sugli indici online consentano l'esecuzione di attività simultanee di aggiornamento utente, le operazioni sugli indici impiegheranno più tempo se l'attività di aggiornamento genera un notevole carico. Le operazioni sugli indici online saranno generalmente più lente delle operazioni sugli indici offline equivalenti, indipendentemente dal livello di attività di aggiornamento simultanee.  
  
 Dato che durante le operazioni sugli indici online vengono mantenute sia la struttura di origine che quella di destinazione, l'utilizzo di risorse per l'inserimento, l'aggiornamento e l'eliminazione delle transazioni viene aumentato, potenzialmente fino al doppio. Ciò può causare una riduzione delle prestazioni e un maggior utilizzo di risorse durante l'operazione sugli indici, specialmente del tempo CPU. Le operazioni sugli indici online vengono registrate completamente.  
  
 Sebbene le operazioni online siano consigliabili, è opportuno valutare l'ambiente e i requisiti specifici, in base ai quali l'esecuzione delle operazioni sugli indici offline potrebbe essere la soluzione ottimale. In quest'ultimo caso gli utenti avrebbero un accesso limitato ai dati durante l'operazione, la quale però terminerebbe più rapidamente e utilizzerebbe meno risorse.  
  
 Nei computer multiprocessore che eseguono [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]le istruzioni per gli indici, analogamente ad altre query, possono utilizzare più processori per eseguire le operazioni di analisi e ordinamento associate all'istruzione. È possibile utilizzare l'opzione dell'indice MAXDOP per controllare il numero di processori dedicati all'operazione di indice online. In questo modo è possibile bilanciare le risorse utilizzate dall'operazione sugli indici con quelle occupate dagli utenti simultanei. Per altre informazioni, vedere [Configurazione di operazioni parallele sugli indici](configure-parallel-index-operations.md). Per altre informazioni sulle edizioni di SQL Server che supportano parallelo le operazioni indicizzate, vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Poiché al termine dell'esecuzione dell'operazione sugli indici viene mantenuto un blocco S o Sch-M, è necessario prestare particolare attenzione quando si esegue un'operazione sugli indici online all'interno di una transazione utente esplicita, ad esempio un blocco BEGIN TRANSACTION...COMMIT. Una tale operazione causa il mantenimento del blocco fino alla fine della transazione, impedendo quindi la concorrenza degli utenti.  
  
 La ricompilazione degli indici online può aumentare la frammentazione quando è consentita l'esecuzione con le opzioni `MAX DOP > 1` e `ALLOW_PAGE_LOCKS = OFF` . Per altre informazioni, vedere [funzionamento: Ricompilazione dell'indice online - può provocare una maggiore frammentazione](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx).  
  
## <a name="transaction-log-considerations"></a>Considerazioni sul log delle transazioni  
 Operazioni sugli indici su larga scala, eseguite online oppure offline, possono generare volumi di dati elevati i quali possono esaurire rapidamente lo spazio disponibile nel log delle transazioni. Per garantire la possibilità di eseguire il rollback dell'operazione sugli indici, non è possibile troncare il log delle transazioni fino al completamento dell'operazione. È tuttavia possibile eseguire il backup del log durante l'operazione sugli indici. È pertanto necessario che il log delle transazioni abbia spazio sufficiente per archiviare sia le transazioni dell'operazione sugli indici sia tutte le transazioni utente simultanee per l'intera durata dell'operazione sugli indici. Per altre informazioni, vedere [Spazio su disco per il log delle transazioni per operazioni sugli indici](transaction-log-disk-space-for-index-operations.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 [Funzionamento delle operazioni sugli indici online](how-online-index-operations-work.md)  
  
 [Eseguire operazioni online sugli indici](perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
  

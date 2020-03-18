---
title: Elaborazione del grafico
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b0934562f2f0ff1a2dd3ec8df1ed15f10d955ee
ms.sourcegitcommit: 6e7696a169876eb914f79706d022451a1213eb6b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428152"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Elaborazione di grafi con SQL Server e il database SQL di Azure
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]offre funzionalità di database a grafo per modellare relazioni molti-a-molti. Le relazioni tra grafi sono integrate in [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e ricevono i vantaggi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] derivanti dall'utilizzo di come sistema di gestione di database di base.


## <a name="what-is-a-graph-database"></a>Che cos'è un database a grafo?  
Un database a grafo è una raccolta di nodi (o vertici) e archi (o relazioni). Un nodo rappresenta un'entità (ad esempio, una persona o un'organizzazione) e un arco rappresenta una relazione tra i due nodi che collega (ad esempio, mi piace o amici). Sia i nodi che i bordi possono avere proprietà associate. Ecco alcune funzionalità che rendono univoco un database a grafo:  
-    Gli archi o relazioni sono entità di prima classe in un Database a grafo e possono avere attributi o proprietà associate ad essi. 
-    Un singolo arco può collegare in modo flessibile più nodi in un Database a grafo.
-    È possibile esprimere facilmente criteri di ricerca e query di navigazione a più hop.
-    È possibile esprimere facilmente chiusura transitiva e query polimorfiche.

## <a name="when-to-use-a-graph-database"></a>Quando utilizzare un database a grafo

Un database relazionale può ottenere qualsiasi elemento di un database Graph. Tuttavia, un database a grafo rende più semplice esprimere determinati tipi di query. Inoltre, con ottimizzazioni specifiche, alcune query possono garantire prestazioni migliori. La scelta di un database relazionale o a grafo si basa sui fattori seguenti:  
-    L'applicazione contiene dati gerarchici. Il tipo di dati HierarchyID può essere utilizzato per implementare gerarchie, ma presenta alcune limitazioni. Ad esempio, non consente di archiviare più elementi padre per un nodo.
-    L'applicazione dispone di relazioni molti-a-molti complesse. Quando l'applicazione si evolve, vengono aggiunte nuove relazioni.
-    È necessario analizzare relazioni e dati interconnessi.

## <a name="graph-features-introduced-in-sssqlv14"></a>Caratteristiche del grafo introdotte in[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Si sta iniziando ad aggiungere estensioni di grafo a SQL Server per semplificare l'archiviazione e l'esecuzione di query sui dati del grafo. Le funzionalità seguenti sono state introdotte nella prima versione. 


### <a name="create-graph-objects"></a>Creare oggetti Graph
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]le estensioni consentiranno agli utenti di creare tabelle node o Edge. Sia i nodi che i bordi possono avere proprietà associate. Poiché i nodi e i bordi vengono archiviati come tabelle, tutte le operazioni supportate nelle tabelle relazionali sono supportate nella tabella Node o Edge. Di seguito è fornito un esempio:   

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![persona-amici-tabelle](../../relational-databases/graphs/media/person-friends-tables.png "Tabelle Edge nodo persona e amici")  
Nodi e bordi vengono archiviati come tabelle  

### <a name="query-language-extensions"></a>Estensioni del linguaggio di query  
La `MATCH` nuova clausola è stata introdotta per supportare la ricerca e l'esplorazione a più hop tramite il grafo. La `MATCH` funzione usa la sintassi di stile ASCII per i criteri di ricerca. Ad esempio:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-ssnoversion-engine"></a>Completamente integrato nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore 
Le estensioni del grafo sono completamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrate nel motore di. Usare lo stesso motore di archiviazione, metadati, query processor e così via per archiviare ed eseguire query sui dati del grafo. Eseguire query su dati grafici e relazionali in un'unica query. Combinando le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Graph con altre tecnologie come columnstore, ha, R Services e così via. Il database SQL Graph supporta inoltre tutte le funzionalità di sicurezza e conformità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]disponibili con.
 
### <a name="tooling-and-ecosystem"></a>Strumenti e ecosistema

Vantaggi offerti dagli strumenti e dall'ecosistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistenti. Strumenti come backup e ripristino, importazione ed esportazione, BCP funzionano in modo predefinito. Altri strumenti o servizi come SSIS, SSRS o Power BI funzioneranno con le tabelle dei grafici, proprio come funzionano con le tabelle relazionali.

## <a name="edge-constraints"></a>Vincoli di arco
Un vincolo Edge viene definito in una tabella Edge del grafico ed è una coppia di tabelle di nodi a cui un determinato tipo di bordo può connettersi. Questo consente agli utenti di ottenere un controllo migliore sullo schema del grafo. Con l'ausilio di vincoli Edge, gli utenti possono limitare il tipo di nodi a cui un determinato bordo è autorizzato a connettersi. 

Per altre informazioni su come creare e usare vincoli Edge, vedere [vincoli Edge](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>Esegui merge DML 
L'istruzione [merge](../../t-sql/statements/merge-transact-sql.md) esegue operazioni di inserimento, aggiornamento o eliminazione in una tabella di destinazione in base ai risultati di un join con una tabella di origine. È possibile, ad esempio, sincronizzare due tabelle inserendo, aggiornando o eliminando righe in una tabella di destinazione in base alle differenze tra la tabella di destinazione e la tabella di origine. L'uso di predicati MATCH in un'istruzione MERGE è ora supportato nel database SQL di Azure e SQL Server vNext. In altre parole, è ora possibile unire i dati del grafo correnti (tabelle nodi o bordi) con nuovi dati usando i predicati di corrispondenza per specificare le relazioni Graph in un'unica istruzione, anziché istruzioni INSERT/UPDATE/DELETE separate.

Per ulteriori informazioni sulla modalità di utilizzo di match in DML di merge, vedere l' [istruzione MERGE](../../t-sql/statements/merge-transact-sql.md)

## <a name="shortest-path"></a>Percorso più breve
La funzione [SHORTEST_PATH](./sql-graph-shortest-path.md) trova il percorso più breve tra due nodi qualsiasi in un grafico o partendo da un nodo specificato a tutti gli altri nodi del grafico. Il percorso più breve può essere usato anche per trovare una chiusura transitiva o per gli attraversamenti di lunghezza arbitraria nel grafico. 

 ## <a name="next-steps"></a>Passaggi successivi  
Leggere l' [architettura del database SQL Graph](./sql-graph-architecture.md)
   


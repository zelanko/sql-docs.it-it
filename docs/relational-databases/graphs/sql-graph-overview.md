---
title: Graph processing con SQL Server e Database SQL di Azure | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 010d985245052949451a0b519ee4d7b312a97f4a
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413071"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Graph processing con SQL Server e Database SQL di Azure
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre funzionalità di database di grafi per modellare le relazioni molti-a-molti. Le relazioni di graph sono integrate [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e ricevere i vantaggi dell'uso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come sistema di gestione di database fondamentali.


## <a name="what-is-a-graph-database"></a>Che cos'è un database a grafo?  
Un database a grafo è una raccolta di nodi (o vertici) e archi (o relazioni). Un nodo rappresenta un'entità (ad esempio, una persona o un'organizzazione) e un arco rappresenta una relazione tra i due nodi che connette (ad esempio, Mi piace o amici). I nodi e bordi possono avere proprietà associate. Ecco alcune funzionalità che rendono un database a grafo univoco:  
-   Perimetri o le relazioni sono entità di prima classe in un Database a grafo e possono avere attributi o le proprietà associate. 
-   Un bordo singolo può connettersi in modo flessibile più nodi in un Database a grafo.
-   È possibile esprimere facilmente criteri di ricerca e query di esplorazione multi hop.
-   È possibile esprimere query polimorfica e chiusura transitiva con facilità.

## <a name="when-to-use-a-graph-database"></a>Quando usare un database a grafo

Non è possibile ottenere un database a grafo, che non può essere ottenuta utilizzando un database relazionale. Tuttavia, un database a grafo può rendere più semplice esprimere determinato tipo di query. Inoltre, con le ottimizzazioni specifiche, determinate query siano migliori. La decisione di scegliere uno di essi può essere basata sui fattori seguenti:  
-   L'applicazione include i dati gerarchici. Il tipo di dati HierarchyID consente di implementare le gerarchie, ma presenta alcune limitazioni. Ad esempio, non consentono di archiviare più elementi padre per un nodo.
-   L'applicazione presenta le complesse relazioni molti-a-molti; l'evoluzione dell'applicazione, vengono aggiunte nuove relazioni.
-   È necessario analizzare le relazioni e i dati interconnessi.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Funzionalità di Graph introdotte in [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Sta iniziando l'aggiunta di estensioni graph per SQL Server, per rendere più semplice l'esecuzione di query e l'archiviazione dei dati del grafico. Le funzionalità seguenti vengono introdotti nella prima versione. 


### <a name="create-graph-objects"></a>Creare gli oggetti di graph
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] le estensioni consentirà agli utenti di creare le tabelle nodi o bordi. I nodi e bordi possono avere proprietà associate a essi. Poiché, nodi e archi vengono archiviati come tabelle, tutte le operazioni che sono supportate nelle tabelle relazionali sono supportate nella tabella nodi o bordi. Esempio:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![le tabelle Person-amici](../../relational-databases/graphs/media/person-friends-tables.png "nodo /People/Person e amici edge tabelle")  
I nodi e archi vengono archiviati come tabelle  

### <a name="query-language-extensions"></a>Estensioni del linguaggio di query  
Nuovo `MATCH` clausola è stata introdotta per supportare criteri di ricerca e l'esplorazione multi hop tramite graph. Il `MATCH` funzione Usa sintassi grafica ASCII per criteri di ricerca. Ad esempio:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Completamente integrato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore 
Estensioni per i grafi sono completamente integrate [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore. Usare lo stesso motore di archiviazione, i metadati, il processore di query, e così via per archiviare ed eseguire query sui dati del grafico. Query su graph e dati relazionali in una singola query. La combinazione di funzionalità di grafi con altri [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologie come la tecnologia columnstore, a disponibilità elevata, R services, e così via. Database a grafo SQL supporta anche tutte le sicurezza e conformità di funzionalità disponibili con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Gli strumenti e l'ecosistema

Trarre vantaggio dall'ecosistema e gli strumenti esistenti che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre. Strumenti come il backup e ripristino, importare ed esportare, funzionano perfettamente BCP impostazione predefinita. Altri strumenti o servizi, ad esempio SSIS, SSRS o Power BI funzionerà con tabelle, graph nel modo in cui funzionano con tabelle relazionali.

## <a name="edge-constraints"></a>Vincoli di arco
Un vincolo di arco è definito in una tabella edge grafico e da una coppia di tabella/e di nodo che è possibile connettere un tipo di bordo specificato. Ciò consente agli utenti un migliore controllo sul loro schemi di grafi. Con l'aiuto di vincoli di arco gli utenti possono limitare il tipo di nodi di che un determinato bordo è autorizzato a connettersi. 

Per altre informazioni su come creare e usare i vincoli di arco, vedere [i vincoli di arco](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>Merge DML 
Il [MERGE](../../t-sql/statements/merge-transact-sql.md) istruzione esegue un'operazione insert, update o operazioni delete in una tabella di destinazione in base ai risultati di un join con una tabella di origine. Ad esempio, è possibile sincronizzare due tabelle inserendo, aggiornando o eliminando righe in una tabella di destinazione in base alle differenze tra la tabella di destinazione e la tabella di origine. Usare MATCH predicati in un'istruzione MERGE è ora supportato nel Database SQL di Azure e SQL Server vNext. Vale a dire, è ora possibile unire i dati del grafo corrente (tabelle nodi o bordi) con i nuovi dati utilizzando i predicati di corrispondenza per specificare le relazioni di graph in un'unica istruzione, invece di istruzioni INSERT/UPDATE/DELETE separate.

Per altre informazioni su come corrispondenza può essere utilizzata nel merge DML, vedere [istruzione MERGE](../../t-sql/statements/merge-transact-sql.md)

## <a name="shortest-path"></a>Percorso più breve
Il [SHORTEST_PATH](./sql-graph-shortest-path.md) funzione Trova percorso più breve tra qualsiasi 2 nodi in un grafico o a partire da un determinato nodo per tutti gli altri nodi nel grafico. Percorso più breve può essere utilizzato anche per trovare una chiusura transitiva o per gli attraversamenti di lunghezza arbitraria nel grafico. 

 ## <a name="next-steps"></a>Passaggi successivi  
Lettura di [Database a grafo SQL - architettura](./sql-graph-architecture.md)
   


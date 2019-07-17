---
title: Architettura di grafi SQL | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0124126556967800e37b296a73bd951a18d3936e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035982"
---
# <a name="sql-graph-architecture"></a>Architettura di grafi SQL  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Informazioni su come è progettato grafo SQL. Conoscere le nozioni di base renderà più facile comprendere altri articoli grafo SQL.
 
## <a name="sql-graph-database"></a>Database di grafi SQL
Gli utenti possono creare un grafico per ogni database. Un grafico è una raccolta di nodi e le tabelle bordi. Le tabelle nodi o archi possono essere create in qualsiasi schema nel database, ma appartengono a un unico grafico logico. Una tabella nodi è una raccolta di tipo simile di nodi. Ad esempio, una tabella nodi di persone contiene tutti i nodi di persone appartenenti a un grafico. Analogamente, una tabella edge è una raccolta di tipo simile di bordi. Ad esempio, una tabella bordi di amici contiene tutti i bordi che connettono una persona a un'altra persona. Poiché i nodi e archi vengono archiviati in tabelle, la maggior parte delle operazioni supportate per le tabelle regolari sono supportata nelle tabelle nodi o bordi. 
 
 
![SQL-graph-architecture](../../relational-databases/graphs/media/sql-graph-architecture.png "architettura del database Sql grafico")   

Figura 1: Architettura di database di grafi SQL
 
## <a name="node-table"></a>Tabella dei nodi
Una tabella nodi rappresenta un'entità in uno schema di grafico. Ogni volta che una tabella nodi viene creata, insieme a colonne definite dall'utente, implicita `$node_id` creazione della colonna, che identifica in modo univoco un nodo specifico nel database. I valori nelle `$node_id` vengono generati automaticamente e sono una combinazione di `object_id` di tale tabella dei nodi e un valore bigint generato internamente. Tuttavia, quando il `$node_id` colonna è selezionata, viene visualizzato un valore calcolato sotto forma di stringa JSON. Inoltre, `$node_id` è una pseudo colonna, che esegue il mapping a un nome interno con la stringa esadecimale in esso. Quando si seleziona `$node_id` dalla tabella, verranno visualizzati i nomi di colonna come `$node_id_<hex_string>`. Utilizzo di nomi di pseudo-colonna nelle query è lo strumento consigliato per l'esecuzione di query interno `$node_id` colonna e dei nomi interna con stringa esadecimale deve essere evitate.

È consigliabile che gli utenti creare un vincolo unique o un indice sul `$node_id` colonna al momento della creazione della tabella dei nodi, ma se non è creato, un valore predefinito viene creato automaticamente l'indice non cluster univoco. Tuttavia, qualsiasi indice su una pseudocolonna grafico viene creato nelle colonne interne sottostante. Vale a dire, un indice creato per il `$node_id` colonna, verranno visualizzati nella classe interna `graph_id_<hex_string>` colonna.   


## <a name="edge-table"></a>Tabella Edge
Una tabella bordi rappresenta una relazione in un grafico. Bordi vengano sempre indirizzati e connettono due nodi. Una tabella edge consente agli utenti di modellare le relazioni molti-a-molti nel grafico. Una tabella edge può o non abbia gli attributi definiti dall'utente in essa. Ogni volta che viene creata una tabella bordi, insieme agli attributi definiti dall'utente, vengono create tre colonne implicite della tabella edge:

|Nome colonna    |Descrizione  |
|---   |---  |
|`$edge_id`   |Identifica in modo univoco un bordo specificato nel database. Si tratta di una colonna generata e il valore è una combinazione di object_id della tabella edge e un valore bigint generato internamente. Tuttavia, quando il `$edge_id` colonna è selezionata, viene visualizzato un valore calcolato sotto forma di stringa JSON. `$edge_id` è una pseudo colonna, che esegue il mapping a un nome interno con la stringa esadecimale in esso. Quando si seleziona `$edge_id` dalla tabella, verranno visualizzati i nomi di colonna come `$edge_id_\<hex_string>`. Utilizzo di nomi di pseudo-colonna nelle query è lo strumento consigliato per l'esecuzione di query interno `$edge_id` colonna e dei nomi interna con stringa esadecimale deve essere evitate. |
|`$from_id`   |Gli archivi di `$node_id` del nodo, da cui ha origine il bordo.  |
|`$to_id`   |Gli archivi di `$node_id` del nodo, in corrispondenza del quale termina il bordo. |

I nodi che è possibile connettere un determinato bordo è disciplinato da quelli inseriti nel `$from_id` e `$to_id` colonne. Nella prima versione, non è possibile definire vincoli sulla tabella edge, per impedire la connessione di qualsiasi tipo due dei nodi. Vale a dire, una rete perimetrale può connettersi due nodi nel grafico, indipendentemente dai relativi tipi.

Simile al `$node_id` colonna, è consigliabile che gli utenti creano un indice univoco o un vincolo nel `$edge_id` colonna al momento della creazione della tabella edge, ma se non è creato, un indice non cluster univoco viene creato automaticamente in valore predefinito Questa colonna. Tuttavia, qualsiasi indice su una pseudocolonna grafico viene creato nelle colonne interne sottostante. Vale a dire, un indice creato per il `$edge_id` colonna, verranno visualizzati nella classe interna `graph_id_<hex_string>` colonna. È inoltre consigliabile, per gli scenari OLTP, che gli utenti di creare un indice su (`$from_id`, `$to_id`) le colonne, per le ricerche più veloci nella direzione del bordo.  

Figura 2 mostra come nodo e le tabelle bordi vengono archiviate nel database. 

![le tabelle Person-amici](../../relational-databases/graphs/media/person-friends-tables.png "nodo /People/Person e amici edge tabelle")   

Figura 2: Rappresentazione in forma di tabella edge e nodo



## <a name="metadata"></a>Metadata
Usare queste viste dei metadati per visualizzare gli attributi di una tabella nodi o bordi.
 
### <a name="systables"></a>sys.tables
La seguente nuovo, tipo, bit verranno aggiunte colonne di SYS. TABELLE. Se `is_node` è impostato su 1, che indica che la tabella è una tabella nodi e, se `is_edge` è impostato su 1, che indica che la tabella è una tabella bordi.
 
|Nome colonna |Tipo di dati |Descrizione |
|--- |---|--- |
|is_node |bit |1 = si tratta di una tabella nodi |
|is_edge |bit |1 = si tratta di una tabella bordi |
 
### <a name="syscolumns"></a>sys.columns
Il `sys.columns` visualizzazione contiene colonne aggiuntive `graph_type` e `graph_type_desc`, che indicano il tipo della colonna nel nodo e le tabelle bordi.
 
|Nome colonna |Tipo di dati |Descrizione |
|--- |---|--- |
|graph_type |int |Colonna interna con un set di valori. I valori sono compresi tra 1 a 8 per le colonne di graph e NULL per altri utenti.  |
|graph_type_desc |nvarchar(60)  |colonna interna con un set di valori |
 
Nella tabella seguente sono elencati i valori validi per `graph_type` colonna

|Valore della colonna  |Descrizione  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` sono inoltre archiviate informazioni sulle colonne implicite create nelle tabelle nodi o bordi. Le seguenti informazioni possono essere recuperate da Sys. Columns, tuttavia, gli utenti non è possibile selezionare tali colonne da una tabella nodi o bordi. 

Colonne implicite in una tabella nodi

|Nome colonna    |Tipo di dati  |is_hidden  |Commento  |
|---  |---|---|---  |
|graph_id_\<hex_string> |BIGINT |1  |interno `graph_id` colonna  |
|$node_id_\<hex_string> |NVARCHAR   |0  |Nodo esterno `node_id` colonna  |

Colonne implicite in una tabella bordi

|Nome colonna    |Tipo di dati  |is_hidden  |Commento  |
|---  |---|---|---  |
|graph_id_\<hex_string> |BIGINT |1  |interno `graph_id` colonna  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |External `edge_id` colonna  |
|from_obj_id_\<hex_string>  |INT    |1  |interno dal nodo `object_id`  |
|from_id_\<hex_string>  |BIGINT |1  |interno dal nodo `graph_id`  |
|$from_id_\<hex_string> |NVARCHAR   |0  |esterno dal nodo `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |interni al nodo `object_id`  |
|to_id_\<hex_string>    |BIGINT |1  |interni al nodo `graph_id`  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |esterna al nodo `node_id`  |
 
### <a name="system-functions"></a>Funzioni di sistema
Le funzioni predefinite seguenti vengono aggiunti. Queste funzionalità permetteranno agli utenti estrarre informazioni dalle colonne generate. Si noti che, questi metodi non determini l'input dell'utente. Se l'utente specifica un valore non valido `sys.node_id` il metodo estraggono la parte appropriata e restituirlo. Ad esempio, OBJECT_ID_FROM_NODE_ID richiederà un `$node_id` come input e restituiscono object_id della tabella, questo nodo appartiene. 
 
|Predefinito   |Descrizione  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Estrarre object_id da un `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |Estrarre il graph_id da un `node_id`  |
|NODE_ID_FROM_PARTS |Costruire un node_id da un `object_id` e un oggetto `graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |Estrarre `object_id` da `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |Identità da estrarre `edge_id`  |
|EDGE_ID_FROM_PARTS |Costruire `edge_id` da `object_id` e identità  |



## <a name="transact-sql-reference"></a>Guida di riferimento a Transact-SQL 
Scopri il [!INCLUDE[tsql-md](../../includes/tsql-md.md)] estensioni introdotte in SQL Server e Database SQL di Azure, che consentono la creazione e l'esecuzione di query su oggetti grafo. Le estensioni del linguaggio di query consentono di query e attraversare il grafo usando sintassi grafica ASCII.
 
### <a name="data-definition-language-ddl-statements"></a>Istruzioni Data Definition Language (DDL)

|Attività   |Articolo correlato  |Note
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE` viene ora estesa per supportare la creazione di una tabella AS nodi o bordi di AS. Si noti che una tabella edge può o non abbiano gli attributi definiti dall'utente.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|È possibile modificare nodi e le tabelle bordi esattamente una tabella relazionale, utilizza il `ALTER TABLE`. Gli utenti possono aggiungere o modificare le colonne definite dall'utente, indici o vincoli. Tuttavia, modificare le colonne grafico interne, ad esempio `$node_id` o `$edge_id`, verrà generato un errore.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Gli utenti possono creare indici su pseudo- colonne e le colonne definite dall'utente nel nodo e le tabelle bordi. Sono supportati tutti i tipi di indice, inclusi gli indici columnstore cluster e non cluster.  |
|CREARE I VINCOLI DI ARCO    |[I vincoli di arco &#40;Transact-SQL&#41;](../../relational-databases/tables/graph-edge-constraints.md)  |Gli utenti possono ora creare vincoli di arco sulle tabelle edge per applicare la semantica specifica e anche mantenere l'integrità dei dati  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |È possibile eliminare nodi e le tabelle bordi esattamente una tabella relazionale, utilizza il `DROP TABLE`. Tuttavia, in questa versione, non sono presenti vincoli per garantire che nessun bordi puntare a un nodo eliminato e propagate l'eliminazione dei bordi, quando si elimina un nodo o una tabella nodi non è supportata. È consigliabile che se viene eliminata una tabella nodi, agli utenti rimuovere tutti i bordi connessi ai nodi in tale tabella nodi manualmente per mantenere l'integrità del grafico.  |


### <a name="data-manipulation-language-dml-statements"></a>Istruzioni Data Manipulation Language (DML)

|Attività   |Articolo correlato  |Note
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|Inserimento in una tabella nodi equivale all'inserimento in una tabella relazionale. I valori per `$node_id` colonna generata automaticamente. Tentativo di inserire un valore in `$node_id` o `$edge_id` colonna verrà generato un errore. Gli utenti devono fornire valori per `$from_id` e `$to_id` colonne durante l'inserimento in una tabella bordi. `$from_id` e `$to_id` sono il `$node_id` valori dei nodi che si connette un determinato bordo.  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|I dati dalle tabelle nodi o archi possono essere eliminati in esattamente come verrà eliminata dalle tabelle relazionali. Tuttavia, in questa versione, non sono presenti vincoli per garantire che nessun bordi puntare a un nodo eliminato e propagate l'eliminazione dei bordi, quando si elimina un nodo non è supportata. È consigliabile che ogni volta che un nodo viene eliminato, tutti i bordi di collegamento a tale nodo vengono eliminati anche, per mantenere l'integrità del grafico.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |I valori nelle colonne definite dall'utente possono essere aggiornati usando l'istruzione UPDATE. Aggiornare le colonne grafico interne `$node_id`, `$edge_id`, `$from_id` e `$to_id` non è consentita.  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` istruzione è supportata in una tabella nodi o bordi.  |


### <a name="query-statements"></a>Istruzioni di query

|Attività   |Articolo correlato  |Note
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|I nodi e archi vengono archiviati internamente come tabelle, di conseguenza la maggior parte delle operazioni supportate in una tabella in SQL Server o Database SQL di Azure sono supportata nelle tabelle di nodo e bordo  |
|MATCH  | [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|CORRISPONDENZA incorporato è stato introdotto per supportare criteri di ricerca e l'attraversamento del grafico.  |



## <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti  
Esistono alcune limitazioni sul nodo e le tabelle bordi in questa versione:
* Tabelle temporanee locali o globali non possono essere tabelle nodi o bordi.
* I tipi di tabella e variabili di tabella non possono essere dichiarate come una tabella nodi o bordi. 
* Nodo e le tabelle bordi non è possibile creare le tabelle temporali con controllo delle versioni del sistema.   
* Nodo e le tabelle bordi non possono essere tabelle con ottimizzazione per la memoria.  
* Gli utenti non è possibile aggiornare il `$from_id` e `$to_id` colonne di un bordo usando l'istruzione UPDATE. Per aggiornare i nodi che si connette una rete perimetrale, gli utenti saranno necessario inserire il nuovo bordo sta puntando a nuovi nodi ed eliminare quello precedente.
* Non sono supportate le query su oggetti grafico tra database. 


## <a name="next-steps"></a>Passaggi successivi
Per iniziare a usare la nuova sintassi, vedere [Database a grafo SQL - esempio](./sql-graph-sample.md)
 


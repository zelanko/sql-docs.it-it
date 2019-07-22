---
title: Indicizzare dati JSON | Microsoft Docs
ms.custom: ''
ms.date: 06/01/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a31be55598d3a3df42a9d5a5fd39832fdbc08754
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909292"
---
# <a name="index-json-data"></a>Indicizzazione dei dati JSON
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

JSON non è un tipo di dati predefinito in SQL Server e nel database SQL e SQL Server non usa indici JSON personalizzati. È possibile tuttavia ottimizzare le query sui documenti JSON usando indici standard. 

Gli indici del database migliorano le prestazioni delle operazioni di filtro e ordinamento. Senza indici, SQL Server deve eseguire un'analisi completa della tabella ogni volta che viene eseguita una query sui dati.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indicizzazione delle proprietà JSON mediante colonne calcolate  
Quando si archiviano i dati JSON in SQL Server, di solito l'obiettivo è filtrare o ordinare i risultati delle query in base a una o più *proprietà* dei documenti JSON.  

### <a name="example"></a>Esempio 
In questo esempio si suppone che la tabella `SalesOrderHeader` di AdventureWorks includa una colonna `Info` che contiene varie informazioni in formato JSON sugli ordini di vendita. Contiene ad esempio informazioni sul cliente, sul venditore, sugli indirizzi di spedizione e di fatturazione e così via. Si vogliono usare i valori della colonna `Info` per filtrare gli ordini di vendita per un cliente.

### <a name="query-to-optimize"></a>Query da ottimizzare
Di seguito è riportato un esempio del tipo di query da ottimizzare usando un indice.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Indice di esempio
Per velocizzare i filtri o le clausole `ORDER BY` su una proprietà in un documento JSON, è possibile usare gli stessi indici già usati per altre colonne. Tuttavia, non è possibile fare *direttamente* riferimento alle proprietà nei documenti JSON.
    
1.  Per prima cosa è necessario creare una "colonna virtuale" che restituisca i valori che verranno usati per il filtro.
2.  È quindi necessario creare un indice su quella colonna virtuale.  
  
Nell'esempio seguente viene creata una colonna calcolata che può essere usata per l'indicizzazione. Successivamente viene creato un indice per la nuova colonna calcolata. In questo esempio viene creata una colonna che espone il nome del cliente archiviato nel percorso `$.Customer.Name` nei dati JSON. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Altre informazioni sulla colonna calcolata 
La colonna calcolata non è persistente. È calcolata solo quando è necessario ricostruire l'indice. Non occupa spazio aggiuntivo nella tabella.   
  
È importante creare la colonna calcolata con la stessa espressione che si prevede di usare nelle query, in questo esempio l'espressione è `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Non è necessario riscrivere le query. Se si usano espressioni con la funzione `JSON_VALUE` come illustrato nella query di esempio precedente, SQL Server rileva la presenza di una colonna calcolata equivalente con la stessa espressione e, se possibile, applica un indice.

### <a name="execution-plan-for-this-example"></a>Piano di esecuzione per questo esempio
Di seguito viene riportato il piano di esecuzione per la query di questo esempio.  
  
![Piano di esecuzione](../../relational-databases/json/media/jsonindexblog1.png "Piano di esecuzione")  
  
Anziché un'analisi completa della tabella, SQL Server usa un indice seek nell'indice non cluster e individua le righe che soddisfano le condizioni specificate. Usa quindi una ricerca chiave nella tabella `SalesOrderHeader` per recuperare le altre colonne a cui si fa riferimento nella query, in questo esempio, `SalesOrderNumber` e `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Ottimizzare ulteriormente l'indice con colonne incluse
Se si aggiungono le colonne richieste nell'indice è possibile evitare questa ulteriore ricerca nella tabella. È possibile aggiungere tali colonne come colonne incluse standard, come illustrato nell'esempio seguente che estende l'esempio `CREATE INDEX` precedente.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
In questo caso SQL Server non deve leggere i dati aggiuntivi della tabella `SalesOrderHeader` perché tutto il necessario è incluso nell'indice non cluster JSON. Questo tipo di indice è un buon metodo per combinare i dati JSON e di colonna nelle query e per creare indici ottimali per il carico di lavoro.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Gli indici JSON sono in grado di riconoscere le regole di confronto  
Una caratteristica importante degli indici per i dati JSON è che gli indici sono in grado di riconoscere le regole di confronto. Il risultato della funzione `JSON_VALUE`, che si usa quando si crea la colonna calcolata, è un valore di testo che eredita le regole di confronto dall'espressione di input. Di conseguenza, i valori dell'indice vengono ordinati usando le regole di confronto definite nelle colonne di origine.  
  
Per dimostrare che gli indici sono sensibili al confronto, nell'esempio seguente viene creata una semplice tabella di raccolta con una chiave primaria e contenuto JSON.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
Il comando precedente consente di specificare le regole di confronto per il serbo (cirillico) per la colonna JSON. Nell'esempio seguente la tabella viene popolata e viene creato un indice nella proprietà del nome.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
I comandi precedenti creano un indice standard per la colonna calcolata `vName`, che rappresenta il valore della proprietà `$.name` JSON. Nella tabella codici per il serbo (cirillico), l'ordine delle lettere è 'А','Б','В','Г','Д','Ђ','Е', ecc. L'ordine degli elementi nell'indice è conforme alle regole per il serbo (cirillico) perché il risultato della funzione `JSON_VALUE` eredita le regole di confronto dalla colonna di origine. Nell'esempio seguente viene eseguita una query su questa raccolta e i risultati vengono ordinati in base al nome.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Se si esamina il piano di esecuzione, si noterà che vengono usati valori ordinati dall'indice non cluster.  
  
 ![Piano di esecuzione](../../relational-databases/json/media/jsonindexblog2.png "Piano di esecuzione")  
  
 Anche se la query include una clausola `ORDER BY`, il piano di esecuzione non usa un operatore di ordinamento. L'indice JSON è già ordinato in base alle regole per il serbo (cirillico). SQL Server può pertanto usare l'indice non cluster in cui risultati sono già ordinati.  
  
 Se tuttavia si modificano le regole di confronto dell'espressione `ORDER BY`, ad esempio inserendo `COLLATE French_100_CI_AS_SC` dopo la funzione `JSON_VALUE`, si ottiene un piano di esecuzione della query diverso.  
  
 ![Piano di esecuzione](../../relational-databases/json/media/jsonindexblog3.png "Piano di esecuzione")  
  
 Poiché l'ordine dei valori in corrispondenza dell'indice non è conforme alle regole di confronto per il francese, SQL Server non può usare l'indice per ordinare i risultati. Pertanto, aggiunge un operatore di ordinamento che ordina i risultati usando le regole di confronto per il francese.  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)

---
title: EXPLAIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 99edc393a8d831373fd3b7175af545f00655980c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465705"
---
# <a name="explain-transact-sql"></a>EXPLAIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Restituisce il piano di query per un'istruzione [!INCLUDE[DWsql](../../includes/dwsql-md.md)] [!INCLUDE[ssDW](../../includes/ssdw-md.md)] senza eseguire l'istruzione. Usare **EXPLAIN** per un'anteprima delle operazioni che richiedono lo spostamento di dati e per visualizzare i costi stimati delle operazioni di query.  
  
 Per altre informazioni sui piani di query, vedere la sezione introduttiva sui piani di query nella [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *SQL_statement*  
 L'istruzione [!INCLUDE[DWsql](../../includes/dwsql-md.md)] per la quale viene eseguita l'istruzione **EXPLAIN**. *SQL_statement* può essere uno qualsiasi dei comandi seguenti: **SELECT**, **INSERT**, **UPDATE**, **DELETE**, **CREATE TABLE AS SELECT**, **CREATE REMOTE TABLE**.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessaria l'autorizzazione **SHOWPLAN** autorizzazione e l'autorizzazione per eseguire *SQL_statement*. Vedere [Autorizzazioni: GRANT, DENY, REVOKE &#40;Azure SQL Data Warehouse, Parallel Data Warehouse&#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Valore restituito  
 Il valore restituito dal comando **EXPLAIN** è un documento XML con la struttura illustrata di seguito. Questo documento XML elenca tutte le operazioni nel piano di query per la query specificata, ognuna racchiuso nel tag `<dsql_operation>`. Il valore restituito è di tipo **nvarchar(max)** .  
  
 Il piano di query restituito illustra istruzioni SQL sequenziali. Quando la query viene eseguita, può implicare operazioni eseguite in parallelo e quindi alcune delle istruzioni sequenziali illustrate possono essere eseguite contemporaneamente.  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 I tag XML contengono queste informazioni:  
  
|Tag XML|Riepilogo, attributi e contenuto|  
|-------------|--------------------------------------|  
|\<dsql_query>|Elemento di livello superiore o documento.|
|\<sql>|Esegue l'eco di *SQL_statement*.|  
|\<params>|Tag attualmente non usato.|  
|\<dsql_operations>|Riepiloga e contiene i passaggi della query e include informazioni sui costi per la query. Contiene anche tutti i blocchi `<dsql_operation>`. Questo tag contiene informazioni relative ai conteggi per l'intera query:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* è il tempo stimato totale per l'esecuzione della query in ms.<br /><br /> *total_number_operations* è il numero totale di operazioni per la query. Un'operazione da eseguire in parallelo in più nodi viene conteggiata come operazione singola.|  
|\<dsql_operation>|Descrive una singola operazione all'interno del piano di query. Il tag \<dsql_operation > contiene il tipo di operazione come attributo:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* è uno dei valori trovati in [sys.dm_pdw_request_steps (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).<br /><br /> Il contenuto del blocco `\<dsql_operation>` dipende dal tipo di operazione.<br /><br /> Vedere la tabella riportata di seguito.|  
  
|Tipo di operazione|Contenuto|Esempio|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE e TRIM_MOVE|Elemento `<operation_cost>` con questi attributi. I valori riflettono solo l'operazione locale:<br /><br /> -   *cost* è il costo dell'operatore locale e visualizza il tempo stimato per l'operazione da eseguire, in ms.<br />-   *accumulative_cost* è la somma di tutte le operazioni visualizzate nel piano inclusa la somma dei valori di operazioni parallele, in ms.<br />-   *average_rowsize* è la dimensione media stimata (in byte) delle righe recuperate e passate durante l'operazione.<br />-   *output_rows* è la cardinalità di output (nodo) e visualizza il numero di righe di output.<br /><br /> `<location>`: i nodi o le distribuzioni in cui verrà eseguita l'operazione. Sono disponibili le opzioni seguenti: "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Distribution" e "SubsetNodes".<br /><br /> `<source_statement>`: i dati di origine per lo spostamento casuale.<br /><br /> `<destination_table>`: la tabella temporanea interna in cui verranno spostati i dati.<br /><br /> `<shuffle_columns>`: applicabile solo alle operazioni SHUFFLE_MOVE. Una o più colonne che verranno usate come colonne di distribuzione per la tabella temporanea.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: vedere la descrizione di `<operation_cost>` riportata in precedenza.<br /><br /> `<DestinationCatalog>`: il nodo o i nodi di destinazione.<br /><br /> `<DestinationSchema>`: lo schema di destinazione in DestinationCatalog.<br /><br /> `<DestinationTableName>`: il nome della tabella di destinazione o "TableName".<br /><br /> `<DestinationDatasource>`: il nome della connessione o le informazioni di connessione per l'origine dati di destinazione.<br /><br /> `<Username>` e `<Password>`: questi campi indicano che la destinazione può richiedere un nome utente e una password.<br /><br /> `<BatchSize>`: la dimensione del batch per l'operazione di copia.<br /><br /> `<SelectStatement>`: l'istruzione SELECT usata per eseguire la copia.<br /><br /> `<distribution>`: la distribuzione in cui viene eseguita la copia.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: la tabella di origine per l'operazione.<br /><br /> `<destination_table>`: la tabella di destinazione per l'operazione.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: vedere la descrizione di `<location>` riportata in precedenza.<br /><br /> `<sql_operation>`: identifica il comando SQL che verrà eseguito in un nodo.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: il catalogo di destinazione.<br /><br /> `<DestinationSchema>`: lo schema di destinazione in DestinationCatalog.<br /><br /> `<DestinationTableName>`: il nome della tabella di destinazione o "TableName".<br /><br /> `<DestinationDatasource>`: il nome dell'origine dati di destinazione.<br /><br /> `<Username>` e `<Password>`: questi campi indicano che la destinazione può richiedere un nome utente e una password.<br /><br /> `<CreateStatement>`: l'istruzione per la creazione della tabella per il database di destinazione.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: l'identificatore per il set di risultati.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: l'identificatore per l'oggetto creato.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 È possibile applicare **EXPLAIN** solo a query a *ottimizzabili*, ovvero a query che possono essere migliorate o modificate in base ai risultati di un comando **EXPLAIN**. I comandi **EXPLAIN** sono elencati più indietro. Se si tenta di usare **EXPLAIN** con un tipo di query non supportato, verrà restituito un errore o verrà eseguito l'eco della query.  
  
 **EXPLAIN** non è supportato nelle transazioni utente.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente illustra un comando **EXPLAIN** eseguito per un'istruzione **SELECT** e il risultato XML.  
  
 **Invio di un'istruzione EXPLAIN**  
  
 Il comando inviato per questo esempio è:  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 Dopo l'esecuzione dell'istruzione con l'opzione **EXPLAIN**, la scheda dei messaggi presenta una sola riga denominata **explain** che inizia con il testo XML `\<?xml version="1.0" encoding="utf-8"?>` Fare clic sull'XML per aprire l'intero testo in un finestra XML. Per comprendere meglio i commenti seguenti, è necessario attivare la visualizzazione dei numeri di riga in SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Per attivare i numeri di riga  
  
1.  Con l'output visualizzato nella scheda **explain** di SSDT selezionare **Opzioni** dal menu **STRUMENTI**.  
  
2.  Espandere la sezione **Editor di testo**, espandere **XML** e quindi fare clic su **Generale**.  
  
3.  Nell'area **Visualizzazione** selezionare **Numeri di riga**.  
  
4.  Fare clic su **OK**.  
  
 **Output di EXPLAIN di esempio**  
  
 L'XML risultante del comando **EXPLAIN** con i numeri di riga attivati è il seguente:  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **Significato dell'output di EXPLAIN**  
  
 L'output precedente contiene 144 righe numerate. L'output della query può essere diverso per diversi utenti. L'elenco seguente descrive le sezioni significative.  
  
-   Le righe da 3 a 16 forniscono una descrizione della query in corso di analisi.  
  
-   La riga 17 specifica che il numero totale di operazioni è 9. È possibile individuare l'inizio di ogni operazione cercando le parole **dsql_operation**.  
  
-   Alla riga 18 inizia l'operazione 1. Le righe 18 e 19 indicano che un'operazione **RND_ID** creerà un numero ID casuale che verrà usato per la descrizione di un oggetto. L'oggetto descritto nell'output precedente è **TEMP_ID_16893**. Il numero sarà diverso per ogni utente.  
  
-   Alla riga 20 inizia l'operazione 2. Righe da 21 a 25: l'operazione crea una tabella temporanea denominata **TEMP_ID_16893** in tutti i nodi di calcolo.  
  
-   Alla riga 26 inizia l'operazione 3. Righe da 27 a 37: l'operazione sposta i dati in **TEMP_ID_16893** tramite uno spostamento dati trasmessi. Viene fornita la query inviata a ogni nodo di calcolo. La riga 37 specifica la tabella di destinazione, **TEMP_ID_16893**.  
  
-   Alla riga 38 inizia l'operazione 4. Righe da 39 a 40: l'operazione crea un ID casuale per una tabella. Nell'esempio qui sopra l'ID è **TEMP_ID_16894**. Il numero sarà diverso per ogni utente.  
  
-   Alla riga 41 inizia l'operazione 5. Righe da 42 a 46: l'operazione crea una tabella temporanea denominata **TEMP_ID_16894** in tutti i nodi.  
  
-   Alla riga 47 inizia l'operazione 6. Righe da 48 a 91: l'operazione sposta i dati da diverse tabelle (inclusa **TEMP_ID_16893**) alla tabella **TEMP_ID_16894** tramite un'operazione di spostamento casuale. Viene fornita la query inviata a ogni nodo di calcolo. La riga 90 specifica la tabella di destinazione, **TEMP_ID_16894**. La riga 91 specifica le colonne.  
  
-   Alla riga 92 inizia l'operazione 7. Righe da 93 a 97: l'operazione elimina la tabella temporanea **TEMP_ID_16893** in tutti i nodi di calcolo.  
  
-   Alla riga 98 inizia l'operazione 8. Righe da 99 a 135: l'operazione restituisce i risultati al client. Usa la query fornita per ottenere i risultati.  
  
-   Alla riga 136 inizia l'operazione 9. Righe da 137 a 140: l'operazione elimina la tabella temporanea **TEMP_ID_16894** in tutti i nodi.  
  
  


---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 7ce26cd3d4e42d6d94e32a3454318a0ee841c486
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124492"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Esegue uno script fornito come argomento di input alla procedura. Lo script viene eseguito nel [framework di estendibilità](../../advanced-analytics/concepts/extensibility-framework.md). Script deve essere scritto in un linguaggio supportato e registrato, in presenza di almeno un'estensione di un motore di database: [**R**](../../advanced-analytics/concepts/extension-r.md), [ **Python**](../../advanced-analytics/concepts/extension-python.md), oppure [ **Java** (in SQL Server 2019 solo anteprima)](../../advanced-analytics/java/extension-java.md). 

Per eseguire **sp_execute_external_script**, è innanzitutto necessario abilitare gli script esterni utilizzando l'istruzione, `sp_configure 'external scripts enabled', 1;`.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> Machine learning (R e Python) e la programmazione delle estensioni viene installate come un componente aggiuntivo per l'istanza del motore di database. Supporto per estensioni specifiche variano a seconda versione di SQL Server.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>Sintassi

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>Sintassi per il 2017 e versioni precedenti

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>Argomenti
 **@language** = N'*linguaggio*'  
 Indica il linguaggio di scripting. *linguaggio* viene **sysname**.  A seconda della versione di SQL Server, i valori validi sono (SQL Server 2016 e versioni successive) di R, Python (SQL Server 2017 e versioni successive) e Java (anteprima di SQL Server 2019). 
  
 **@script** = N'*script*' dello script del linguaggio esterno specificato come input un valore letterale o una variabile. *lo script* viene **nvarchar (max)** .  

`[ @input_data_1 =  N'input_data_1' ]` Specifica i dati di input usati dallo script esterno sotto forma di un [!INCLUDE[tsql](../../includes/tsql-md.md)] query. Il tipo di dati *input_data_1* viene **nvarchar (max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` Specifica il nome della variabile utilizzata per rappresentare la query definita dal @input_data_1. Il tipo di dati della variabile nello script esterno dipende dalla lingua. In caso di R, la variabile di input è un frame di dati. Nel caso di Python, input deve essere in formato tabulare. *input_data_1_name* viene **sysname**.  Valore predefinito è *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` Si applica solo a SQL Server 2019 e viene usato per creare modelli per ogni partizione. Specifica il nome della colonna usata per ordinare il set di risultati, ad esempio tramite il nome del prodotto. Il tipo di dati della variabile nello script esterno dipende dalla lingua. In caso di R, la variabile di input è un frame di dati. Nel caso di Python, input deve essere in formato tabulare.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` Si applica solo a SQL Server 2019 e viene usato per creare modelli per ogni partizione. Specifica il nome della colonna usata per segmentare i dati, ad esempio area geografica o Data. Il tipo di dati della variabile nello script esterno dipende dalla lingua. In caso di R, la variabile di input è un frame di dati. Nel caso di Python, input deve essere in formato tabulare. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` Specifica il nome della variabile nello script esterno che contiene i dati da restituire al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo il completamento della chiamata alla stored procedure. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Per R, l'output deve essere un frame di dati. Per Python, l'output deve essere un frame di dati pandas. *output_data_1_name* viene **sysname**.  Valore predefinito è *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` Abilitare l'esecuzione parallela di script R, impostando il `@parallel` parametro 1. Il valore predefinito per questo parametro è 0 (nessun parallelism). Se `@parallel = 1` e l'output come flusso direttamente al computer client, il `WITH RESULT SETS` clausola è obbligatoria e deve essere specificato uno schema di output.  

 + Per gli script R che non usano funzioni RevoScaleR, usando il `@parallel` parametro può essere utile per l'elaborazione di grandi set di dati, presupponendo che lo script può essere facilmente parallelizzato. Ad esempio, quando si usa R `predict` funzione con un modello per generare nuove stime, impostare `@parallel = 1` come hint per il motore di query. Se la query può essere parallelizzata, le righe vengono distribuite in base al **MAXDOP** impostazione.  
  
 + Per gli script R che usano funzioni RevoScaleR, l'elaborazione parallela viene gestita automaticamente e non è necessario specificare `@parallel = 1` per il **sp_execute_external_script** chiamare.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` Un elenco di dichiarazioni di parametro di input utilizzate nello script esterni.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` Un elenco di valori per i parametri di input usati dallo script esterno.  

## <a name="remarks"></a>Note

> [!IMPORTANT]
> L'albero della query è controllata dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli utenti non possono eseguire operazioni arbitrari nella query. 

Uso **sp_execute_external_script** per eseguire script scritti in una lingua supportata. Lingue supportate sono attualmente R per SQL Server 2016 R Services e Python e R per Machine Learning Services di SQL Server 2017. 

Per impostazione predefinita, i set di risultati restituiti dalla stored procedure vengono restituiti con le colonne senza nome. Nomi di colonna usati in uno script sono locali per l'ambiente di scripting e non vengono riflesse nel set di risultati output. Per denominare le colonne del set di risultati, usare il `WITH RESULT SET` della clausola [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Oltre a restituire un set di risultati, è possibile restituire valori scalari per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando i parametri di OUTPUT. Nell'esempio seguente viene illustrato l'utilizzo del parametro di OUTPUT per restituire il modello R serializzato che è stato usato come input allo script:  
  
È possibile controllare le risorse usate dagli script esterno tramite la configurazione di un pool di risorse esterne. Per altre informazioni, vedere [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informazioni sul carico di lavoro possono essere ottenute dalle viste del catalogo di resource governor, viste a gestione dinamica e contatori. Per altre informazioni, vedere [viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor correlati viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [ SQL Server oggetto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorare l'esecuzione di script

L'esecuzione di script di monitoraggio mediante [DM external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parametri per la modellazione di partizione

 In SQL Server 2019, attualmente in anteprima pubblica, è possibile impostare due parametri aggiuntivi che consentono la modellazione delle minacce su dati partizionati, in cui partizioni sono basate su uno o più colonne è fornire che naturalmente segmentare un set di dati in partizioni logiche creato e utilizzato solo durante l'esecuzione di script. Le colonne che contengono i valori ripetuti per età, sesso, area geografica, data o ora, sono riportati alcuni esempi che si prestano a set di dati partizionati.
 
 I due parametri sono **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, in cui il secondo parametro viene usato per ordinare il set di risultati. I parametri vengono passati come input per `sp_execute_external_script` con l'esterno script in esecuzione una sola volta per ogni partizione. Per altre informazioni ed esempi, vedere [esercitazione: Creare modelli basati sulla partizione](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

 È possibile eseguire script in parallelo specificando `@parallel=1`. Se la query di input può essere eseguite in parallelo, è necessario impostare `@parallel=1` come parte degli argomenti su `sp_execute_external_script`. Per impostazione predefinita, query optimizer opera `@parallel=1` nelle tabelle che includono più di 256 righe, ma se si vuole gestirlo in modo esplicito, questo script include il parametro come dimostrazione.

 > [!Tip]
> Per la formazione workoads, è possibile usare `@parallel` qualsiasi script di training arbitrari, anche quelli con algoritmi non-Microsoft-rx. Solo gli algoritmi di RevoScaleR (con il prefisso di rx) offrono in genere, il parallelismo in scenari di training in SQL Server. Ma con i nuovi parametri in SQL Server vNext, è possibile parallelizzare uno script che chiama le funzioni non specificamente progettate con tale funzionalità.
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>Esecuzione di flusso per gli script R e Python  

Il flusso consente lo script R o Python da usare con più dati possono adattarsi alla memoria. Per controllare il numero di righe passate durante lo streaming, specificare un valore integer per il parametro `@r_rowsPerRead` nella `@params` raccolta.  Ad esempio, se si è training di un modello che usa i dati molto ampie, è possibile regolare il valore per leggere un minor numero di righe, per garantire che tutte le righe possono essere inviate in un blocco di dati. È anche possibile usare questo parametro per gestire il numero di righe da letti ed elaborati in una sola volta, per attenuare i problemi di prestazioni di server. 
  
Entrambi il `@r_rowsPerRead` parametro per lo streaming e il `@parallel` argomento deve essere considerato l'hint. Per l'hint da applicare, deve essere possibile generare un piano di query SQL che include l'elaborazione parallela. Se questo non è possibile, non è possibile abilitare l'elaborazione parallela.  
  
> [!NOTE]  
>  Elaborazione parallela e streaming sono supportati solo nella Enterprise Edition. È possibile includere parametri nelle query in Standard Edition senza generare un errore, ma i parametri non hanno alcun effetto e gli script R eseguiti in un unico processo.  
  
## <a name="restrictions"></a>Restrizioni  


### <a name="data-types"></a>Tipi di dati

Tipi di dati seguenti non sono supportati quando usato nelle query di input o i parametri del **sp_execute_external_script** procedure e restituito un errore di tipo non supportato.  

In alternativa, **CAST** la colonna o un valore a un tipo supportato in [!INCLUDE[tsql](../../includes/tsql-md.md)] prima dell'invio dello script esterno.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **hierarchyid**, **geometry**, **geography**  
  
-   Tipi CLR definiti dall'utente

In generale, qualsiasi risultato set che non può essere mappato a un [!INCLUDE[tsql](../../includes/tsql-md.md)] tipo di dati, vengono restituiti come NULL.  

### <a name="restrictions-specific-to-r"></a>Restrizioni specifiche di R

Se l'input include **data/ora** i valori che non rientrano nell'intervallo consentito di valori in R, i valori vengono convertiti in **NA**. Questa operazione è necessaria perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente a un intervallo più ampio di valori rispetto a quelle supportate nel linguaggio R.

Valori di float (ad esempio, `+Inf`, `-Inf`, `NaN`) non sono supportati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se entrambi i linguaggi usano IEEE 754. Comportamento attuale Invia solo i valori per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direttamente; di conseguenza, il client SQL in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] genera un errore. Di conseguenza, questi valori vengono convertiti **NULL**.

## <a name="permissions"></a>Permissions

È necessario **EXECUTE ANY EXTERNAL SCRIPT** autorizzazione del database.  

## <a name="examples"></a>Esempi

In questa sezione contiene esempi di come è possibile utilizzare questa stored procedure per eseguire gli script R o Python usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>R. Restituisce un set di dati R per SQL Server  

L'esempio seguente crea una stored procedure che utilizza **sp_execute_external_script** per restituire il set di dati Iris incluso in R per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generare un modello R basato sui dati da SQL Server  

L'esempio seguente crea una stored procedure che utilizza **sp_execute_external_script** per generare un modello iris e restituisce il modello a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  In questo esempio richiede l'installazione di avanzamento del pacchetto e1071. Per altre informazioni, vedere [installare altri pacchetti R in SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Per generare un modello simile tramite Python, è necessario modificare l'identificatore del linguaggio da `@language=N'R'` a `@language = N'Python'` e apportare le modifiche necessarie all'argomento `@script`. In caso contrario, tutti i parametri funzionano allo stesso modo di R.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Creare un modello Python e generare punteggi da esso

Questo esempio illustra come usare sp\_execute\_external\_script per generare punteggi in un modello Python semplice. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Le intestazioni di colonna usate nel codice Python non vengono trasmesse a SQL Server. Pertanto, utilizzare l'istruzione con risultati per specificare i nomi di colonna e tipi di dati SQL deve usare.

Per il punteggio, è anche possibile usare la funzione nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), che è in genere più veloce, perché consente di evitare la chiamata al runtime di Python o R.

## <a name="see-also"></a>Vedere anche

 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tipi di dati e le librerie Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Tipi di dati R e librerie di R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [Servizi R per SQL Server](../../advanced-analytics/r/sql-server-r-services.md)   
 [Problemi noti per SQL Server Machine Learning Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREATE EXTERNAL LIBRARY &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opzione di configurazione del server external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [Oggetto External Scripts di SQL Server](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 

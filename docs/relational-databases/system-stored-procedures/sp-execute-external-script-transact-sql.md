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
ms.openlocfilehash: 6a7eb58883a94f1eb29d2c7e26e52768f4e08d9e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304933"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Esegue uno script fornito come argomento di input per la stored procedure. Lo script viene eseguito nel [Framework di estendibilità](../../advanced-analytics/concepts/extensibility-framework.md). Lo script deve essere scritto in un linguaggio supportato e registrato, in un motore di database con almeno un'estensione: [**R**](../../advanced-analytics/concepts/extension-r.md), [**Python**](../../advanced-analytics/concepts/extension-python.md)o [ **Java** (solo in SQL Server 2019 Preview)](../../advanced-analytics/java/extension-java.md). 

Per eseguire **sp_execute_external_script**, è necessario innanzitutto abilitare gli script esterni usando l'istruzione `sp_configure 'external scripts enabled', 1;`.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> Machine Learning (R e Python) e le estensioni di programmazione sono installate come componente aggiuntivo per l'istanza del motore di database. Il supporto per estensioni specifiche varia in base alla versione SQL Server.

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
## <a name="syntax-for-2017-and-earlier"></a>Sintassi per 2017 e versioni precedenti

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
 **\@language** = n'*Language*'  
 Indica il linguaggio di scripting. *Language* è di **tipo sysname**.  A seconda della versione di SQL Server, i valori validi sono R (SQL Server 2016 e versioni successive), Python (SQL Server 2017 e versioni successive) e Java (SQL Server 2019 Preview). 
  
 script di linguaggio esterno **\@script** = n'*script*specificato come input letterale o variabile. *lo script* è **nvarchar (max)** .  

`[ @input_data_1 =  N'input_data_1' ]` specifica i dati di input usati dallo script esterno sotto forma di query [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il tipo di dati di *input_data_1* è **nvarchar (max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` specifica il nome della variabile utilizzata per rappresentare la query definita da @input_data_1. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. *input_data_1_name* è di **tipo sysname**.  Il valore predefinito è *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` si applica solo SQL Server 2019 e viene usato per compilare i modelli per partizione. Specifica il nome della colonna utilizzata per ordinare il set di risultati, ad esempio in base al nome del prodotto. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` si applica solo SQL Server 2019 e viene usato per compilare i modelli per partizione. Specifica il nome della colonna usata per segmentare i dati, ad esempio l'area geografica o la data. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` specifica il nome della variabile nello script esterno che contiene i dati da restituire al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al completamento della chiamata di stored procedure. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Per R, l'output deve essere un frame di dati. Per Python, l'output deve essere un frame di dati Pandas. *output_data_1_name* è di **tipo sysname**.  Il valore predefinito è *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` consente l'esecuzione parallela di script R impostando il parametro `@parallel` su 1. Il valore predefinito per questo parametro è 0 (nessun parallelismo). Se `@parallel = 1` e l'output viene trasmesso direttamente al computer client, è necessario specificare la clausola `WITH RESULT SETS` ed è necessario specificare uno schema di output.  

 + Per gli script R che non usano funzioni RevoScaleR, l'uso del parametro `@parallel` può essere utile per l'elaborazione di set di impostazioni di grandi dimensioni, supponendo che lo script possa essere trivialmente parallelo. Ad esempio, quando si usa la funzione R `predict` con un modello per generare nuove stime, impostare `@parallel = 1` come hint per il motore di query. Se la query può essere eseguita in parallelo, le righe vengono distribuite in base all'impostazione **MAXDOP** .  
  
 + Per gli script R che usano funzioni RevoScaleR, l'elaborazione parallela viene gestita automaticamente e non è necessario specificare `@parallel = 1` alla chiamata **sp_execute_external_script** .  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` un elenco di dichiarazioni di parametro di input utilizzate nello script esterno.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` un elenco di valori per i parametri di input usati dallo script esterno.  

## <a name="remarks"></a>Note

> [!IMPORTANT]
> L'albero della query è controllato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli utenti non possono eseguire operazioni arbitrarie sulla query. 

Usare **sp_execute_external_script** per eseguire gli script scritti in un linguaggio supportato. Attualmente, le lingue supportate sono R per SQL Server 2016 R Services, Python e R per SQL Server 2017 Machine Learning Services. 

Per impostazione predefinita, i set di risultati restituiti da questo stored procedure vengono restituiti con colonne senza nome. I nomi di colonna utilizzati in uno script sono locali rispetto all'ambiente di scripting e non vengono riflessi nel set di risultati di output. Per denominare le colonne del set di risultati, usare la clausola `WITH RESULT SET` di [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md).
  
 Oltre a restituire un set di risultati, è possibile restituire valori scalari a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando parametri di OUTPUT. Nell'esempio seguente viene illustrato l'uso del parametro OUTPUT per restituire il modello R serializzato usato come input per lo script:  
  
È possibile controllare le risorse usate dagli script esterni configurando un pool di risorse esterne. Per altre informazioni, vedere [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Le informazioni sul carico di lavoro possono essere ottenute dalle viste del catalogo di Resource Governor, dalla DMV e dai contatori. Per ulteriori informazioni, vedere [Resource Governor viste &#40;del catalogo Transact-&#41;SQL](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor viste &#40;a gestione dinamica correlate Transact&#41;-SQL](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [SQL Server, oggetto script esterni](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorare l'esecuzione degli script

Monitorare l'esecuzione degli script utilizzando [sys. dm _external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys. dm _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parametri per la modellazione della partizione

 In SQL Server 2019, attualmente in anteprima pubblica, è possibile impostare due parametri aggiuntivi che consentono di modellare i dati partizionati, in cui le partizioni sono basate su una o più colonne fornite che segmentano naturalmente un set di dati in partizioni logiche create e usate solo durante l'esecuzione dello script. Le colonne contenenti valori ripetuti per età, sesso, area geografica, data o ora sono alcuni esempi che si prestano ai set di dati partizionati.
 
 I due parametri sono **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, in cui il secondo parametro viene usato per ordinare il set di risultati. I parametri vengono passati come input a `sp_execute_external_script` con lo script esterno eseguito una volta per ogni partizione. Per ulteriori informazioni ed esempi, vedere [Tutorial: Creare modelli basati su partizioni @ no__t-0.

 È possibile eseguire lo script in parallelo specificando `@parallel=1`. Se la query di input può essere eseguita in parallelo, è necessario impostare `@parallel=1` come parte degli argomenti su `sp_execute_external_script`. Per impostazione predefinita, il Query Optimizer opera in `@parallel=1` sulle tabelle che includono più di 256 righe, ma se si desidera gestirlo in modo esplicito, questo script include il parametro come dimostrazione.

 > [!Tip]
> Per workoads di training, è possibile usare `@parallel` con qualsiasi script di training arbitrario, anche quelli che usano algoritmi non Microsoft-RX. In genere, solo gli algoritmi RevoScaleR (con il prefisso RX) offrono il parallelismo negli scenari di training in SQL Server. Tuttavia, con i nuovi parametri in SQL Server vNext, è possibile parallelizzare uno script che chiama funzioni non specificamente progettate con tale funzionalità.
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>Esecuzione del flusso per gli script R e Python  

Il flusso consente allo script R o Python di funzionare con più dati rispetto a quelli che possono adattarsi alla memoria. Per controllare il numero di righe passate durante il flusso, specificare un valore intero per il parametro, `@r_rowsPerRead` nella raccolta `@params`.  Se, ad esempio, si esegue il training di un modello che utilizza dati molto estesi, è possibile modificare il valore per leggere un numero inferiore di righe, in modo da garantire che tutte le righe possano essere inviate in un blocco di dati. È inoltre possibile utilizzare questo parametro per gestire il numero di righe da leggere ed elaborare contemporaneamente, per mitigare i problemi di prestazioni del server. 
  
Sia il parametro `@r_rowsPerRead` per il flusso che l'argomento `@parallel` devono essere considerati hint. Per applicare l'hint, è necessario che sia possibile generare un piano di query SQL che includa l'elaborazione parallela. Se ciò non è possibile, l'elaborazione parallela non può essere abilitata.  
  
> [!NOTE]  
>  Il flusso e l'elaborazione parallela sono supportati solo in Enterprise Edition. È possibile includere i parametri nelle query in Standard Edition senza generare un errore, ma i parametri non hanno effetto e gli script R vengono eseguiti in un unico processo.  
  
## <a name="restrictions"></a>Restrictions  


### <a name="data-types"></a>Tipi di dati

I tipi di dati seguenti non sono supportati quando vengono utilizzati nella query di input o nei parametri della procedura **sp_execute_external_script** e restituiscono un errore di tipo non supportato.  

Come soluzione alternativa, **eseguire il cast** della colonna o del valore a un tipo supportato in [!INCLUDE[tsql](../../includes/tsql-md.md)] prima di inviarlo allo script esterno.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **hierarchyid**, **Geometry**, **geography**  
  
-   Tipi CLR definiti dall'utente

In generale, qualsiasi set di risultati di cui non è possibile eseguire il mapping a un tipo di dati [!INCLUDE[tsql](../../includes/tsql-md.md)] viene restituito come NULL.  

### <a name="restrictions-specific-to-r"></a>Limitazioni specifiche di R

Se l'input include valori **DateTime** che non rientrano nell'intervallo consentito di valori in R, i valori vengono convertiti in **na**. Questa operazione è necessaria perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente un intervallo di valori maggiore di quello supportato nel linguaggio R.

I valori float (ad esempio, `+Inf`, `-Inf`, `NaN`) non sono supportati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se entrambi i linguaggi usano IEEE 754. Il comportamento corrente Invia solo i valori a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direttamente; di conseguenza, il client SQL in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] genera un errore. Pertanto, questi valori vengono convertiti in **null**.

## <a name="permissions"></a>Permissions

È richiesta l'autorizzazione **Execute any external script** database.  

## <a name="examples"></a>Esempi

Questa sezione contiene esempi di come è possibile usare questa stored procedure per eseguire script R o Python con [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>R. Restituisce un set di dati R a SQL Server  

Nell'esempio seguente viene creato un stored procedure che usa **sp_execute_external_script** per restituire il set di dati Iris incluso con R per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generare un modello R basato sui dati di SQL Server  

Nell'esempio seguente viene creato un stored procedure che utilizza **sp_execute_external_script** per generare un modello Iris e restituire il modello al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Questo esempio richiede l'installazione anticipata del pacchetto e1071. Per altre informazioni, vedere [installare pacchetti R aggiuntivi in SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Creazione di un modello Python e generazione di punteggi

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

Le intestazioni di colonna usate nel codice Python non vengono restituite a SQL Server; Pertanto, utilizzare l'istruzione WITH RESULT per specificare i nomi di colonna e i tipi di dati per SQL da utilizzare.

Per il punteggio, è anche possibile usare la funzione nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), che è in genere più veloce, perché consente di evitare la chiamata al runtime di Python o R.

## <a name="see-also"></a>Vedere anche

 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Librerie e tipi di dati Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Librerie r e tipi di dati R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
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

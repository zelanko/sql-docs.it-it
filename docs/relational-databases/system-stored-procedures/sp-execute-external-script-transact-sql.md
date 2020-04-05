---
title: sp_execute_external_script (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663009"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
La **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input per la routine e viene utilizzata con [Machine Learning Services](../../machine-learning/index.yml) ed [Estensioni linguaggio](../../language-extensions/language-extensions-overview.md). 

Per i servizi di Machine Learning, [Python](../../machine-learning/concepts/extension-python.md) e [R](../../machine-learning/concepts/extension-r.md) sono linguaggi supportati. Per le estensioni del linguaggio, Java è supportato ma deve essere definito con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md).

Per eseguire **sp_execute_external_script,** è innanzitutto necessario installare Machine Learning Services o Estensioni del linguaggio. Per altre informazioni, vedere [Installare SQL Server Machine Learning Services (Python e R) in Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md) e [Linux](../../linux/sql-server-linux-setup-machine-learning.md) [oppure Installare le estensioni del linguaggio SQL Server in Windows](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) e [Linux.](../../linux/sql-server-linux-setup-language-extensions.md)
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input per la procedura e viene usata con [Machine Learning Services](../../machine-learning/index.yml) in SQL Server 2017. 

Per i servizi di Machine Learning, [Python](../../machine-learning/concepts/extension-python.md) e [R](../../machine-learning/concepts/extension-r.md) sono linguaggi supportati. 

Per eseguire **sp_execute_external_script**, è innanzitutto necessario installare Machine Learning Services. Per altre informazioni, vedere Installare I servizi di [SQL Server Machine Learning Services (Python e R) in Windows.](../../machine-learning/install/sql-machine-learning-services-windows-install.md)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input per la procedura e viene usata con R Services in SQL Server 2016.The example stored procedure executes a script provided as a input argument to the procedure, and is used with [R Services](../../machine-learning/r/sql-server-r-services.md) on SQL Server 2016.

Per R Services, [R](../../machine-learning/concepts/extension-r.md) è la lingua supportata.

Per eseguire **sp_execute_external_script**, è innanzitutto necessario installare R Services. Per altre informazioni, vedere Installare I servizi di [SQL Server Machine Learning Services (Python e R) in Windows.](../../machine-learning/install/sql-r-services-windows-install.md)
::: moniker-end

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

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
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
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
 lingua - lingua N *'* ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica il linguaggio di script. *language* è **sysname**. I valori validi sono **R**, **Python**e qualsiasi linguaggio definito con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (ad esempio, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica il linguaggio di script. *language* è **sysname**. In SQL Server 2017SQL Server 2017, i valori validi sono **R** e **Python**.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica il linguaggio di script. *language* è **sysname**. In SQL Server 2016, l'unico valore valido è **R**.
::: moniker-end

 script - Script*N'* script ' Script di linguaggio esterno specificato come input di valori letterali o variabili. ** \@** *script* è **nvarchar(max)**.  

`[ @input_data_1 =  N'input_data_1' ]`Specifica i dati di input utilizzati dallo [!INCLUDE[tsql](../../includes/tsql-md.md)] script esterno sotto forma di query. Il tipo di dati di *input_data_1* è **nvarchar(max)**.

`[ @input_data_1_name = N'input_data_1_name' ]`Specifica il nome della variabile utilizzata per @input_data_1rappresentare la query definita da . Il tipo di dati della variabile nello script esterno dipende dal linguaggio. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. *input_data_1_name* è **sysname**.  Il valore predefinito è *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`Utilizzato per creare modelli per partizione. Specifica il nome della colonna utilizzata per ordinare il set di risultati, ad esempio in base al nome del prodotto. Il tipo di dati della variabile nello script esterno dipende dal linguaggio. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`Utilizzato per creare modelli per partizione. Specifica il nome della colonna utilizzata per segmentare i dati, ad esempio l'area geografica o la data. Il tipo di dati della variabile nello script esterno dipende dal linguaggio. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`Specifica il nome della variabile nello script esterno che contiene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i dati da restituire al completamento della chiamata di stored procedure. Il tipo di dati della variabile nello script esterno dipende dal linguaggio. Per R, l'output deve essere un frame di dati. Per Python, l'output deve essere un frame di dati panda. *output_data_1_name* è **sysname**.  Il valore predefinito è *OutputDataSet*.  

`[ @parallel = 0 | 1 ]`Abilitare l'esecuzione parallela `@parallel` degli script R impostando il parametro su 1.Enable parallel execution of R scripts by setting the parameter to 1. Il valore predefinito per questo parametro è 0 (nessun parallelismo). Se `@parallel = 1` e l'output viene trasmesso direttamente al `WITH RESULT SETS` computer client, la clausola è obbligatoria ed è necessario specificare uno schema di output.  

 + Per gli script R che non usano le `@parallel` funzioni RevoScaleR, l'uso del parametro può essere utile per l'elaborazione di set di dati di grandi dimensioni, presupponendo che lo script possa essere parallelizzato in modo semplice. Ad esempio, quando `predict` si usa la funzione R con `@parallel = 1` un modello per generare nuove stime, impostare come suggerimento per il motore di query. Se la query può essere parallelizzata, le righe vengono distribuite in base all'impostazione **MAXDOP.**  
  
 + Per gli script R che usano le funzioni RevoScaleR, `@parallel = 1` l'elaborazione parallela viene gestita automaticamente e non è necessario specificare per la **chiamata sp_execute_external_script.**  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`Elenco di dichiarazioni di parametri di input utilizzate nello script esterno.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`Elenco di valori per i parametri di input utilizzati dallo script esterno.  

## <a name="remarks"></a>Osservazioni

> [!IMPORTANT]
> L'albero delle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] query è controllato da e gli utenti non possono eseguire operazioni arbitrarie sulla query. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire script scritti in una lingua supportata. I linguaggi supportati sono **Python** e **R** usati con Machine Learning Services e qualsiasi linguaggio definito con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (ad esempio, Java) usato con le estensioni del linguaggio.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire script scritti in una lingua supportata. I linguaggi supportati sono **Python** e **R** in SQL Server 2017 Machine Learning Services.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire script scritti in una lingua supportata. L'unica lingua supportata è R in SQL Server 2016 R Services.The only supported language is **R** in SQL Server 2016 R Services.
::: moniker-end

Per impostazione predefinita, i set di risultati restituiti da questa stored procedure vengono restituiti con colonne senza nome. I nomi di colonna utilizzati all'interno di uno script sono locali rispetto all'ambiente di scripting e non vengono riflessi nel set di risultati restituito. Per denominare le `WITH RESULT SET` colonne [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)del set di risultati, utilizzare la clausola di .

Oltre a restituire un set di risultati, è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile restituire valori scalari utilizzando i parametri OUTPUT. 
  
È possibile controllare le risorse utilizzate dagli script esterni configurando un pool di risorse esterno. Per ulteriori informazioni, vedere [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Le informazioni sul carico di lavoro possono essere ottenute dalle viste del catalogo, dalle DMV e dai contatori del catalogo di Resource Governor. Per ulteriori informazioni, vedere Visualizzazioni del catalogo di [Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Viste a gestione dinamica correlate a Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [SQL Server, oggetto Script esterni](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorare l'esecuzione dello scriptMonitor script execution

Monitorare l'esecuzione di script utilizzando [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parametri per la modellazione delle partizioni

È possibile impostare due parametri aggiuntivi che consentono la modellazione dei dati partizionati, in cui le partizioni sono basate su una o più colonne fornite che segmentano naturalmente un set di dati in partizioni logiche create e utilizzate solo durante l'esecuzione dello script. Le colonne contenenti valori ripetuti per età, sesso, area geografica, data o ora sono alcuni esempi che si prestano a set di dati partizionati.
 
I due parametri sono **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, in cui il secondo parametro viene utilizzato per ordinare il set di risultati. I parametri vengono passati `sp_execute_external_script` come input con lo script esterno in esecuzione una volta per ogni partizione. Per ulteriori informazioni ed esempi, vedere [Esercitazione: Creare modelli basati su partizioni](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition).

È possibile eseguire script in `@parallel=1`parallelo specificando . Se la query di input può `@parallel=1` essere parallelizzata, `sp_execute_external_script`è necessario impostare come parte degli argomenti su . Per impostazione predefinita, Query `@parallel=1` Optimizer opera in su tabelle con più di 256 righe, ma se si desidera gestire questo in modo esplicito, questo script include il parametro come dimostrazione.

> [!Tip]
> Per i carichi di lavoro di training, è possibile usare `@parallel` con qualsiasi script di training arbitrario, anche quelli che usano algoritmi non Microsoft Rx. In genere, solo gli algoritmi RevoScaleR (con il prefisso rx) offrono il parallelismo negli scenari di training in SQL Server. Ma con i nuovi parametri in SQL Server vNext, è possibile parallelizzare uno script che chiama funzioni non specificamente progettate con tale funzionalità.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Esecuzione dello streaming per script Python e R  

Lo streaming consente allo script Python o R di funzionare con più dati di quanti possano contenere. Per controllare il numero di righe passate durante lo `@r_rowsPerRead` streaming, specificare un valore intero per il parametro nella `@params` raccolta.  Ad esempio, se si esegue il training di un modello che usa dati molto ampi, è possibile modificare il valore per leggere un numero inferiore di righe, per garantire che tutte le righe possano essere inviate in un unico blocco di dati. È inoltre possibile utilizzare questo parametro per gestire il numero di righe lette ed elaborate contemporaneamente, per ridurre i problemi di prestazioni del server. 
  
Sia `@r_rowsPerRead` il parametro `@parallel` per lo streaming che l'argomento devono essere considerati suggerimenti. Per l'hint da applicare, deve essere possibile generare un piano di query SQL che include l'elaborazione parallela. Se ciò non è possibile, non è possibile abilitare l'elaborazione parallela.  
  
> [!NOTE]  
> Lo streaming e l'elaborazione parallela sono supportati solo in Enterprise Edition. È possibile includere i parametri nelle query in Standard Edition senza generare un errore, ma i parametri non hanno alcun effetto e gli script R vengono eseguiti in un unico processo.  
  
## <a name="restrictions"></a>Restrizioni  

### <a name="data-types"></a>Tipi di dati

I tipi di dati seguenti non sono supportati quando vengono utilizzati nella query di input o nei parametri di **sp_execute_external_script** procedura e restituiscono un errore di tipo non supportato.  

Per risolvere il problema, **eseguire** il cast [!INCLUDE[tsql](../../includes/tsql-md.md)] della colonna o del valore in un tipo supportato prima di inviarlo allo script esterno.  
  
-   **Cursore**  
  
-   **Timestamp**  
  
-   **datetime2**, **datetimeoffset**, **ora**  
  
-   **sql_variant**  
  
-   **testo**, **immagine**  
  
-   **xml**  
  
-   **hierarchyid**, **geometria**, **geografia**  
  
-   Tipi CLR definiti dall'utente

In generale, qualsiasi set di risultati [!INCLUDE[tsql](../../includes/tsql-md.md)] che non può essere mappato a un tipo di dati viene restituito come NULL.  

### <a name="restrictions-specific-to-r"></a>Restrizioni specifiche di R

Se l'input include valori **datetime** che non rientrano nell'intervallo consentito di valori in R, i valori vengono convertiti in **NA**. Questa operazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessaria perché consente un intervallo di valori più ampio rispetto a quello supportato nel linguaggio R.This is required because permits a larger range of values than is supported in the R language.

I valori float `+Inf`(ad `NaN`esempio, , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `-Inf`, ) non sono supportati in anche se entrambe le lingue utilizzano IEEE 754. Il comportamento corrente invia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo i valori direttamente; di conseguenza, il [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] client SQL in genera un errore. Pertanto, questi valori vengono convertiti in **NULL**.

## <a name="permissions"></a>Autorizzazioni

Richiede l'autorizzazione del database **EXECUTE ANY EXTERNAL SCRIPT.**  

## <a name="examples"></a>Esempi

Questa sezione contiene esempi di come questa stored procedure può [!INCLUDE[tsql](../../includes/tsql-md.md)]essere utilizzata per eseguire script R o Python utilizzando .

### <a name="a-return-an-r-data-set-to-sql-server"></a>R. Restituire un set di dati R a SQL ServerReturn an R data set to SQL Server  

Nell'esempio seguente viene creata **sp_execute_external_script** una stored procedure che utilizza sp_execute_external_script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]per restituire il dataset Iris incluso in R a .  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generare un modello R basato sui dati da SQL ServerGenerate an R model based on data from SQL Server  

Nell'esempio riportato di seguito viene creata una stored procedure che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]utilizza **sp_execute_external_script** per generare un modello di iride e restituire il modello a .  

> [!NOTE]
>  Questo esempio richiede l'installazione anticipata del pacchetto e1071. Per altre informazioni, vedere Installare pacchetti R aggiuntivi in SQL Server.For more information, see [Install additional R packages on SQL Server.](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)

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

Le intestazioni di colonna usate nel codice Python non vengono restituite in SQL ServerSQL Server; pertanto, utilizzare il WITH RESULT istruzione per specificare i nomi di colonna e i tipi di dati per SQL da utilizzare.

Per il punteggio, è anche possibile usare la funzione nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), che è in genere più veloce, perché consente di evitare la chiamata al runtime di Python o R.

## <a name="see-also"></a>Vedere anche

+ [Servizi di Machine Learning di SQL Server](../../machine-learning/index.yml)
+ [Estensioni del linguaggio SQL Server](../../language-extensions/language-extensions-overview.md). 
+ [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Librerie Python e tipi di dati](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [R Libraries and R Data Types](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [SQL Server R Services](../../machine-learning/r/sql-server-r-services.md)   
+ [Problemi noti per i servizi di Machine Learning di SQL ServerKnown Issues for SQL Server Machine Learning Services](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREATE EXTERNAL LIBRARY &#40;&#41;Transact-SQL](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opzione di configurazione del server external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [Oggetto External Scripts di SQL Server](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 

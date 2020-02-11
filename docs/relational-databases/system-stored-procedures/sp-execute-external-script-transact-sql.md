---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: ab3bf4f98abaf5f164a3b38f4e09b10acf28b2f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73532828"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Il **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input per la stored procedure e viene utilizzato con [Machine Learning Services](../../advanced-analytics/index.yml) e le [estensioni del linguaggio](../../language-extensions/language-extensions-overview.md). 

Per Machine Learning Services, [Python](../../advanced-analytics/concepts/extension-python.md) e [R](../../advanced-analytics/concepts/extension-r.md) sono linguaggi supportati. Per le estensioni del linguaggio, Java è supportato, ma deve essere definito con [Create external language](../../t-sql/statements/create-external-language-transact-sql.md).

Per eseguire **sp_execute_external_script**, è necessario innanzitutto installare Machine Learning Services o le estensioni del linguaggio. Per altre informazioni, vedere [install SQL Server Machine Learning Services (Python and R) on Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) and [linux](../../linux/sql-server-linux-setup-machine-learning.md)o [Install SQL Server Language Extensions on Windows](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) and [Linux](../../linux/sql-server-linux-setup-language-extensions.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Il **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input della stored procedure e viene utilizzato con [Machine Learning Services](../../advanced-analytics/index.yml) su SQL Server 2017. 

Per Machine Learning Services, [Python](../../advanced-analytics/concepts/extension-python.md) e [R](../../advanced-analytics/concepts/extension-r.md) sono linguaggi supportati. 

Per eseguire **sp_execute_external_script**, è necessario innanzitutto installare Machine Learning Services. Per altre informazioni, vedere [Install SQL Server Machine Learning Services (Python and R) in Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md).
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Il **sp_execute_external_script** stored procedure esegue uno script fornito come argomento di input per la stored procedure e viene usato con [R Services](../../advanced-analytics/r/sql-server-r-services.md) in SQL Server 2016.

Per R Services, [r](../../advanced-analytics/concepts/extension-r.md) è il linguaggio supportato.

Per eseguire **sp_execute_external_script**, è necessario innanzitutto installare R Services. Per altre informazioni, vedere [Install SQL Server Machine Learning Services (Python and R) in Windows](../../advanced-analytics/install/sql-r-services-windows-install.md).
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
 lingua = N'*lingua*' ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica il linguaggio di scripting. *Language* è di **tipo sysname**. I valori validi sono **R**, **Python**e qualsiasi linguaggio definito con [Create external language](../../t-sql/statements/create-external-language-transact-sql.md) (ad esempio, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica il linguaggio di scripting. *Language* è di **tipo sysname**. In SQL Server 2017 i valori validi sono **R** e **Python**.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica il linguaggio di scripting. *Language* è di **tipo sysname**. In SQL Server 2016, l'unico valore valido è **R**.
::: moniker-end

 script = n'script '*script*' linguaggio esterno specificato come input letterale o variabile. ** \@** *lo script* è **nvarchar (max)**.  

`[ @input_data_1 =  N'input_data_1' ]`Specifica i dati di input usati dallo script esterno sotto forma di [!INCLUDE[tsql](../../includes/tsql-md.md)] query. Il tipo di dati di *input_data_1* è **nvarchar (max)**.

`[ @input_data_1_name = N'input_data_1_name' ]`Specifica il nome della variabile utilizzata per rappresentare la query definita da @input_data_1. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. *input_data_1_name* è di **tipo sysname**.  Il valore predefinito è *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`Utilizzato per compilare modelli per partizione. Specifica il nome della colonna utilizzata per ordinare il set di risultati, ad esempio in base al nome del prodotto. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`Utilizzato per compilare modelli per partizione. Specifica il nome della colonna usata per segmentare i dati, ad esempio l'area geografica o la data. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Nel caso di R, la variabile di input è un frame di dati. Nel caso di Python, l'input deve essere tabulare. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`Specifica il nome della variabile nello script esterno che contiene i dati da restituire al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completamento della chiamata stored procedure. Il tipo di dati della variabile nello script esterno dipende dalla lingua. Per R, l'output deve essere un frame di dati. Per Python, l'output deve essere un frame di dati Pandas. *output_data_1_name* è di **tipo sysname**.  Il valore predefinito è *OutputDataSet*.  

`[ @parallel = 0 | 1 ]`Abilitare l'esecuzione parallela di script R impostando il `@parallel` parametro su 1. Il valore predefinito per questo parametro è 0 (nessun parallelismo). Se `@parallel = 1` e l'output viene trasmesso direttamente al computer client, la `WITH RESULT SETS` clausola è obbligatoria ed è necessario specificare uno schema di output.  

 + Per gli script R che non usano funzioni RevoScaleR, l'uso `@parallel` del parametro può essere utile per l'elaborazione di set di impostazioni di grandi dimensioni, supponendo che lo script possa essere trivialmente parallelo. Ad esempio, quando si usa la `predict` funzione R con un modello per generare nuove stime, impostare `@parallel = 1` come hint per il motore di query. Se la query può essere eseguita in parallelo, le righe vengono distribuite in base all'impostazione **MAXDOP** .  
  
 + Per gli script R che usano funzioni RevoScaleR, l'elaborazione parallela viene gestita automaticamente e non `@parallel = 1` è necessario specificare alla chiamata **sp_execute_external_script** .  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`Elenco di dichiarazioni di parametro di input utilizzate nello script esterno.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`Elenco di valori per i parametri di input utilizzati dallo script esterno.  

## <a name="remarks"></a>Osservazioni

> [!IMPORTANT]
> L'albero della query è controllato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da e gli utenti non possono eseguire operazioni arbitrarie sulla query. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire gli script scritti in un linguaggio supportato. Le lingue supportate sono **Python** e **R** usati con Machine Learning Services e qualsiasi linguaggio definito con [Create external language](../../t-sql/statements/create-external-language-transact-sql.md) (ad esempio, Java) usato con le estensioni del linguaggio.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire gli script scritti in un linguaggio supportato. Le lingue supportate sono **Python** e **R** in SQL Server 2017 Machine Learning Services.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Utilizzare **sp_execute_external_script** per eseguire gli script scritti in un linguaggio supportato. L'unica lingua supportata è **r** in SQL Server 2016 r Services.
::: moniker-end

Per impostazione predefinita, i set di risultati restituiti da questo stored procedure vengono restituiti con colonne senza nome. I nomi di colonna utilizzati in uno script sono locali rispetto all'ambiente di scripting e non vengono riflessi nel set di risultati di output. Per denominare le colonne del set `WITH RESULT SET` di risultati [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md), utilizzare la clausola di.

Oltre a restituire un set di risultati, è possibile restituire valori scalari [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a utilizzando parametri di output. 
  
È possibile controllare le risorse usate dagli script esterni configurando un pool di risorse esterne. Per altre informazioni, vedere [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Le informazioni sul carico di lavoro possono essere ottenute dalle viste del catalogo di Resource Governor, dalla DMV e dai contatori. Per ulteriori informazioni, vedere [Resource Governor viste del catalogo &#40;&#41;Transact-sql ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) [Resource Governor viste a gestione dinamica correlate a &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [SQL Server, oggetto script esterni](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorare l'esecuzione degli script

Monitorare l'esecuzione di script utilizzando [sys. dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys. dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parametri per la modellazione della partizione

È possibile impostare due parametri aggiuntivi che consentono di modellare i dati partizionati, in cui le partizioni sono basate su una o più colonne fornite che segmentano naturalmente un set di dati in partizioni logiche create e usate solo durante l'esecuzione dello script. Le colonne contenenti valori ripetuti per età, sesso, area geografica, data o ora sono alcuni esempi che si prestano ai set di dati partizionati.
 
I due parametri sono **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, in cui il secondo parametro viene utilizzato per ordinare il set di risultati. I parametri vengono passati come input a `sp_execute_external_script` con lo script esterno eseguito una volta per ogni partizione. Per ulteriori informazioni ed esempi, vedere [esercitazione: creare modelli basati su partizioni](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

È possibile eseguire lo script in parallelo specificando `@parallel=1`. Se la query di input può essere eseguita in parallelo, è `@parallel=1` necessario impostare come parte degli argomenti `sp_execute_external_script`su. Per impostazione predefinita, il Query Optimizer opera `@parallel=1` con sulle tabelle che includono più di 256 righe, ma se si desidera gestirlo in modo esplicito, questo script include il parametro come dimostrazione.

> [!Tip]
> Per i carichi di lavoro di training, è possibile usare `@parallel` con qualsiasi script di training arbitrario, anche quelli che usano algoritmi non Microsoft Rx. In genere, solo gli algoritmi RevoScaleR (con il prefisso rx) offrono il parallelismo negli scenari di training in SQL Server. Tuttavia, con i nuovi parametri in SQL Server vNext, è possibile parallelizzare uno script che chiama funzioni non specificamente progettate con tale funzionalità.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Esecuzione del flusso per gli script Python e R  

Il flusso consente allo script Python o R di funzionare con più dati rispetto a quelli che possono adattarsi alla memoria. Per controllare il numero di righe passate durante il `@r_rowsPerRead` `@params` flusso, specificare un valore intero per il parametro nella raccolta.  Se, ad esempio, si esegue il training di un modello che utilizza dati molto estesi, è possibile modificare il valore per leggere un numero inferiore di righe, in modo da garantire che tutte le righe possano essere inviate in un blocco di dati. È inoltre possibile utilizzare questo parametro per gestire il numero di righe da leggere ed elaborare contemporaneamente, per mitigare i problemi di prestazioni del server. 
  
Sia il `@r_rowsPerRead` parametro per lo streaming che `@parallel` l'argomento devono essere considerati hint. Per applicare l'hint, è necessario che sia possibile generare un piano di query SQL che includa l'elaborazione parallela. Se ciò non è possibile, l'elaborazione parallela non può essere abilitata.  
  
> [!NOTE]  
> Il flusso e l'elaborazione parallela sono supportati solo in Enterprise Edition. È possibile includere i parametri nelle query in Standard Edition senza generare un errore, ma i parametri non hanno effetto e gli script R vengono eseguiti in un unico processo.  
  
## <a name="restrictions"></a>Restrizioni  

### <a name="data-types"></a>Tipi di dati

I tipi di dati seguenti non sono supportati quando vengono utilizzati nella query di input o nei parametri della procedura **sp_execute_external_script** e restituiscono un errore di tipo non supportato.  

Come soluzione alternativa, **eseguire il cast** della colonna o del valore a un [!INCLUDE[tsql](../../includes/tsql-md.md)] tipo supportato in prima di inviarlo allo script esterno.  
  
-   **cursore**  
  
-   **timestamp**  
  
-   **datetime2**, **DateTimeOffset**, **Time**  
  
-   **sql_variant**  
  
-   **testo**, **immagine**  
  
-   **XML**  
  
-   **hierarchyid**, **Geometry**, **geography**  
  
-   Tipi CLR definiti dall'utente

In generale, qualsiasi set di risultati di cui non è possibile [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguire il mapping a un tipo di dati viene restituito come null.  

### <a name="restrictions-specific-to-r"></a>Limitazioni specifiche di R

Se l'input include valori **DateTime** che non rientrano nell'intervallo consentito di valori in R, i valori vengono convertiti in **na**. Questa operazione è necessaria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] perché consente un intervallo di valori maggiore di quello supportato nel linguaggio R.

I valori float (ad esempio `+Inf` `-Inf`,, `NaN`) non sono supportati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se entrambi i linguaggi usano IEEE 754. Il comportamento corrente Invia solo i valori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direttamente; di conseguenza, il client SQL in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] genera un errore. Pertanto, questi valori vengono convertiti in **null**.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione **Execute any external script** database.  

## <a name="examples"></a>Esempi

Questa sezione contiene esempi di come è possibile usare questa stored procedure per eseguire script R o Python usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>R. Restituisce un set di dati R a SQL Server  

Nell'esempio seguente viene creato un stored procedure che usa **sp_execute_external_script** per restituire il set di dati Iris incluso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in R a.  

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

Nell'esempio seguente viene creato un stored procedure che utilizza **sp_execute_external_script** per generare un modello Iris e restituire il modello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a.  

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

Le intestazioni di colonna usate nel codice Python non vengono restituite a SQL Server; Pertanto, utilizzare l'istruzione WITH RESULT per specificare i nomi di colonna e i tipi di dati per SQL da utilizzare.

Per il punteggio, è anche possibile usare la funzione nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), che è in genere più veloce, perché consente di evitare la chiamata al runtime di Python o R.

## <a name="see-also"></a>Vedere anche

+ [SQL Server Machine Learning Services](../../advanced-analytics/index.yml)
+ [Estensioni del linguaggio SQL Server](../../language-extensions/language-extensions-overview.md). 
+ [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Librerie e tipi di dati Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
+ [Librerie r e tipi di dati R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
+ [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
+ [Problemi noti per SQL Server Machine Learning Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREARE una libreria esterna &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opzione di configurazione del server external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, oggetto script esterni](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 

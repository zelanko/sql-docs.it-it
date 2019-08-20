---
title: Come creare query MDX in R tramite olapr
description: Usare la libreria di pacchetti olapr in SQL Server per scrivere query MDX nello script del linguaggio R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb2918e5fb89d85d7f6fa1cc12622481e585d848
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887668"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>Come creare query MDX in R tramite olapr
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il pacchetto [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) supporta le query MDX su cubi ospitati in SQL Server Analysis Services. È possibile compilare una query su un cubo esistente, esplorare le dimensioni e altri oggetti del cubo e incollare le query MDX esistenti per recuperare i dati.

Questo articolo descrive i due usi principali del pacchetto **olapr** :

+ [Compilare una query MDX da R, usando i costruttori forniti nel pacchetto olapr](#buildMDX)
+ [Eseguire una query MDX valida esistente utilizzando olapr e un provider OLAP](#executeMDX)

Le operazioni seguenti non sono supportate:

+ Query DAX su un modello tabulare
+ Creazione di nuovi oggetti OLAP
+ Writeback delle partizioni, incluse misure o somme

## <a name="buildMDX"></a>Compilare una query MDX da R

1. Definire una stringa di connessione che specifica l'origine dati OLAP (istanza di SSAS) e il provider MSOLAP.

2. Usare la funzione `OlapConnection(connectionString)` per creare un handle per la query MDX e passare la stringa di connessione.

3. Usare il costruttore `Query()` per creare un'istanza di un oggetto query.

4. Usare le funzioni helper seguenti per fornire altri dettagli sulle dimensioni e sulle misure da includere nella query MDX:

     + `cube()` Specificare il nome del database SSAS. Se ci si connette a un'istanza denominata, specificare il nome del computer e il nome dell'istanza. 
     + `columns()`Specificare i nomi delle misure da usare nell'argomento **on Columns** .
     + `rows()`Specificare i nomi delle misure da usare nell'argomento **on Rows** .
     + `slicers()` Specificare un campo o i membri da usare come filtro dei dati. Si tratta di un filtro che viene applicato a tutti i dati delle query MDX.
     
     + `axis()` Specificare il nome di un altro asse da usare nella query. 
     
         Un cubo OLAP può contenere un massimo di 128 assi di query. In genere, i primi quattro assi sono detti **colonne**, **righe**, **pagine**e capitoli. 
         
         Se la query è relativamente semplice, è possibile usare le funzioni `columns`, `rows`e così via per crearla. È tuttavia possibile usare anche la funzione `axis()` con un valore di indice diverso da zero per creare una query MDX con molti qualificatori o aggiungere altre dimensioni come qualificatori.

5. Passare l'handle e la query MDX completata in una delle funzioni seguenti, a seconda della forma dei risultati: 

  + `executeMD` restituisce una matrice multidimensionale
  + `execute2D` restituisce un frame di dati bidimensionale (tabulare)

## <a name="executeMDX"></a>Eseguire una query MDX valida da R

1. Definire una stringa di connessione che specifica l'origine dati OLAP (istanza di SSAS) e il provider MSOLAP.

2. Usare la funzione `OlapConnection(connectionString)` per creare un handle per la query MDX e passare la stringa di connessione.

3. Definire una variabile R per archiviare il testo della query MDX.

4. Passare l'handle e la variabile contenente la query MDX nella funzione `executeMD` o `execute2D`, a seconda della forma dei risultati.

    + `executeMD` restituisce una matrice multidimensionale
    + `execute2D` restituisce un frame di dati bidimensionale (tabulare)

## <a name="examples"></a>Esempi

Gli esempi seguenti si basano sul progetto AdventureWorks data mart e Cube, perché il progetto è ampiamente disponibile, in più versioni, inclusi i file di backup che possono essere facilmente ripristinati per Analysis Services. Se non si dispone di un cubo esistente, ottenere un cubo di esempio utilizzando una di queste opzioni:

+ Creare il cubo utilizzato in questi esempi seguendo le Analysis Services Esercitazione fino alla lezione 4: [Creazione di un cubo OLAP](https://docs.microsoft.com/analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial)

+ Scaricare un cubo esistente come backup e ripristinarlo in un'istanza di Analysis Services. Questo sito, ad esempio, fornisce un cubo completamente elaborato in formato compresso: [Modello multidimensionale di Adventure Works SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334). Estrarre il file e quindi ripristinarlo nell'istanza di SSAS. Per altre informazioni, vedere [backup e ripristino](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)o [cmdlet Restore-ASDatabase](https://docs.microsoft.com/analysis-services/powershell/restore-asdatabase-cmdlet).

### <a name="1-basic-mdx-with-slicer"></a>1. Query MDX di base con filtro dei dati

Questa query MDX seleziona le _misure_ per il conteggio e la quantità di Internet sales count e Sales amount e li inserisce nell'asse Column. Aggiunge un membro della dimensione SalesTerritory come *filtro dei dati*per filtrare la query in modo da includere nei calcoli solo le vendite relative all'Australia.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ Nelle colonne è possibile specificare più misure come elementi di una stringa con valori delimitati da virgole.
+ L'asse Row usa tutti i valori possibili (tutti i MEMBERS) della dimensione "Product Line". 
+ Questa query restituisce una tabella con tre colonne contenenti un riepilogo _cumulativo_ delle vendite Internet di tutti i paesi.
+ La clausola WHERE specifica l' _asse_di sezionamento. In questo esempio, il filtro dei dati utilizza un membro della dimensione **SalesTerritory** per filtrare la query in modo da utilizzare solo le vendite dell'Australia nei calcoli.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>Per compilare la query con le funzioni di olapR

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

Per un'istanza denominata, assicurarsi di eseguire l'escape di tutti i caratteri che possono essere considerati caratteri di controllo in R.  La stringa di connessione seguente, ad esempio, fa riferimento a un'istanza OLAP01, in un server denominato ContosoHQ:

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>Per eseguire la query come stringa MDX predefinita

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Se si definisce una query utilizzando il Generatore MDX in SQL Server Management Studio e quindi si salva la stringa MDX, il numero di assi verrà numerato a partire da 0, come illustrato di seguito: 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

La query può sempre essere eseguita come stringa MDX predefinita. Tuttavia, per compilare la stessa query usando R usando la `axis()` funzione, è necessario rinumerare gli assi a partire da 1.

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Esplorare i cubi e i relativi campi in un'istanza di SSAS

È possibile usare la funzione `explore` per restituire un elenco di cubi, dimensioni o membri da usare per creare una query. Questa funzione è utile se non si può accedere ad altri strumenti di esplorazione OLAP o se si desidera modificare o creare la query MDX a livello di codice.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>Per elencare i cubi disponibili per la connessione specificata

Per visualizzare tutti i cubi o le prospettive dell'istanza per i quali si dispone dei diritti di visualizzazione, specificare l'handle come argomento di `explore`.

> [!IMPORTANT]
> Il risultato finale **non** è un cubo. TRUE indica semplicemente che l'operazione sui metadati è stata completata. Se gli argomenti non sono validi, viene generato un errore.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| Risultati  |
| ----|
| _Analysis Services Tutorial_|
|_Internet Sales_|
|_Reseller Sales_|
|_Sales Summary_|
|_[1] TRUE_|

#### <a name="to-get-a-list-of-cube-dimensions"></a>Per ottenere un elenco delle dimensioni del cubo

Per visualizzare tutte le dimensioni del cubo o della prospettiva, specificare il nome del cubo o della prospettiva.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| Risultati  |
| ----|
| _Customer_|
|_Date_|
|_Region_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>Per restituire tutti i membri della dimensione e della gerarchia specificate

Dopo aver definito l'origine e la creazione dell'handle, specificare il cubo, la dimensione e la gerarchia da restituire. Nei risultati restituiti gli elementi con **->** prefisso rappresentano elementi figlio del membro precedente.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| Risultati  |
| ----|
| _Accessories_|
|_Bikes_|
|_Clothing_|
|_Components_|
|-> Assembly Components|
|-> Assembly Components|


## <a name="see-also"></a>Vedere anche

[Uso di dati da cubi OLAP in R](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)

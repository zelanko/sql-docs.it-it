---
title: Stimare le dimensioni di un indice cluster | Microsoft Docs
description: Usare questa procedura per valutare la quantità di spazio necessaria per l'archiviazione dei dati in un indice cluster in SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || >= sql-server-2016
ms.openlocfilehash: d963a8745d83be039fa2970a24d04a2a882bf7a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478362"
---
# <a name="estimate-the-size-of-a-clustered-index"></a>Stima delle dimensioni di un indice cluster

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Per stimare la quantità di spazio necessaria per l'archiviazione dati in un indice cluster, è possibile utilizzare la procedura seguente:  
  
1.  Calcolare lo spazio utilizzato per archiviare dati nel livello foglia dell'indice cluster.  
  
2.  Calcolare lo spazio utilizzato per archiviare le informazioni sugli indici per l'indice cluster.  
  
3.  Sommare i valori calcolati.  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>Passaggio 1. Calcolare lo spazio utilizzato per l'archiviazione di dati nel livello foglia  
  
1.  Specificare il numero di righe che verranno incluse nella tabella:  
  
     ***Num_Rows** _ = numero di righe della tabella  
  
2.  Specificare il numero di colonne di lunghezza fissa e e variabile e calcolare lo spazio necessario per la loro archiviazione:  
  
     Calcolare lo spazio occupato da ognuno di questi gruppi di colonne all'interno della riga di dati. Le dimensioni di una colonna dipendono dal tipo di dati e dalla lunghezza specificata.  
  
     _*_Num_Cols_*_ = numero totale di colonne (a lunghezza fissa e a lunghezza variabile)  
  
     _*_Fixed_Data_Size_*_ = dimensioni totali in byte di tutte le colonne a lunghezza fissa  
  
     _*_Num_Variable_Cols_*_ = numero di colonne a lunghezza variabile  
  
     _*_Max_Var_Size_*_ = dimensioni massime in byte di tutte le colonne a lunghezza variabile  
  
3.  Se l'indice cluster è non univoco, considerare la colonna _uniqueifier*:  
  
     La colonna uniqueifier è una colonna a lunghezza variabile che ammette valori Null. Sarà una colonna non Null da 4 byte nelle righe che includono valori chiave non univoci. Questo valore fa parte della chiave di indice ed è necessario per garantire che ogni riga includa un valore di chiave univoco.  
  
     ***Num_Cols** _ = _*_Num_Cols_*_ + 1  
  
     _*_Num_Variable_Cols_*_  = _*_Num_Variable_Cols_*_ + 1  
  
     _*_Max_Var_Size_*_  = _*_Max_Var_Size_*_ + 4  
  
     In queste modifiche si presuppone che tutti i valori siano non univoci.  
  
4.  Parte della riga, nota come mappa di bit null, è riservata alla gestione del supporto dei valori Null in una colonna. Calcolarne le dimensioni:  
  
     _*_Null_Bitmap_*_ = 2 + ((_*_Num_Cols_*_ + 7) / 8)  
  
     Utilizzare solo la parte intera del risultato dell'espressione indicata in precedenza, eliminando eventuali residui.  
  
5.  Calcolare le dimensioni dei dati di lunghezza variabile:  
  
     Se la tabella include colonne di lunghezza variabile, determinare la quantità di spazio utilizzata per l'archiviazione delle colonne nella riga:  
  
     _*_Variable_Data_Size_*_ = 2 + (_*_Num_Variable_Cols_*_ x 2) + _*_Max_Var_Size_*_  
  
     I byte aggiunti a _*_Max_Var_Size_*_ servono a tenere traccia di ogni colonna variabile. Questa formula si basa sul presupposto che tutte le colonne a lunghezza variabile siano piene al 100%. Se si prevede che verrà usata una percentuale inferiore dello spazio di archiviazione delle colonne a lunghezza variabile, è possibile modificare il valore di _*_Max_Var_Size_*_ in base a tale percentuale per ottenere una stima più accurata delle dimensioni complessive della tabella.  
  
    > [!NOTE]  
    >  È possibile combinare colonne _*varchar**, **nvarchar**, **varbinary** o **sql_variant** che causano il superamento di 8.060 byte per la larghezza totale definita della tabella. La lunghezza di ogni colonna deve essere compresa nel limite di 8.000 byte per una colonna **varchar**, **varbinary** o **sql_variant** e di 4.000 byte per le colonne **nvarchar** . Le larghezze combinate di tali colonne possono tuttavia superare il limite di 8.060 byte in una tabella.  
  
     Se non sono presenti colonne di lunghezza variabile, impostare **_Variable_Data_Size_* _ su 0.  
  
6.  Calcolare le dimensioni totali della riga:  
  
     _*_Row_Size_*_  = _*_Fixed_Data_Size_*_ + _*_Variable_Data_Size_*_ + _*_Null_Bitmap_*_ + 4  
  
     Il valore 4 rappresenta l'overhead dell'intestazione di riga di una riga di dati.  
  
7.  Calcolare il numero di righe per pagina (8096 byte liberi per pagina):  
  
     _*_Rows_Per_Page_*_ = 8096 / (_*_Row_Size_*_ + 2)  
  
     Poiché le righe non si estendono su più pagine, il numero di righe per pagina deve essere arrotondato alla riga completa più vicina. Il valore 2 nella formula è per la voce di riga nella matrice di slot della pagina.  
  
8.  Calcolare il numero di righe libere riservate per pagina, in base al [fattore di riempimento](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) specificato:  
  
     _*_Free_Rows_Per_Page_*_ = 8096 x ((100 - _*_Fill_Factor_*_) / 100) / (_*_Row_Size_*_ + 2)  
  
     Il fattore di riempimento utilizzato nel calcolo è un valore intero, non una percentuale. Poiché le righe non si estendono su più pagine, il numero di righe per pagina deve essere arrotondato alla riga completa più vicina. Aumentando il fattore di riempimento, in ciascuna pagina verrà archiviata una quantità maggiore di dati e il numero di pagine diminuirà. Il valore 2 nella formula è per la voce di riga nella matrice di slot della pagina.  
  
9. Calcolare il numero di pagine necessario per archiviare tutte le righe:  
  
     _*_Num_Leaf_Pages_*_  = _*_Num_Rows_*_ / (_*_Rows_Per_Page_*_ - _*_Free_Rows_Per_Page_*_ )  
  
     Il numero di pagine stimato deve essere arrotondato alla pagina intera più vicina.  
  
10. Calcolare la quantità di spazio necessaria per l'archiviazione dei dati nel livello foglia (8192 byte totali per pagina):  
  
     _*_Leaf_space_used_*_ = 8192 x _*_Num_Leaf_Pages_*_  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>Passaggio 2. Calcolare lo spazio utilizzato per l'archiviazione di informazioni sull'indice  
 Per stimare la quantità di spazio necessario per archiviare i livelli superiori dell'indice, è possibile utilizzare la seguente procedura:  
  
1.  Specificare il numero di colonne a lunghezza fissa e a lunghezza variabile incluse nella chiave dell'indice e calcolare lo spazio necessario per archiviarle:  
  
     Le colonne chiave di un indice possono includere colonne a lunghezza fissa e a lunghezza variabile. Per stimare le dimensioni delle righe di indice di livello interno, calcolare lo spazio occupato da ognuno di questi gruppi di colonne all'interno della riga di indice. Le dimensioni di una colonna dipendono dal tipo di dati e dalla lunghezza specificata.  
  
     _*_Num_Key_Cols_*_ = numero totale di colonne chiave (a lunghezza fissa e a lunghezza variabile)  
  
     _*_Fixed_Key_Size_*_ = dimensioni totali in byte di tutte le colonne chiave a lunghezza fissa  
  
     _*_Num_Variable_Key_Cols_*_ = numero di colonne chiave a lunghezza variabile  
  
     _*_Max_Var_Key_Size_*_ = dimensioni massime in byte di tutte le colonne chiave a lunghezza variabile  
  
2.  Considerare le eventuali colonne uniqueifier necessarie se l'indice è non univoco:  
  
     La colonna uniqueifier è una colonna a lunghezza variabile che ammette valori Null. Sarà una colonna non Null da 4 byte nelle righe che includono valori chiave di indice non univoci. Questo valore fa parte della chiave di indice ed è necessario per garantire che ogni riga includa un valore di chiave univoco.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + 1  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + 1  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + 4  
  
     In queste modifiche si presuppone che tutti i valori siano non univoci.  
  
3.  Calcolare le dimensioni della mappa di bit Null:  
  
     Se nella chiave di indice sono incluse colonne che ammettono valori Null, una parte della riga di indice viene riservata per la mappa di bit Null. Calcolarne le dimensioni:  
  
     _*_Index_Null_Bitmap_*_ =  2 + ((numero di colonne nella riga di indice + 7) / 8)  
  
     Deve essere utilizzata solo la parte Integer dell'espressione precedente. Eliminare le parti restanti.  
  
     Se invece non sono disponibili colonne chiave che ammettono i valori Null, impostare _*_Index_Null_Bitmap_*_ su 0.  
  
4.  Calcolare le dimensioni dei dati di lunghezza variabile:  
  
     Se l'indice include colonne a lunghezza variabile, determinare la quantità di spazio utilizzata per l'archiviazione delle colonne nella riga di indice:  
  
     _*_Variable_Key_Size_*_ = 2 + (_*_Num_Variable_Key_Cols_*_ x 2) + _*_Max_Var_Key_Size_*_  
  
     I byte aggiunti a _*_Max_Var_Key_Size_*_ servono a tenere traccia di ogni colonna a lunghezza variabile. Questa formula si basa sul presupposto che tutte le colonne a lunghezza variabile siano piene al 100%. Se si prevede una percentuale inferiore di uso dello spazio di archiviazione delle colonne a lunghezza variabile, è possibile modificare il valore di _*_Max_Var_Key_Size_*_ in base a tale percentuale per ottenere una stima più accurata delle dimensioni complessive della tabella.  
  
     Se non sono disponibili colonne a lunghezza variabile, impostare _*_Variable_Key_Size_*_ su 0.  
  
5.  Calcolare le dimensioni della riga di indice:  
  
     _*_Index_Row_Size_*_  = _*_Fixed_Key_Size_*_ + _*_Variable_Key_Size_*_ + _*_Index_Null_Bitmap_*_ + 1 (per l'overhead dell'intestazione di una riga di indice) + 6 (per il puntatore ID della pagina figlio)  
  
6.  Calcolare il numero di righe di indice per pagina (8096 byte liberi per pagina):  
  
     _*_Index_Rows_Per_Page_*_ = 8096 / (_*_Index_Row_Size_*_ + 2)  
  
     Poiché le righe di indice non si estendono su più pagine, il numero di righe di indice per pagina deve essere arrotondato alla riga completa più vicina. Il numero 2 nella formula si riferisce alla voce della riga nella matrice di slot della pagina.  
  
7.  Calcolare il numero di livelli nell'indice:  
  
     _*_Non-leaf_Levels_*_ = 1 + log (Index_Rows_Per_Page) (_*_Num_Leaf_Pages_*_ / _*_Index_Rows_Per_Page_*_)  
  
     Arrotondare questo valore per eccesso al numero intero più vicino. Nel valore non è incluso il livello foglia dell'indice cluster.  
  
8.  Calcolare il numero di pagine non foglia dell'indice:  
  
     _*_Num_Index_Pages =_*_ ∑Level _*_ (Num_Leaf_Pages / (Index_Rows_Per_Page_ *_^Level_* _))_ *_  
  
     dove 1 <= Level <= _*_Non-leaf_Levels_*_  
  
     Arrotondare ogni addendo al numero intero più vicino. Per un esempio semplice, considerare un indice in cui _*_Num_Leaf_Pages_*_ = 1000 e _*_Index_Rows_Per_Page_*_ = 25. Nel primo livello dell'indice sopra il livello foglia vengono archiviate 1000 righe di indice, ovvero una riga di indice per pagina foglia, ed è possibile inserire 25 righe di indice per pagina. Per archiviare le 1000 righe di indice, sono quindi necessarie 40 pagine. Nel livello successivo dell'indice devono invece essere archiviate 40 righe, pertanto sono necessarie 2 pagine. Nel livello finale dell'indice devono essere archiviate 2 righe, pertanto è necessaria una sola pagina. Si ottengono quindi 43 pagine di indice non foglia. Se nella formula precedente si utilizzano questi numeri, il risultato sarà il seguente:  
  
     _*_Non-leaf_Levels_*_ = 1 + log(25) (1000 / 25) = 3  
  
     _*_Num_Index_Pages_*_ = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, ovvero il numero di pagine descritto nell'esempio.  
  
9. Calcolare le dimensioni dell'indice (8192 byte totali per pagina):  
  
     _*_Index_Space_Used_*_ = 8192 x _*_Num_Index_Pages_*_  
  
## <a name="step-3-total-the-calculated-values"></a>Passaggio 3. Sommare i valori calcolati  
 Sommare i valori ottenuti nei due passaggi precedenti:  
  
 Dimensioni indice cluster (byte) = _*_Leaf_Space_Used_*_ + _*_Index_Space_used_*_  
  
 Il calcolo non prende in considerazione i fattori seguenti:  
  
-   Partizionamento  
  
     L'overhead dello spazio derivante dal partizionamento è minimo, ma difficile da calcolare. Non è fondamentale includerlo.  
  
-   Pagine di allocazione  
  
     Esiste almeno una pagina IAM utilizzata per tenere traccia delle pagine allocate su un heap, ma l'overhead dello spazio è minimo e non è presente alcun algoritmo per calcolare in modo deterministico l'esatto numero di pagine IAM che verranno utilizzate.  
  
-   Valori LOB  
  
     L'algoritmo per determinare con esattezza la quantità di spazio usata per archiviare i tipi di dati LOB _*varchar(max)**, **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml** e **image** è complesso. È sufficiente aggiungere le dimensioni medie dei valori LOB previste, moltiplicare per **_Num_Rows_** e quindi aggiungere il valore ottenuto alle dimensioni totali dell'indice cluster.  
  
-   Compressione  
  
     Non è possibile pre-calcolare la dimensione di un indice compresso.  
  
-   Colonne di tipo sparse  
  
     Per informazioni sui requisiti di spazio delle colonne di tipo sparse, vedere [Utilizzo di colonne di tipo sparse](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Descrizione di indici cluster e non cluster.](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Stima delle dimensioni di una tabella](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Creare indici cluster](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Creare indici non cluster](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Stima delle dimensioni di un indice non cluster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Stima delle dimensioni di un heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Stima delle dimensioni di un database](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  

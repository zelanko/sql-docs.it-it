---
title: Stimare le dimensioni di un indice non cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa4b0d73d1cba3d612da9f666bb548dfbc54102f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054115"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Stima delle dimensioni di un indice non cluster
  Per stimare la quantità di spazio necessaria per archiviare un indice non cluster, effettuare le operazioni seguenti:  
  
1.  Calcolare le variabili da utilizzare nei passaggi 2 e 3.  
  
2.  Calcolare lo spazio utilizzato per l'archiviazione di informazioni sull'indice nel livello foglia dell'indice non cluster.  
  
3.  Calcolare lo spazio utilizzato per l'archiviazione di informazioni sull'indice nei livelli non foglia dell'indice non cluster.  
  
4.  Sommare i valori calcolati.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Passaggio 1. Calcolare le variabili da utilizzare nei passaggi 2 e 3  
 Per calcolare le variabili utilizzate per stimare la quantità di spazio necessario per archiviare i livelli superiori dell'indice, è possibile effettuare le operazioni seguenti:  
  
1.  Specificare il numero di righe che verranno incluse nella tabella:  
  
     ***Num_Rows***  = numero di righe della tabella  
  
2.  Specificare il numero di colonne a lunghezza fissa e a lunghezza variabile incluse nella chiave dell'indice e calcolare lo spazio necessario per archiviarle:  
  
     Le colonne chiave di un indice possono includere colonne a lunghezza fissa e a lunghezza variabile. Per stimare le dimensioni delle righe di indice di livello interno, calcolare lo spazio occupato da ognuno di questi gruppi di colonne all'interno della riga di indice. Le dimensioni di una colonna dipendono dal tipo di dati e dalla lunghezza specificata.  
  
     ***Num_Key_Cols***  = numero totale di colonne chiave (a lunghezza fissa e a lunghezza variabile)  
  
     ***Fixed_Key_Size***  = dimensioni totali in byte di tutte le colonne chiave a lunghezza fissa  
  
     ***Num_Variable_Key_Cols***  = numero di colonne chiave a lunghezza variabile  
  
     ***Max_Var_Key_Size***  = dimensioni massime in byte di tutte le colonne chiave a lunghezza variabile  
  
3.  Considerare anche l'indicatore di posizione delle righe di dati, necessario se l'indice non è univoco:  
  
     Se l'indice non cluster non è univoco, l'indicatore di posizione delle righe di dati viene combinato con la chiave dell'indice non cluster in modo da ottenere un valore di chiave univoco per ciascuna riga.  
  
     Se l'indice non cluster è su un heap, l'indicatore di posizione delle righe di dati corrisponde al RID dell'heap, le cui dimensioni sono pari a 8 byte.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     Se l'indice non cluster è su un indice cluster, l'indicatore di posizione delle righe di dati corrisponde alla chiave di clustering. Le colonne da combinare con la chiave dell'indice non cluster sono le colonne della chiave di clustering non incluse già nel set di colonne chiave dell'indice non cluster.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + numero di colonne chiave di clustering non nel set di colonne chiave di indice non cluster (+ 1 se l'indice cluster è non univoco)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + dimensioni totali in byte delle colonne chiave di clustering a lunghezza fissa non nel set di colonne chiave di indice non cluster  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + numero di colonne chiave di clustering a lunghezza variabile non nel set di colonne chiave di indice non cluster (+ 1 se l'indice cluster è non univoco)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + dimensioni massime in byte delle colonne chiave di clustering a lunghezza variabile non nel set di colonne chiave di indice non cluster (+ 4 se l'indice cluster è non univoco)  
  
4.  È possibile riservare parte della riga, nota come mappa di bit Null, per la gestione del supporto dei valori Null della colonna. Calcolarne le dimensioni:  
  
     Se sono presenti colonne che ammettono i valori Null nella chiave dell'indice, incluse le eventuali colonne chiave di clustering necessarie descritte al passaggio 1.3, parte della riga di indice viene riservata alla mappa di bit Null.  
  
     ***Index_Null_Bitmap***  = 2 + ((numero di colonne nella riga di indice + 7) / 8)  
  
     Deve essere utilizzata solo la parte Integer dell'espressione precedente. Eliminare le parti restanti.  
  
     Se invece non sono disponibili colonne chiave che ammettono i valori Null, impostare ***Index_Null_Bitmap*** su 0.  
  
5.  Calcolare le dimensioni dei dati a lunghezza variabile:  
  
     Se sono presenti colonne a lunghezza variabile nella chiave dell'indice, incluse eventuali colonne chiave dell'indice cluster necessarie, determinare lo spazio utilizzato per archiviare le colonne all'interno della riga di indice:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     I byte aggiunti a ***Max_Var_Key_Size*** servono a tenere traccia di ogni colonna variabile. Questa formula si basa sul presupposto che tutte le colonne a lunghezza variabile siano piene al 100%. Se si prevede una percentuale inferiore di utilizzo dello spazio di archiviazione delle colonne a lunghezza variabile, è possibile modificare il valore di ***Max_Var_Key_Size*** in base a tale percentuale per ottenere una stima più accurata delle dimensioni complessive della tabella.  
  
     Se non sono disponibili colonne a lunghezza variabile, impostare ***Variable_Key_Size*** su 0.  
  
6.  Calcolare le dimensioni della riga di indice:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (per l'overhead dell'intestazione di una riga di indice) + 6 (per il puntatore ID della pagina figlio)  
  
7.  Calcolare il numero di righe di indice per pagina (8096 byte liberi per pagina):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Poiché le righe di indice non si estendono su più pagine, il numero di righe di indice per pagina deve essere arrotondato alla riga completa più vicina. Il numero 2 nella formula si riferisce alla voce della riga nella matrice di slot della pagina.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Passaggio 2. Calcolare lo spazio utilizzato per l'archiviazione di informazioni sull'indice nel livello foglia  
 Per stimare la quantità di spazio necessaria per archiviare il livello foglia dell'indice, effettuare le operazioni seguenti. Per completare questo passaggio, sono necessari i valori preservati al passaggio 1.  
  
1.  Specificare il numero di colonne a lunghezza fissa e a lunghezza variabile incluse a livello foglia e calcolare lo spazio necessario per archiviarle:  
  
    > [!NOTE]  
    >  È possibile estendere un indice non cluster includendo colonne non chiave oltre alle colonne chiave. Tali colonne aggiuntive vengono archiviate solo al livello foglia dell'indice non cluster. Per altre informazioni, vedere [Creare indici con colonne incluse](../indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  È possibile combinare colonne `varchar`, `nvarchar`, `varbinary` o `sql_variant` che fanno eccedere gli 8.060 byte per la larghezza totale definita della tabella. La lunghezza di ogni colonna deve essere compresa nel limite di 8.000 byte per una colonna `varchar`, `varbinary` o `sql_variant` e di 4.000 byte per le colonne `nvarchar`. Le larghezze combinate di tali colonne possono tuttavia superare il limite di 8.060 byte in una tabella. Lo stesso vale inoltre per le righe foglia dell'indice non cluster che presentano colonne incluse.  
  
     Se l'indice non cluster non dispone di colonne incluse, utilizzare i valori del passaggio 1, incluse le eventuali modifiche determinate al passaggio 1.3:  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     Se l'indice non cluster dispone di colonne incluse, aggiungere i valori appropriati a quelli del passaggio 1, incluse le eventuali modifiche del passaggio 1.3. Le dimensioni di una colonna dipendono dal tipo di dati e dalla lunghezza specificata. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + numero di colonne incluse  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + dimensioni massime in byte di tutte le colonne incluse a lunghezza fissa  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + number of variable-length included columns  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + dimensioni massime in byte di tutte le colonne incluse a lunghezza variabile  
  
2.  Considerare l'indicatore di posizione delle righe di dati:  
  
     Se l'indice non cluster non è univoco, l'overhead per l'indicatore di posizione delle righe di dati è già stato considerato al passaggio 1.3 e non sono richieste modifiche ulteriori. Procedere con il passaggio successivo.  
  
     Se l'indice non cluster è univoco, è necessario considerare l'indicatore di posizione delle righe di dati per tutte le righe al livello foglia.  
  
     Se l'indice non cluster è su un heap, l'indicatore di posizione delle righe di dati corrisponde al RID dell'heap, ovvero a 8 byte.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     Se l'indice non cluster è su un indice cluster, l'indicatore di posizione delle righe di dati corrisponde alla chiave di clustering. Le colonne da combinare con la chiave dell'indice non cluster sono le colonne della chiave di clustering non incluse già nel set di colonne chiave dell'indice non cluster.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + numero di colonne chiave di clustering non nel set di colonne chiave di indice non cluster (+ 1 se l'indice cluster è non univoco)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + numero di colonne chiave di clustering a lunghezza fissa non nel set di colonne chiave di indice non cluster  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + numero di colonne chiave di clustering a lunghezza variabile non nel set di colonne chiave di indice non cluster (+ 1 se l'indice cluster è non univoco)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + dimensione in byte delle colonne chiave di clustering a lunghezza variabile non nel set di colonne chiave di indice non cluster (+ 4 se l'indice cluster è non univoco)  
  
3.  Calcolare le dimensioni della mappa di bit Null:  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     Deve essere utilizzata solo la parte Integer dell'espressione precedente. Eliminare le parti restanti.  
  
4.  Calcolare le dimensioni dei dati a lunghezza variabile:  
  
     Se sono presenti colonne a lunghezza variabile nella chiave dell'indice, incluse eventuali colonne chiave di clustering necessarie descritte al passaggio 2.2, determinare lo spazio utilizzato per archiviare le colonne all'interno della riga di indice:  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     I byte aggiunti a ***Max_Var_Key_Size*** servono a tenere traccia di ogni colonna variabile. Questa formula si basa sul presupposto che tutte le colonne a lunghezza variabile siano piene al 100%. Se si prevede una percentuale inferiore di utilizzo dello spazio di archiviazione delle colonne di lunghezza variabile, è possibile modificare il valore ***Max_Var_Leaf_Size*** in base a tale percentuale per ottenere una stima più precisa delle dimensioni complessive della tabella.  
  
     Se non sono disponibili colonne a lunghezza variabile, impostare ***Variable_Leaf_Size*** su 0.  
  
5.  Calcolare le dimensioni della riga di indice:  
  
     ***Leaf_Row_Size***  = ***Fixed_Leaf_Size*** + ***Variable_Leaf_Size*** + ***Leaf_Null_Bitmap*** + 1 (per l'overhead dell'intestazione di una riga di indice) + 6 (per il puntatore ID della pagina figlio)  
  
6.  Calcolare il numero di righe di indice per pagina (8096 byte liberi per pagina):  
  
     ***Leaf_Rows_Per_Page***  = 8096 / (***Leaf_Row_Size*** + 2)  
  
     Poiché le righe di indice non si estendono su più pagine, il numero di righe di indice per pagina deve essere arrotondato alla riga completa più vicina. Il numero 2 nella formula si riferisce alla voce della riga nella matrice di slot della pagina.  
  
7.  Calcolare il numero di righe libere riservate per pagina, sulla base del [fattore di riempimento](../indexes/specify-fill-factor-for-an-index.md) specificato:  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Leaf_Row_Size*** + 2)  
  
     Il fattore di riempimento utilizzato nel calcolo è un valore intero, non una percentuale. Poiché le righe non si estendono su più pagine, il numero di righe per pagina deve essere arrotondato alla riga completa più vicina. Aumentando il fattore di riempimento, in ciascuna pagina verrà archiviata una quantità maggiore di dati e il numero di pagine diminuirà. Il numero 2 nella formula si riferisce alla voce della riga nella matrice di slot della pagina.  
  
8.  Calcolare il numero di pagine necessario per archiviare tutte le righe:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     Il numero di pagine stimato deve essere arrotondato alla pagina intera più vicina.  
  
9. Calcolare le dimensioni dell'indice (8192 byte totali per pagina):  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Passaggio 3. Calcolare lo spazio utilizzato per l'archiviazione di informazioni sull'indice nei livelli non foglia  
 Per stimare la quantità di spazio necessaria per archiviare i livelli intermedio e radice dell'indice, effettuare le operazioni seguenti: Per completare questo passaggio, sono necessari i valori preservati ai passaggi 2 e 3.  
  
1.  Calcolare il numero di livelli non foglia dell'indice:  
  
     ***I livelli non foglia*** = 1 + log Index_Rows_Per_Page (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     Arrotondare questo valore per eccesso al numero intero più vicino. Nel valore non è incluso il livello foglia dell'indice non cluster.  
  
2.  Calcolare il numero di pagine non foglia dell'indice:  
  
     ***Num_Index_Pages*** = ∑ Level (***Num_Leaf_Pages/Index_Rows_Per_Page***<sup>livello</sup>) dove 1 < = Level < = ***livelli***  
  
     Arrotondare ogni addendo al numero intero più vicino. Per un esempio semplice, considerare un indice in cui ***Num_Leaf_Pages*** = 1000 e ***Index_Rows_Per_Page*** = 25. Nel primo livello dell'indice sopra il livello foglia vengono archiviate 1000 righe di indice, ovvero una riga di indice per pagina foglia, ed è possibile inserire 25 righe di indice per pagina. Per archiviare le 1000 righe di indice, sono quindi necessarie 40 pagine. Nel livello successivo dell'indice devono invece essere archiviate 40 righe, pertanto sono necessarie 2 pagine. Nel livello finale dell'indice devono essere archiviate 2 righe, pertanto è necessaria una sola pagina. Si ottengono quindi 43 pagine di indice non foglia. Se nella formula precedente si utilizzano questi numeri, il risultato sarà il seguente:  
  
     ***Non leaf Levels*** = 1 + log25 (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000 /(25<sup>3</sup>) + 1000 / (25<sup>2</sup>) + 1000 / (25<sup>1</sup>) = 1 + 2 + 40 = 43, ovvero il numero di pagine descritto nell'esempio.  
  
3.  Calcolare le dimensioni dell'indice (8192 byte totali per pagina):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>Passaggio 4. Sommare i valori calcolati  
 Sommare i valori ottenuti nei due passaggi precedenti:  
  
 Dimensioni indice non cluster (byte) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 Il calcolo non prende in considerazione i fattori seguenti:  
  
-   Partizionamento  
  
     L'overhead dello spazio derivante dal partizionamento è minimo, ma difficile da calcolare. Non è fondamentale includerlo.  
  
-   Pagine di allocazione  
  
     Esiste almeno una pagina IAM utilizzata per tenere traccia delle pagine allocate su un heap, ma l'overhead dello spazio è minimo e non è presente alcun algoritmo per calcolare in modo deterministico l'esatto numero di pagine IAM che verranno utilizzate.  
  
-   Valori LOB  
  
     L'algoritmo per determinare con esattezza la quantità di spazio utilizzata per archiviare i tipi di dati LOB `varchar(max)`, `varbinary(max)`, `nvarchar(max)`, `text`, `ntext`, `xml` e `image` è complesso. È comunque sufficiente aggiungere le dimensioni medie dei valori LOB previsti, moltiplicarle per ***Num_Rows***e aggiungere il prodotto alle dimensioni totali dell'indice non cluster.  
  
-   Compressione  
  
     Non è possibile pre-calcolare la dimensione di un indice compresso.  
  
-   Colonne di tipo sparse  
  
     Per informazioni sui requisiti di spazio delle colonne di tipo sparse, vedere [Usare le colonne di tipo sparse](../tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Descrizione di indici cluster e non cluster.](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [Creare indici non cluster](../indexes/create-nonclustered-indexes.md)   
 [Creare indici cluster](../indexes/create-clustered-indexes.md)   
 [Stima delle dimensioni di una tabella](estimate-the-size-of-a-table.md)   
 [Stima delle dimensioni di un indice cluster](estimate-the-size-of-a-clustered-index.md)   
 [Stima delle dimensioni di un heap](estimate-the-size-of-a-heap.md)   
 [Stima delle dimensioni di un database](estimate-the-size-of-a-database.md)  
  
  

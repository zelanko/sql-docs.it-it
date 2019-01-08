---
title: Trasformazione Raggruppamento fuzzy | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0108e55f6038b234d78f3fd66d9bae243af28a9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357350"
---
# <a name="fuzzy-grouping-transformation"></a>Raggruppamento fuzzy - trasformazione
  La trasformazione Raggruppamento fuzzy consente di eseguire attività di pulizia dei dati identificando le righe che con maggiore probabilità sono duplicate e selezionando una riga canonica di dati da utilizzare per la standardizzazione dei dati.  
  
> [!NOTE]  
>  Per informazioni dettagliate sulla trasformazione Raggruppamento fuzzy, inclusi i limiti di memoria e prestazioni, vedere il white paper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604).  
  
 La trasformazione Raggruppamento fuzzy richiede la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la creazione delle tabelle temporanee di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] necessarie all'algoritmo di trasformazione. La connessione deve corrispondere a un utente autorizzato che dispone dell'autorizzazione per la creazione di tabelle nel database.  
  
 Per configurare la trasformazione, è necessario selezionare le colonne di input da usare per l'identificazione di duplicati e il tipo di corrispondenza, fuzzy o esatta, per ogni colonna. Con una corrispondenza esatta vengono raggruppate solo le righe della colonna contenenti gli stessi valori. Questo tipo di corrispondenza può essere applicato alle colonne con qualsiasi tipo di dati di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , ad eccezione di DT_TEXT, DT_NTEXT e DT_IMAGE. Con una corrispondenza fuzzy vengono raggruppate le righe contenenti valori simili. Questo tipo di corrispondenza è basato su un punteggio di somiglianza specificato dall'utente. Nella corrispondenza fuzzy è possibile utilizzare solo colonne con tipo di dati DT_WSTR o DT_STR. Per altre informazioni, vedere [Tipi di dati di Integration Services](../integration-services-data-types.md).  
  
 L'output della trasformazione include tutte le colonne di input, una o più colonne con dati standardizzati e una colonna contenente il punteggio di somiglianza. Il punteggio è un valore decimale compreso tra 0 e 1. La riga canonica ha un punteggio di 1. Le altre righe nel raggruppamento fuzzy hanno punteggi che indicano il livello di corrispondenza di queste righe rispetto alla riga canonica. I punteggi più prossimi a 1 indicano una corrispondenza maggiore. Se il raggruppamento fuzzy include righe che sono duplicati esatti della riga canonica, anche queste righe avranno un punteggio di 1. La trasformazione non rimuove le righe duplicate ma le raggruppa creando una chiave di correlazione tra la riga canonica e queste righe.  
  
 La trasformazione restituisce una riga di output per ogni riga di input oltre alle colonne aggiuntive seguenti:  
  
-   **_key_in**, colonna che identifica in modo univoco ogni riga.  
  
-   **_key_out**, colonna che identifica un gruppo di righe duplicate. Il valore della colonna **_key_out** corrisponde al valore della colonna **_key_in** nella riga di dati canonica. Le righe della colonna **_key_out** aventi lo stesso valore fanno parte dello stesso gruppo. Il valore di **_key_out**di un gruppo corrisponde al valore **_key_in** nella riga di dati canonica.  
  
-   **_score**, valore compreso tra 0 e 1 che indica la somiglianza della riga di input con la riga canonica.  
  
 È possibile configurare la trasformazione Raggruppamento fuzzy specificando nomi di colonna diversi da questi nomi predefiniti. Anche nell'output è indicato un punteggio di somiglianza per ogni colonna di un gruppo fuzzy.  
  
 La trasformazione Raggruppamento fuzzy include due caratteristiche per la personalizzazione del raggruppamento, ovvero i delimitatori token e la soglia di somiglianza. È inoltre disponibile un set di delimitatori predefiniti utilizzati per suddividere i dati in token. È tuttavia possibile aggiungere nuovi delimitatori per migliorare la suddivisione in token dei propri dati.  
  
 La soglia di somiglianza indica in quale misura la trasformazione identifica i duplicati. Le soglie di somiglianza possono essere impostate a livello di componente e di colonna. La soglia di somiglianza a livello di colonna è disponibile solo per le colonne che eseguono una corrispondenza fuzzy. L'intervallo di somiglianza è compreso tra 0 e 1. Più la soglia è vicina a 1 e più simili devono essere le righe e le colonne per essere qualificate come duplicati. Per impostare la soglia di somiglianza tra righe e colonne, è necessario impostare la proprietà MinSimilarity a livello di componente e di colonna. Per soddisfare la soglia di somiglianza specificata a livello di componente, è necessario che la somiglianza di tutte le righe in tutte le colonne sia maggiore o uguale alla soglia di somiglianza specificata a livello di componente.  
  
 La trasformazione Raggruppamento fuzzy calcola misure di somiglianza interne. Le righe il cui valore è meno simile al valore specificato in MinSimilarity non vengono raggruppate.  
  
 Per identificare la soglia di somiglianza più appropriata per i dati in uso, potrebbe essere necessario applicare la trasformazione Raggruppamento fuzzy più volte specificando soglie di somiglianza minime diverse. In fase di esecuzione, nelle colonne del punteggio dell'output della trasformazione è riportato il punteggio di somiglianza di ogni riga di un gruppo. In base a questi valori, è possibile stabilire qual è la soglia di somiglianza appropriata per i dati in uso. Se si desidera incrementare la somiglianza, impostare MinSimilarity su un valore maggiore dei valori contenuti nelle colonne del punteggio.  
  
 È possibile personalizzare il raggruppamento eseguito dalla trasformazione impostando le proprietà delle colonne nell'input della trasformazione Raggruppamento fuzzy. Ad esempio, la proprietà FuzzyComparisonFlags specifica la modalità di confronto dei dati stringa di una colonna, mentre la proprietà ExactFuzzy specifica se viene eseguita una corrispondenza fuzzy o una corrispondenza esatta.  
  
 La quantità di memoria usata dalla trasformazione Raggruppamento fuzzy può essere configurata impostando la proprietà personalizzata MaxMemoryUsage. È possibile specificare il numero di megabyte (MB) oppure il valore 0, che consente alla trasformazione di utilizzare una quantità dinamica di memoria, a seconda delle esigenze e della quantità di memoria fisica disponibile. La proprietà personalizzata MaxMemoryUsage può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
## <a name="row-comparison"></a>Confronto tra righe  
 Quando si configura la trasformazione Raggruppamento fuzzy, è possibile specificare l'algoritmo di confronto utilizzato per confrontare le righe dell'input della trasformazione. Se si imposta la proprietà Exhaustive su `true`, la trasformazione confronta ogni riga dell'input da tutte le altre righe nell'input. Questo algoritmo di confronto restituisce in genere risultati più precisi, ma la trasformazione viene eseguita più lentamente, a meno che l'input non includa un numero di righe ridotto. Per evitare problemi di prestazioni, è consigliabile impostare la proprietà Exhaustive su `true` solo durante lo sviluppo dei pacchetti.  
  
## <a name="temporary-tables-and-indexes"></a>Tabelle e indici temporanei  
 In fase di esecuzione, la trasformazione Raggruppamento fuzzy crea oggetti temporanei, quali tabelle e indici, potenzialmente di grandi dimensioni, nel database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui la trasformazione si connette. Le dimensioni delle tabelle e degli indici sono proporzionali al numero di righe dell'input della trasformazione Raggruppamento fuzzy e al numero di token creati dalla trasformazione.  
  
 La trasformazione esegue inoltre query nelle tabelle temporanee. È pertanto consigliabile connettere la trasformazione Raggruppamento fuzzy a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]non di produzione, soprattutto se lo spazio su disco disponibile nel server di produzione è ridotto.  
  
 Le prestazioni della trasformazione possono risultare migliori se le tabelle e gli indici utilizzati si trovano sullo stesso computer locale.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>Configurazione della trasformazione Raggruppamento fuzzy  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione Raggruppamento fuzzy &#40;scheda Gestione connessione&#41;](../../fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [Editor trasformazione Raggruppamento fuzzy &#40;scheda Colonne&#41;](../../fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [Editor trasformazione Raggruppamento fuzzy &#40;scheda Avanzate&#41;](../../fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni dettagliate sull'impostazione di questa attività, fare clic su uno degli argomenti seguenti:  
  
-   [Identificazione di righe di dati simili tramite la trasformazione Raggruppamento fuzzy](fuzzy-grouping-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca fuzzy](lookup-transformation.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  

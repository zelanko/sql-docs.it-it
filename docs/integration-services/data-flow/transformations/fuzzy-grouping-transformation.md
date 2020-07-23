---
title: Trasformazione Raggruppamento fuzzy | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fuzzygroupingtrans.f1
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4e00be6f692bd3e4bec21acec6c2de6359622b7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919335"
---
# <a name="fuzzy-grouping-transformation"></a>Raggruppamento fuzzy - trasformazione

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Raggruppamento fuzzy consente di eseguire attività di pulizia dei dati identificando le righe che con maggiore probabilità sono duplicate e selezionando una riga canonica di dati da utilizzare per la standardizzazione dei dati.  
  
> [!NOTE]  
>  Per informazioni dettagliate sulla trasformazione Raggruppamento fuzzy, inclusi i limiti di memoria e prestazioni, vedere il white paper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604).  
  
 La trasformazione Raggruppamento fuzzy richiede la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la creazione delle tabelle temporanee di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] necessarie all'algoritmo di trasformazione. La connessione deve corrispondere a un utente autorizzato che dispone dell'autorizzazione per la creazione di tabelle nel database.  
  
 Per configurare la trasformazione, è necessario selezionare le colonne di input da usare per l'identificazione di duplicati e il tipo di corrispondenza, fuzzy o esatta, per ogni colonna. Con una corrispondenza esatta vengono raggruppate solo le righe della colonna contenenti gli stessi valori. Questo tipo di corrispondenza può essere applicato alle colonne con qualsiasi tipo di dati di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , ad eccezione di DT_TEXT, DT_NTEXT e DT_IMAGE. Con una corrispondenza fuzzy vengono raggruppate le righe contenenti valori simili. Questo tipo di corrispondenza è basato su un punteggio di somiglianza specificato dall'utente. Nella corrispondenza fuzzy è possibile utilizzare solo colonne con tipo di dati DT_WSTR o DT_STR. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
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
  
 La quantità di memoria usata dalla trasformazione Raggruppamento fuzzy può essere configurata impostando la proprietà personalizzata MaxMemoryUsage. È possibile specificare il numero di megabyte (MB) oppure il valore 0, che consente alla trasformazione di utilizzare una quantità dinamica di memoria, a seconda delle esigenze e della quantità di memoria fisica disponibile. La proprietà personalizzata MaxMemoryUsage può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
## <a name="row-comparison"></a>Confronto tra righe  
 Quando si configura la trasformazione Raggruppamento fuzzy, è possibile specificare l'algoritmo di confronto utilizzato per confrontare le righe dell'input della trasformazione. Se si imposta la proprietà Exhaustive su **true**, ogni riga dell'input viene confrontata con le altre righe dell'input. Questo algoritmo di confronto restituisce in genere risultati più precisi, ma la trasformazione viene eseguita più lentamente, a meno che l'input non includa un numero di righe ridotto. Per evitare un impatto negativo sulle prestazioni, è consigliabile impostare la proprietà Exhaustive su **true** solo in fase di sviluppo dei pacchetti.  
  
## <a name="temporary-tables-and-indexes"></a>Tabelle e indici temporanei  
 In fase di esecuzione, la trasformazione Raggruppamento fuzzy crea oggetti temporanei, quali tabelle e indici, potenzialmente di grandi dimensioni, nel database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui la trasformazione si connette. Le dimensioni delle tabelle e degli indici sono proporzionali al numero di righe dell'input della trasformazione Raggruppamento fuzzy e al numero di token creati dalla trasformazione.  
  
 La trasformazione esegue inoltre query nelle tabelle temporanee. È pertanto consigliabile connettere la trasformazione Raggruppamento fuzzy a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]non di produzione, soprattutto se lo spazio su disco disponibile nel server di produzione è ridotto.  
  
 Le prestazioni della trasformazione possono risultare migliori se le tabelle e gli indici utilizzati si trovano sullo stesso computer locale.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>Configurazione della trasformazione Raggruppamento fuzzy  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni dettagliate sull'impostazione di questa attività, fare clic su uno degli argomenti seguenti:  
  
-   [Identificare righe di dati simili tramite la trasformazione Raggruppamento fuzzy](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Gestione connessione)
  Utilizzare la scheda **Gestione connessione** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** per selezionare una connessione esistente o crearne una nuova.  
  
> [!NOTE]  
>  Sul server specificato dalla connessione deve essere in esecuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La trasformazione Raggruppamento fuzzy crea in tempdb oggetti dati temporanei che possono avere le stesse dimensioni dell'intero input della trasformazione. Durante l'esecuzione della trasformazione vengono eseguite query del server su tali oggetti temporanei. Queste query possono influire sulle prestazioni generali del server.  
  
### <a name="options"></a>Opzioni  
 **Gestione connessione OLE DB**  
 Consente di selezionare una gestione connessione OLE DB esistente usando la casella di riepilogo o di creare una nuova connessione tramite il pulsante **Nuova** .  
  
 **Nuovo**  
 Consente di creare una nuova connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
## <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Colonne)
  Utilizzare la scheda **Colonne** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** per specificare le colonne utilizzate per raggruppare le righe contenenti valori duplicati  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne di input utilizzate per raggruppare le righe contenenti valori duplicati.  
  
 **Nome**  
 Consente di visualizzare i nomi delle colonne di input disponibili.  
  
 **Pass-through**  
 Consente di includere la colonna di input nell'output della trasformazione. Tutte le colonne utilizzate per il raggruppamento vengono copiate automaticamente nell'output. Selezionando questa colonna è possibile includere colonne aggiuntive.  
  
 **Colonna di input**  
 Consente di selezionare una delle colonne di input selezionate precedentemente nell'elenco **Colonne di input disponibili** .  
  
 **Alias di output**  
 Consente di immettere un nome descrittivo per la colonna di output corrispondente. Per impostazione predefinita, il nome della colonna di output corrisponde al nome della colonna di input.  
  
 **Alias di output gruppo**  
 Consente di immettere un nome descrittivo per la colonna che conterrà il valore canonico per i duplicati raggruppati. Il nome predefinito di questa colonna di output è il nome della colonna di input con l'aggiunta di _clean.  
  
 **Tipo di corrispondenza**  
 Consente di selezionare la corrispondenza fuzzy o esatta. Le righe vengono considerate duplicati se sono sufficientemente simili in tutte le colonne della corrispondenza fuzzy. Se inoltre si specifica la corrispondenza esatta su determinate colonne, vengono considerati possibili duplicati solo le righe contenenti valori identici nelle colonne della corrispondenza esatta. Se si sa pertanto che una determinata colonna non contiene errori o inconsistenze, è possibile specificare la corrispondenza esatta su tale colonna per aumentare la precisione della corrispondenza fuzzy su altre colonne.  
  
 **Somiglianza minima**  
 Consente di impostare la soglia di somiglianza minima a livello di join tramite un dispositivo di scorrimento. Più il valore è vicino a 1, maggiore deve essere la somiglianza tra il valore di ricerca e il valore di origine per essere considerata una corrispondenza. L'aumento della soglia può migliorare la velocità di confronto, poiché verrà considerato un numero minore di record candidati.  
  
 **Alias di output somiglianza**  
 Consente di specificare il nome di una nuova colonna di output contenente i punteggi di somiglianza per il join selezionato. Se non si specifica un valore, la colonna di output non viene creata.  
  
 **Numerali**  
 Consente di specificare l'importanza dei numerali iniziali e finali nel confronto dei dati della colonna. Ad esempio, se i numerali iniziali sono significativi, "2005 Vendite" non verrà raggruppato con "2004 Vendite".  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Nessuno**|I numerali iniziali e finali non sono significativi.|  
|**Iniziali**|Sono significativi solo i numerali iniziali.|  
|**Finali**|Sono significativi solo i numerali finali.|  
|**Iniziali e finali**|Sono significativi i numerali sia iniziali che finali.|  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](../../../integration-services/data-flow/comparing-string-data.md).  
  
## <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Avanzate)
  La scheda **Avanzate** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** consente di specificare le colonne di input e output, impostare le soglie di somiglianza e definire i delimitatori.  
  
> [!NOTE]  
>  Le proprietà **Exhaustive** e **MaxMemoryUsage** della trasformazione Raggruppamento fuzzy non sono disponibili nell' **Editor trasformazione Raggruppamento fuzzy**, tuttavia possono essere impostate utilizzando l' **Editor avanzato**. Per ulteriori informazioni su queste proprietà, vedere la sezione relativa alla trasformazione Raggruppamento fuzzy in [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opzioni  
 **Nome colonna chiave di input**  
 Consente di specificare il nome di una colonna di output contenente l'identificatore univoco per ogni riga di input. La colonna **_key_in** contiene un valore che identifica in modo univoco ogni riga.  
  
 **Nome colonna chiave di output**  
 Consente di specificare il nome di una colonna di output contenente l'identificatore univoco per la riga canonica di un gruppo di righe duplicate. La colonna **_key_out** corrisponde al valore **_key_in** della riga di dati canonica.  
  
 **Nome colonna punteggio somiglianza**  
 Consente di specificare un nome per la colonna contenente il punteggio di somiglianza. Il punteggio di somiglianza è un valore compreso tra 0 e 1 che indica la somiglianza della riga di input alla riga canonica. I punteggi più prossimi a 1 indicano una corrispondenza maggiore.  
  
 **Soglia di somiglianza**  
 Consente di impostare la soglia di somiglianza mediante il dispositivo di scorrimento. Le soglie vicine a 1 indicano che le righe devono avere una somiglianza maggiore per poter essere considerate duplicati. L'aumento della soglia può incrementare la velocità di ricerca della corrispondenza in quanto viene considerato un minor numero di record candidati.  
  
 **Delimitatori token**  
 La trasformazione genera un set predefinito di delimitatori per la suddivisione in token dei dati. È tuttavia possibile aggiungere o rimuovere i delimitatori in base alle esigenze modificando l'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca fuzzy](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

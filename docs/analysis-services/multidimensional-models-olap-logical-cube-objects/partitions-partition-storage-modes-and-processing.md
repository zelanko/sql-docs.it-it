---
title: Partizionare le modalità di archiviazione ed elaborazione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57c73e3ae9661058277a377b7d17b6a4af393ba0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640456"
---
# <a name="partitions---partition-storage-modes-and-processing"></a>Partizioni: elaborazione e modalità di archiviazione delle partizioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La modalità di archiviazione di una partizione influisce sulle prestazioni di esecuzione delle query e di elaborazione e su requisiti e percorsi di archiviazione della partizione e del relativo cubo e gruppo di misure padre. La scelta della modalità di archiviazione influisce inoltre sulle opzioni di elaborazione.  
  
 Una partizione può utilizzare una delle tre modalità di archiviazione di base seguenti:  
  
-   OLAP multidimensionale (MOLAP)  
  
-   OLAP relazionale (ROLAP)  
  
-   OLAP ibrido (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta tutte e tre le modalità di archiviazione di base. Supporta inoltre la memorizzazione nella cache attiva, che consente di combinare le caratteristiche dell'archiviazione ROLAP e MOLAP ai fini dell'attualità dei dati e delle prestazioni di esecuzione delle query. Per altre informazioni, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="molap"></a>MOLAP  
 La modalità di archiviazione MOLAP determina l'archiviazione delle aggregazioni della partizione e di una copia dei dati di origine in una struttura multidimensionale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante l'elaborazione della partizione. Questa struttura MOLAP è ottimizzata in modo da garantire le massime prestazioni di esecuzione delle query. L'archiviazione può essere eseguita in un percorso sul computer in cui la partizione è definita o su un altro computer che esegue [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Poiché una copia dei dati di origine risiede nella struttura multidimensionale, le query possono essere risolte senza accedere ai dati di origine della partizione. I tempi di risposta alle query possono essere ridotti significativamente utilizzando le aggregazioni. I dati nella struttura MOLAP della partizione sono aggiornati all'elaborazione più recente della partizione.  
  
 Poiché i dati di origine vengono modificati, gli oggetti nell'archivio MOLAP devono essere elaborati periodicamente in modo da incorporare tali modifiche e renderle disponibili agli utenti. L'elaborazione determina l'aggiornamento completo o incrementale dei dati nella struttura MOLAP. L'intervallo di tempo tra un'elaborazione e quella successiva crea un periodo di latenza durante il quale i dati negli oggetti OLAP potrebbero non corrispondere ai dati di origine. È possibile eseguire l'aggiornamento completo o incrementale degli oggetti nell'archivio MOLAP senza porre la partizione o il cubo in modalità offline. In alcune situazioni, tuttavia, può essere necessario porre un cubo in modalità offline per elaborare determinate modifiche strutturali agli oggetti OLAP. Il tempo di inattività necessario per aggiornare l'archivio MOLAP può essere ridotto al minimo aggiornando ed elaborando i cubi su un server dell'area di gestione temporanea e utilizzando la sincronizzazione di database per copiare gli oggetti elaborati nel server di produzione. È inoltre possibile utilizzare la memorizzazione nella cache attiva per ridurre al minimo la latenza e ottimizzare la disponibilità mantenendo la maggior parte dei vantaggi offerti in termini di prestazioni dall'archiviazione MOLAP. Per altre informazioni, vedere [memorizzazione nella cache &#40;partizioni&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), [sincronizzare i database di Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md), e [l'elaborazione di un modello multidimensionale &#40; Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 La modalità di archiviazione ROLAP determina l'archiviazione delle aggregazioni della partizione in viste indicizzate del database relazionale specificato nell'origine dei dati della partizione. A differenza della modalità di archiviazione MOLAP, la modalità ROLAP non prevede l'archiviazione di una copia dei dati di origine nelle cartelle dei dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Quando non è possibile derivare risultati dalla cache delle query, per rispondere alle query viene invece eseguito l'accesso alle viste indicizzate dell'origine dei dati. I tempi di risposta alle query sono in genere più lenti con la modalità di archiviazione ROLAP rispetto alle modalità di archiviazione MOLAP e HOLAP, così come sono in genere più lenti i tempi di elaborazione con ROLAP. La modalità ROLAP consente inoltre agli utenti di visualizzare i dati in tempo reale e di risparmiare spazio di archiviazione quando si utilizzano set di dati di grandi dimensioni su cui vengono raramente eseguite query, ad esempio dati esclusivamente cronologici.  
  
> [!NOTE]  
>  Quando si utilizza ROLAP, in caso di combinazione di join con una clausola GROUP BY è possibile che [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisca informazioni non corrette relativamente al membro sconosciuto. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina errori di integrità relazionali anziché restituire il valore del membro sconosciuto.  
  
 Se una partizione utilizza la modalità di archiviazione ROLAP e i dati di origine sono archiviati in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cerca di creare viste indicizzate per contenere le aggregazioni della partizione. Se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non è in grado di creare viste indicizzate, non vengono create tabelle di aggregazione. Sebbene i requisiti della sessione per la creazione di viste indicizzate in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengano gestiti da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], è necessario che la partizione ROLAP e le tabelle nel relativo schema soddisfino le condizioni seguenti in modo che [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sia in grado di creare viste indicizzate per le aggregazioni:  
  
-   La partizione non può contenere misure che utilizzano le **Min** oppure **Max** funzioni di aggregazione.  
  
-   Ogni tabella nello schema della partizione ROLAP deve essere utilizzata una sola volta. Lo schema non può ad esempio contenere le stringhe [dbo].[address] AS "Customer Address" e [dbo].[address] AS "SalesRep Address".  
  
-   Ogni tabella deve essere effettivamente una tabella e non una vista.  
  
-   Tutti i nomi di tabella presenti nello schema della partizione devono essere qualificati con il nome del proprietario, ad esempio [dbo].[customer].  
  
-   Tutte le tabelle nello schema della partizione devono avere lo stesso proprietario. Non è possibile, ad esempio, avere una clausola FROM che fa riferimento alle tabelle [tk].[customer], [john].[store] e [dave].[sales_fact_2004].  
  
-   Le colonne di origine delle misure della partizione non devono ammettere valori Null.  
  
-   Tutte le tabelle utilizzate nella vista devono essere state create attivando le opzioni seguenti:  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   Le dimensioni totali di una chiave dell'indice, in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], non possono essere maggiori di 900 byte. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Questa condizione basata su colonne chiave a lunghezza fissa quando viene elaborata l'istruzione CREATE INDEX verrà verificata. Tuttavia, se sono presenti colonne a lunghezza variabile nella chiave di indice, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verrà inoltre verificata questa condizione per tutti gli aggiornamenti di tabelle di base. Poiché aggregazioni diverse utilizzano definizioni di viste diverse, l'elaborazione ROLAP con viste indicizzate avrà esito positivo o negativo in base alla progettazione delle aggregazioni.  
  
-   Nella sessione di creazione della vista indicizzata deve avere le seguenti opzioni impostate su ON: ARITHABORT, CONCAT_NULL_YEILDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING e ANSI_WARNING. Questa impostazione può essere eseguita in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Nella sessione di creazione della vista indicizzata deve avere la seguente opzione impostata su OFF: NUMERIC_ROUNDABORT. Questa impostazione può essere eseguita in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="holap"></a>HOLAP  
 La modalità di archiviazione HOLAP combina attributi sia di MOLAP che di ROLAP. Come MOLAP, HOLAP determina le aggregazioni della partizione che deve essere archiviato in una struttura multidimensionale in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza. HOLAP non prevede l'archiviazione di una copia dei dati di origine. Per le query che accedono esclusivamente ai dati di riepilogo nelle aggregazioni di una partizione, la modalità HOLAP equivale a MOLAP. Le query che accedono ai dati di origine, ad esempio, se si desidera eseguire il drill down una cella del cubo atomica per cui non esiste alcuna aggregazione dei dati, deve recuperare dati dal database relazionale e non sarà stessa velocità con cui verrebbero usati se i dati di origine sono stati archiviati nel structur MOLAP e. Con la modalità di archiviazione HOLAP, gli utenti riscontrano in genere differenze significative nei tempi di esecuzione delle query a seconda che la query possa essere risolta dalla cache o dalle aggregazioni oppure dai dati di origine.  
  
 Le partizioni archiviate come HOLAP presentano dimensioni inferiori rispetto alle partizioni MOLAP equivalenti, poiché non contengono i dati di origine, e garantiscono tempi di risposta più rapidi rispetto alle partizioni ROLAP per le query in cui sono coinvolti dati di riepilogo. La modalità di archiviazione HOLAP è in genere appropriata per partizioni di cubi che necessitano di tempi di risposta alle query rapidi per riepiloghi basati su un'ingente quantità di dati di origine. Nei casi in cui gli utenti generano query che devono accedere ai dati a livello foglia, ad esempio per il calcolo di mediane, è in genere preferibile la modalità MOLAP.  
  
## <a name="see-also"></a>Vedere anche  
 [La memorizzazione nella cache &#40;partizioni&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Sincronizzare database di Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  

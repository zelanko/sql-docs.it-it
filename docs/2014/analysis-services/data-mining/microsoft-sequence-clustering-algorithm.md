---
title: Algoritmo Microsoft Sequence Clustering | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc90c76792ae6eaaa21ba3e32bea66e4942c354f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733697"
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo Microsoft Sequence Clustering
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è un algoritmo di analisi delle sequenze fornito da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile utilizzare questo algoritmo per esplorare i dati contenenti eventi che possono essere collegati dai percorsi seguenti, oppure *sequenze*. L'algoritmo consente di individuare le sequenze più comuni raggruppando quelle identiche o eseguendone il clustering. Di seguito sono riportati alcuni esempi di dati contenenti sequenze che potrebbero essere utilizzate per il data mining per fornire informazioni su problemi comuni o scenari aziendali:  
  
-   Percorsi creati dagli utenti durante l'utilizzo di un sito Web.  
  
-   Log in cui vengono elencati eventi che precedono un incidente, ad esempio errori del disco rigido o deadlock del server.  
  
-   Record di transazioni in cui viene descritto l'ordine in base al quale un cliente aggiunge articoli al carrello acquisti in un punto vendita online.  
  
-   Record in cui si seguono le interazioni del cliente (o paziente) nel tempo, per stimare annullamenti del servizio o altri risultati insufficienti.  
  
 Questo algoritmo è simile per molti versi all'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. ma, anziché rilevare cluster di case contenenti attributi simili, l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering individua i cluster di case contenenti percorsi simili in una sequenza.  
  
## <a name="example"></a>Esempio  
 Il [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] sito Web raccoglie informazioni su quali pagine del sito dagli utenti e sull'ordine in cui le pagine vengono visitate. Poiché l'azienda accetta solo ordini online, i clienti devono accedere al sito. In questo modo, l'azienda ottiene informazioni di esplorazione per il profilo di ogni cliente. Tramite l'applicazione dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering a tali dati, l'azienda può individuare gruppi o cluster di clienti con schemi di acquisto o sequenze di selezioni simili. In seguito, l'azienda può utilizzare tali cluster per analizzare gli spostamenti degli utenti nel sito Web, identificare le pagine più strettamente correlate alla vendita di un prodotto specifico ed eseguire la stima delle pagine che con maggiore probabilità verranno visitate successivamente.  
  
## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è un algoritmo ibrido che combina tecniche di clustering e l'analisi delle catene di Markov per identificare i cluster e le relative sequenze. Una delle caratteristiche distintive dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è l'utilizzo dei dati in sequenza. Questi dati rappresentano in genere una serie di eventi o transizioni tra stati in un set di dati, ad esempio una serie di acquisti di prodotti o di clic sul Web per un determinato utente. Per determinare le sequenze migliori da usare come input per il clustering, l'algoritmo esamina tutte le probabilità di transizione e misura le differenze, o distanze, tra tutte le sequenze possibili del set di dati. Dopo la creazione dell'elenco di sequenze candidate, l'algoritmo utilizza le informazioni sulla sequenza come input per il metodo EM di clustering.  
  
 Per una descrizione dettagliata dell'implementazione, vedere [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-sequence-clustering-models"></a>Dati necessari per i modelli Sequence Clustering  
 Quando si preparano dati da utilizzare nel training di un modello Sequence Clustering, è importante comprendere i requisiti per l'algoritmo specifico, tra cui la quantità di dati necessari e la modalità di utilizzo dei dati.  
  
 I requisiti per un modello Sequence Clustering sono i seguenti:  
  
-   **Una colonna a chiave singola** Un modello Sequence Clustering richiede una chiave che identifica i record.  
  
-   **Una colonna della sequenza** Per i dati in sequenza, il modello deve disporre di una tabella annidata contenente una colonna di ID sequenza. L'ID sequenza può essere qualsiasi tipo di dato ordinabile. Ad esempio, è possibile utilizzare un identificatore di pagina Web, un numero intero o una stringa di testo, purché la colonna identifichi gli eventi in una sequenza. Per ogni sequenza è consentito un unico identificatore di sequenza e per ogni modello è consentito un unico tipo di sequenza.  
  
-   **Attributi fuori sequenza facoltativi** L'algoritmo supporta l'aggiunta di altri attributi non correlati alle sequenze. Questi attributi possono includere le colonne nidificate.  
  
 Nell'esempio del sito Web di [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] riportato in precedenza, un modello Sequence Clustering potrebbe includere informazioni sull'ordine come tabella del case, dati demografici sul cliente specifico per ogni ordine come attributi fuori sequenza e una tabella nidificata contenente la sequenza in cui il cliente ha esplorato il sito o ha inserito gli articoli nel carrello acquisti come informazioni sulla sequenza.  
  
 Per informazioni più dettagliate sui tipi di contenuto e i tipi di dati supportati per i modelli Sequence Clustering, vedere la sezione Requisiti di [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-sequence-clustering-model"></a>Visualizzazione di un modello Sequence Clustering  
 Il modello di data mining creato da questo algoritmo contiene le descrizioni delle sequenze più comuni incluse nei dati. Per esplorare il modello, è possibile usare il **Visualizzatore Microsoft Sequence Clustering**. Quando si visualizza un modello Sequence Clustering, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono visualizzati i cluster che contengono più transizioni. È inoltre possibile visualizzare statistiche pertinenti. Per altre informazioni, vedere [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Per maggiori dettagli, è possibile esplorare il modello in [Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). Il contenuto archiviato per il modello include la distribuzione per tutti i valori in ogni nodo, la probabilità di ogni cluster e altre informazioni sulle transizioni. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data mining&#41;](mining-model-content-for-sequence-clustering-models.md).  
  
## <a name="creating-predictions"></a>Creazione di stime  
 Dopo il training del modello, i risultati vengono archiviati come set di modelli. È possibile utilizzare le descrizioni delle sequenze più comuni nei dati per la stima del probabile passaggio successivo di una nuova sequenza. Poiché tuttavia l'algoritmo include altre colonne, è possibile utilizzare il modello risultante per individuare le relazioni tra i dati in sequenza e gli input non sequenziali. Ad esempio, se si aggiungono dati demografici al modello, è possibile eseguire stime per gruppi specifici di clienti. È possibile personalizzare le query di stima per restituire un numero variabile di stime o statistiche descrittive.  
  
 Per informazioni sulla creazione di query in base a un modello di data mining, vedere [Query di data mining](data-mining-queries.md). Per alcuni esempi su come usare le query con un modello Sequence Clustering, vedere [Esempi di query sul modello di cluster di sequenza](clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Note  
  
-   Non supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.  
  
-   Supporta il drill-through.  
  
-   Supporta l'utilizzo di modelli di data mining OLAP e la creazione di dimensioni di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Esempi di query sul modello di cluster di sequenza](clustering-model-query-examples.md)   
 [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  

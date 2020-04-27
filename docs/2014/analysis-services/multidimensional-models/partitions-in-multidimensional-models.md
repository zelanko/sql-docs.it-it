---
title: Partizioni nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00d17af3ce46ee5b20a730e536321140bb69f4ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073325"
---
# <a name="partitions-in-multidimensional-models"></a>Partizioni nei modelli multidimensionali
  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]una *partizione* consente l'archiviazione fisica delle tabelle dei fatti in un gruppo di misure. Per ogni gruppo di misure viene automaticamente creata una singola partizione, ma è frequente creare partizioni aggiuntive per l'ulteriore segmentazione dei dati, con il conseguente miglioramento dell'elaborazione e delle prestazioni delle query.  
  
 L'elaborazione diventa più efficiente poiché le partizioni possono essere elaborate in modo indipendente e in parallelo su uno o più server. Le query vengono eseguite più velocemente poiché ogni partizione può essere configurata con le modalità di archiviazione e le ottimizzazioni di aggregazione che assicurano tempi di risposta più brevi. Ad esempio, l'archiviazione MOLAP per le partizioni che contengono dati più recenti è in genere più veloce dell'archiviazione ROLAP. In modo analogo, se si effettua il partizionamento in base alla data, le partizioni che contengono dati più recenti possono includere più ottimizzazioni delle partizioni contenenti dati più vecchi a cui si accede con minore frequenza. Tenere presente che la scelta di impostazioni di archiviazione e aggregazione diverse in base alla partizione influirà negativamente sulle operazioni di unione successive. Valutare attentamente se l'unione è un componente fondamentale della strategia di gestione delle partizioni prima di ottimizzare le singole partizioni.  
  
> [!NOTE]  
>  Il supporto per più partizioni è disponibile nella Business Intelligence Edition e nella Enterprise Edition. La Standard Edition non supporta più partizioni. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>Importanti considerazioni per la progettazione di una strategia di partizionamento  
 L'integrità dei dati di un cubo si basa sui dati distribuiti tra le partizioni del cubo in modo che nessun dato venga duplicato tra le partizioni. Quando i dati vengono riepilogati nelle partizioni, tutti gli elementi di dati presenti in più partizioni saranno riepilogati come se fossero elementi di dati diversi. Tale operazione può comportare la visualizzazione di riepiloghi e dati errati all'utente finale. Ad esempio, se una transazione di vendita per il prodotto X viene duplicata nelle tabelle dei fatti per due partizioni, nei riepiloghi delle vendite del prodotto X può essere inclusa una contabilità doppia della transazione duplicata.  
  
 Le partizioni possono essere unite; tale caratteristica può essere utilizzata nella strategia complessiva di archiviazione e aggiornamento dei dati. Le partizioni possono essere unite solo se dispongono della stessa modalità di archiviazione e della medesima progettazione aggregazioni. Per creare partizioni che possono essere unite in un secondo momento, è possibile copiare la progettazione aggregazioni di un'altra partizione quando si creano partizioni. Una partizione può anche essere modificata dopo la relativa creazione per copiare la progettazione aggregazioni di un'altra partizione. L'unione di partizioni deve essere eseguita attentamente per evitare la duplicazione di dati nella partizione risultante, infatti tale operazione può comportare dati del cubo imprecisi.  
  
## <a name="local-partitions"></a>Partizioni locali  
 Le partizioni locali sono partizioni definite, elaborate e archiviate in un solo server. Se un cubo include gruppi di dimensioni estesi, potrebbe risultare utile partizionarli in modo che l'elaborazione venga eseguita in parallelo in tutte le partizioni. L'elaborazione parallela consente tempi di esecuzione più rapidi. Dato che un processo di elaborazione delle partizioni può essere avviato anche mentre ne è in corso un altro, i due processi possono essere eseguiti in parallelo. Per altre informazioni, vedere [Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="remote-partitions"></a>Partizioni remote  
 Le partizioni remote sono partizioni definite in un solo server, ma elaborate e archiviate in un altro server. Se si desidera distribuire l'archiviazione di dati e metadati tra più server, utilizzare le partizioni remote. In genere, nel passaggio dallo sviluppo alla produzione, le dimensioni dei dati analizzati aumentano notevolmente. Quando esistono gruppi di dati di grandi dimensioni, è possibile distribuirli su più computer, non tanto perché i dati non possono essere contenuti tutti in uno stesso computer, quanto per consentirne l'elaborazione in parallelo. Per altre informazioni, vedere [Creare e gestire una partizione remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md).  
  
## <a name="aggregations"></a>Aggregations  
 Le aggregazioni sono riepiloghi precalcolati dei dati del cubo che consentono a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di fornire rapidamente le risposte alle query. È possibile determinare il numero di aggregazioni create per un gruppo di misure impostando limiti sull'archiviazione e sul miglioramento delle prestazioni oppure arrestando arbitrariamente il processo di compilazione delle aggregazioni dopo un certo periodo di esecuzione. Un numero superiore di aggregazioni non costituisce necessariamente un vantaggio. Ogni nuova aggregazione ha un costo, sia in termini di spazio su disco che di tempo di elaborazione. Si consiglia di creare aggregazioni fino a ottenere un miglioramento delle prestazioni pari al 30% e quindi di aumentarne il numero solo se richiesto da attività di test o dall'esperienza. Per altre informazioni, vedere [Progettazione di aggregazioni &#40;Analysis Services - Multidimensionale&#41;](designing-aggregations-analysis-services-multidimensional.md).  
  
## <a name="partition-merging-and-editing"></a>Unione e modifica di partizioni  
 Se due partizioni sono basate sulla stessa progettazione di aggregazione, è possibile unirle. Se una dimensione delle scorte, ad esempio, è partizionata in base al mese, alla fine di ogni mese è possibile unire la partizione mensile con la partizione da inizio anno esistente. In tal modo la partizione mensile corrente può essere elaborata e analizzata in modo rapido, mentre gli altri mesi dell'anno devono essere rielaborati solo in fase di unione. Tale rielaborazione richiede tempi più lunghi e può essere eseguita con minor frequenza. Per altre informazioni sull'unione di partizioni, vedere [Unire partizioni in Analysis Services &#40;SSAS - Multidimensionale&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md). Per modificare le partizioni del cubo tramite la scheda **partizioni** in Progettazione cubi, vedere [modificare o eliminare partizioni &#40;Analysis Services-&#41;multidimensionali ](edit-or-delete-partitions-analyisis-services-multidimensional.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)|Sono contenute informazioni su come partizionare i dati utilizzando filtri o tabelle dei fatti diverse senza duplicare i dati.|  
|[Impostare l'archiviazione delle partizioni &#40;Analysis Services - Multidimensionale&#41;](set-partition-storage-analysis-services-multidimensional.md)|Viene descritto come configurare l'archiviazione per le partizioni.|  
|[Modificare o eliminare partizioni &#40;Analysis Services-multidimensionale&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|Viene descritto come visualizzare e modificare le partizioni.|  
|[Unire partizioni in Analysis Services &#40;SSAS - Multidimensionale&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)|Sono contenute informazioni su come unire le partizioni in cui sono presenti tabelle dei fatti o sezioni dei dati diverse senza duplicare i dati.|  
|[Impostare tabelle writeback delle partizioni](set-partition-writeback.md)|Vengono fornite istruzioni su come abilitare una partizione per la scrittura.|  
|[Creare e gestire una partizione remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)|Viene descritto come creare e gestire una partizione remota.|  
  
  

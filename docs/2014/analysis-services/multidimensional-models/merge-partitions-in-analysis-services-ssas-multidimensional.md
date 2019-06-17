---
title: Unire partizioni in Analysis Services (SSAS - multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], merging
- merging partitions [Analysis Services]
ms.assetid: b3857b9b-de43-4911-989d-d14da0196f89
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 365f89286a59057efa39b503eedaedebb875c039
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073645"
---
# <a name="merge-partitions-in-analysis-services-ssas---multidimensional"></a>Unire partizioni in Analysis Services (SSAS - Multidimensionale)
  È possibile unire partizioni in un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente per consolidare i dati delle tabelle dei fatti da più partizioni dello stesso gruppo di misure.  
  
 [Scenari comuni](#bkmk_Scenario)  
  
 [Requisiti](#bkmk_prereq)  
  
 [Aggiornare l'origine partizione in seguito all'unione delle partizioni](#bkmk_Where)  
  
 [Considerazioni speciali per le partizioni segmentate dalla tabella dei fatti o dalla query denominata](#bkmk_fact)  
  
 [Come unire partizioni mediante SSMS](#bkmk_partitionSSMS)  
  
 [Come unire partizioni mediante XMLA](#bkmk_partitionsXMLA)  
  
##  <a name="bkmk_Scenario"></a> Scenari comuni  
 La configurazione più comune adottata per l'utilizzo di partizioni consiste nel separare i dati in base a una dimensione temporale. La granularità del tempo associata a ciascuna partizione dipende dalle esigenze commerciali relative al progetto. È ad esempio possibile eseguire la segmentazione per anni, con l'anno più recente diviso per mesi, oltre a una partizione separata per il mese in corso. La partizione mensile attiva assume regolarmente nuovi dati.  
  
 Quando il mese corrente è completato, la partizione corrispondente viene unita alla partizione dei mesi dell'anno in corso e il processo continua. Alla fine dell'anno, sarà stata creata una nuova partizione dell'anno completa.  
  
 Come illustrato in questo scenario, l'unione di partizioni può diventare un'attività di routine eseguita regolarmente, fornendo un approccio progressivo per il consolidamento e l'organizzazione di dati cronologici.  
  
##  <a name="bkmk_prereq"></a> Requisiti  
 Le partizioni possono essere unite solo se soddisfano tutti i criteri seguenti:  
  
-   Dispongono dello stesso gruppo di misure.  
  
-   Hanno la stessa struttura.  
  
-   Sono in uno stato elaborato.  
  
-   Supportano le stesse modalità di archiviazione.  
  
-   Includono progettazioni di aggregazione identiche.  
  
-   Condividono lo stesso livello di compatibilità (si applica solo a gruppi di misure Distinct Count partizionati) dell'archivio di stringhe.  
  
 Se la partizione di destinazione è vuota (ovvero include una progettazione di aggregazione, ma non aggregazioni), l'unione eliminerà le aggregazioni per le partizioni di origine. È necessario eseguire Elaborazione indice, Elaborazione completa o Elaborazione predefinita nella partizione per creare le aggregazioni.  
  
 Le partizioni remote possono essere unite solo ad altre partizioni remote definite con la stessa istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Se si utilizza una combinazione di partizioni remote e locali, un approccio alternativo consiste nel creare nuove partizioni contenenti dati combinati, eliminando quelle non più in uso.  
  
 Per creare una partizione che possa in seguito essere unita, in Creazione guidata partizione è possibile scegliere di copiare la progettazione delle aggregazioni da un'altra partizione del cubo. In tal modo le due partizioni avranno la stessa progettazione di aggregazione. Durante l'operazione di unione le aggregazioni della partizione di origine vengono unite alle aggregazioni della partizione di destinazione.  
  
##  <a name="bkmk_Where"></a> Aggiornare l'origine partizione in seguito all'unione delle partizioni  
 Le partizioni vengono segmentate per query, ad esempio la clausola WHERE di una query SQL utilizzata per elaborare i dati, o per una tabella o query denominata che fornisce dati alla partizione. La proprietà `Source` nella partizione indica se la partizione è associata a una query o una tabella.  
  
 Quando si uniscono partizioni, il contenuto delle partizioni viene consolidato, ma la proprietà `Source` non viene aggiornata per riflettere l'ambito aggiuntivo della partizione. In questo caso, se successivamente si rielaborerà una partizione che mantiene l'elemento `Source`originale, si otterranno dati errati dalla partizione. La partizione aggregherà dati in modo errato al livello padre. Nell'esempio seguente viene illustrato questo comportamento.  
  
 **Problema**  
  
 Si supponga di disporre di un cubo contenente informazioni su tre bibite analcoliche. Il cubo include tre partizioni che utilizzano la stessa tabella dei fatti. Queste partizioni sono segmentate per prodotto. La partizione 1 contiene dati relativi a [ColaFull], la partizione 2 dati relativi a [ColaDecaf] e la partizione 3 dati relativi a [ColaDiet]. Se la partizione 3 viene unita alla partizione 2, i dati della partizione risultante (la partizione 2) saranno corretti e i dati del cubo saranno accurati. Tuttavia, quando viene elaborata la partizione 2, il relativo contenuto potrebbe essere determinato dal padre dei membri al livello del prodotto. Questo elemento padre [SoftDrinks] include [ColaFull], il prodotto incluso in Partition 1. L'elaborazione di Partition 2 consente di caricare i dati per tutte le bibite, incluso il prodotto [ColaFull], nella partizione. Il cubo conterrà pertanto dati duplicati per [ColaFull] e restituirà dati non corretti agli utenti finali.  
  
 **Soluzione**  
  
 La soluzione consiste nell'aggiornare la proprietà `Source`, regolando la clausola WHERE o la query denominata oppure unendo manualmente i dati dalle tabelle dei fatti sottostanti, per garantire che l'elaborazione successiva sia accurata per via dell'ambito esteso della partizione.  
  
 In questo esempio, dopo aver unito la partizione 3 alla partizione 2, è possibile applicare il filtro ("Product" = 'ColaDecaf' OR "Product" = 'ColaDiet') nella partizione 2 risultante per specificare che devono essere estratti dalla tabella dei fatti solo i dati relativi a [ColaDecaf] e a [ColaDiet] e che devono essere esclusi i dati relativi a [ColaFull]. In alternativa, è possibile specificare i filtri per la partizione 2 e la partizione 3 in fase di creazione, in modo che vengano combinati durante il processo di unione. In entrambi i casi, il cubo non conterrà dati duplicati dopo l'elaborazione della partizione.  
  
 **Conclusione**  
  
 Dopo aver unito le partizioni, controllare sempre l'elemento `Source` per verificare che per i dati uniti il filtro sia corretto. Se si inizia con una partizione che include dati cronologici per Q1, Q2 e Q3 e si unisce quindi Q4, è necessario modificare il filtro affinché includa Q4. In caso contrario, la successiva elaborazione della partizione genererà risultati errati. Non sarà corretta per Q4.  
  
##  <a name="bkmk_fact"></a> Considerazioni speciali per le partizioni segmentate dalla tabella dei fatti o dalla query denominata  
 Oltre alle query, le partizioni possono essere segmentate anche per tabella o query denominata. Se la partizione di origine e la partizione di destinazione utilizzano la stessa tabella dei fatti in un'origine dati o in una vista origine dati, la proprietà `Source` sarà valida in seguito all'unione delle partizioni. Specifica i dati della tabella dei fatti appropriati alla partizione risultante. Poiché i fatti necessari per la partizione risultante sono contenuti nella tabella dei fatti, non è necessaria alcuna modifica alla proprietà `Source`.  
  
 Le partizioni che utilizzano dati di più tabelle dei fatti o più query denominate richiedono ulteriori attività. In questo caso è necessario unire in modo manuale i dati della tabella dei fatti della partizione di origine alla tabella dei fatti della partizione di destinazione.  
  
 In alternativa, è possibile sostituire l'origine della partizione unita con una query denominata che restituisce il contenuto di due tabelle dei fatti distinte. Se non si esegue questo passaggio manuale, le informazioni contenute nella partizione non saranno complete.  
  
 Per lo stesso motivo, anche le partizioni che ottengono dati segmentati da query denominate richiedono aggiornamenti. La partizione combinata deve disporre ora di una query denominata che restituisce il set di risultati combinati precedentemente ottenuto dalle query denominate distinte.  
  
## <a name="partition-storage-considerations-molap"></a>Considerazioni sull'archiviazione di partizione: MOLAP  
 Quando si uniscono partizioni MOLAP, vengono uniti anche i fatti archiviati nelle strutture multidimensionali delle partizioni. Internamente viene pertanto creata una partizione consistente e completa. I fatti archiviati nelle partizioni MOLAP, tuttavia, sono copie dei fatti presenti nella tabella dei fatti. Durante la successiva elaborazione della partizione, i fatti della struttura multidimensionale vengono eliminati (solo per l'elaborazione completa e di aggiornamento) e i dati vengono copiati dalla tabella dei fatti in base all'origine dei dati e al filtro per la partizione. Se la partizione di origine utilizza una tabella dei fatti diversa da quella della partizione di destinazione, le tabelle dei fatti delle due partizioni devono essere unite manualmente per garantire la disponibilità di un set di dati completo durante l'elaborazione della partizione risultante. Ciò vale anche se le due partizioni sono basate su query denominate diverse.  
  
> [!IMPORTANT]  
>  Una partizione MOLAP unita contenente una tabella dei fatti incompleta include una copia unita internamente dei dati delle tabelle dei fatti e funziona in modo corretto fino a quando non viene elaborata.  
  
## <a name="partition-storage-considerations-holap-and-rolap-partitions"></a>Considerazioni sull'archiviazione di partizione: Partizioni ROLAP e HOLAP  
 Quando si uniscono partizioni HOLAP o ROLAP a cui sono associate tabelle dei fatti diverse, le tabelle dei fatti non vengono unite automaticamente. Se queste tabelle non vengono unite in modo manuale, nella partizione risultante sarà disponibile solo la tabella dei fatti della partizione di destinazione. I fatti associati alla partizione di origine non sono disponibili per il drill-down nella partizione risultante e in fase di elaborazione della partizione le aggregazioni non riepilogheranno i dati della tabella non disponibile.  
  
> [!IMPORTANT]  
>  Una partizione HOLAP o ROLAP unita contenente una tabella dei fatti incompleta include aggregazioni corrette, ma fatti incompleti. Le query che fanno riferimento a fatti mancanti restituiscono dati non corretti. In fase di elaborazione della partizione, le aggregazioni vengono calcolate solo in base ai fatti disponibili.  
  
 L'assenza di fatti non disponibili potrebbe passare inosservata, a meno che un utente non tenti di eseguire il drill-down di un fatto della tabella non disponibile o esegua una query che richiede un fatto della tabella non disponibile. Poiché le aggregazioni vengono combinate durante il processo di unione, le query i cui risultati si basano esclusivamente su aggregazioni restituiscono dati corretti. Gli altri tipi di query potrebbero invece restituire dati non corretti. Anche dopo l'elaborazione della partizione risultante, la mancanza dei dati della tabella dei fatti non disponibile potrebbe passare inosservata, soprattutto se i dati mancanti rappresentano solo una piccola parte dei dati combinati.  
  
 Le tabelle dei fatti possono essere unite prima o dopo l'unione delle partizioni. Le aggregazioni, tuttavia, rappresentano i fatti sottostanti in modo accurato solo dopo il completamento di entrambe le operazioni. È consigliabile unire le partizioni HOLAP o ROLAP che accedono a tabelle dei fatti diverse quando gli utenti non sono connessi al cubo contenente tali partizioni.  
  
##  <a name="bkmk_partitionSSMS"></a> Come unire partizioni mediante SSMS  
  
> [!IMPORTANT]  
>  Prima di unire le partizioni, copiare le informazioni relative al filtro dei dati (spesso si tratta della clausola WHERE per filtri basati su query SQL). In seguito, al termine dell'unione, sarà opportuno aggiornare la proprietà di origine della partizione che contiene i dati delle tabelle dei fatti accumulati.  
  
1.  In Esplora oggetti espandere il nodo **Gruppi di misure** del cubo contenente le partizioni che si desidera unire, quindi espandere **Partizioni**e fare clic con il pulsante destro del mouse sulla partizione di destinazione dell'operazione di unione. Se ad esempio si spostano dati delle tabelle dei fatti trimestrali in una partizione in cui sono archiviati dati delle tabelle dei fatti annuali, selezionare la partizione che contiene i dati delle tabelle dei fatti annuali.  
  
2.  Fare clic su **Unisci partizioni** per aprire il **Unisci partizione \<nome partizione >** nella finestra di dialogo.  
  
3.  In **Partizioni di origine**selezionare la casella di controllo accanto a ogni partizione di origine che si desidera unire alla partizione di destinazione, quindi fare clic su **OK**.  
  
    > [!NOTE]  
    >  Le partizioni di origine verranno immediatamente eliminate in seguito all'unione con le partizioni di destinazione. Aggiornare la cartella Partizioni per aggiornarne i contenuto in seguito all'unione.  
  
4.  Fare clic con il pulsante destro del mouse sulla partizione che contiene i dati accumulati e scegliere **Proprietà**.  
  
5.  Aprire il `Source` proprietà e modificare la clausola WHERE in modo che includa i dati della partizione appena uniti. Si tenga presente che il `Source` proprietà non viene aggiornata automaticamente. Se esegue la rielaborazione senza prima aggiornare il `Source`, potrebbe non ottenere tutti i dati previsti.  
  
##  <a name="bkmk_partitionsXMLA"></a> Come unire partizioni mediante XMLA  
 Per informazioni, vedere l'argomento [Unione di partizioni &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione di oggetti di Analysis Services](processing-analysis-services-objects.md)   
 [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)   
 [Creare e gestire una partizione remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)   
 [Impostare tabelle writeback delle partizioni](set-partition-writeback.md)   
 [Partizioni abilitate per la scrittura](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Configurare l'archivio di stringhe per dimensioni e partizioni](configure-string-storage-for-dimensions-and-partitions.md)  
  
  

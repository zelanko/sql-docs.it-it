---
title: Scheda convalida incrociata (vista grafico di accuratezza Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5a8508218ed6a2b4407943fe962959e3cd4f97d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086623"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>Scheda Convalida incrociata (vista Grafico accuratezza modello di data mining)
  La convalida incrociata consente di partizionare una struttura di data mining in sezioni trasversali, eseguire in maniera iterativa il training dei modelli e testarli a fronte di ciascuna sezione trasversale. È possibile specificare un numero di riduzioni in cui suddividere i dati. Ciascuna riduzione viene a sua volta utilizzata come dati di test, mentre i dati rimanenti vengono usati per eseguire il training di un nuovo modello. In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene quindi generato un set di misure di accuratezza standard per ogni modello. Confrontando le misure relative ai modelli generati per ogni sezione trasversale, è possibile valutare l'affidabilità del modello di data mining per l'intero set di dati.  
  
 Per altre informazioni, vedere [Cross-Validation &#40;Analysis Services - Data Mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Non è possibile usare la funzione di convalida incrociata con i modelli compilati mediante l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series o [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering. Se si esegue il report su una struttura di data mining che contiene tali tipi di modelli, questi ultimi non saranno inclusi nel report.  
  
## <a name="task-list"></a>Elenco attività  
  
-   Specificare il numero di riduzioni.  
  
-   Specificare il numero massimo di case da utilizzare per la convalida incrociata.  
  
-   Specificare la colonna stimabile.  
  
-   Se si desidera, specificare un stato stimabile.  
  
-   Se si desidera, impostare i parametri che consentono di controllare la modalità di valutazione dell'accuratezza della stima.  
  
-   Fare clic su **Ottieni risultati** per visualizzare i risultati della convalida incrociata.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Conteggio di riduzione**  
 Specificare il numero di riduzioni, o partizioni, da creare. Poiché il valore minimo è 2, metà del set di dati viene utilizzata per il testing e l'altra metà per il training.  
  
 Per le strutture di data mining di sessione, il valore massimo è 10.  
  
 Se la struttura di data mining è archiviata in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], il valore massimo è 256.  
  
> [!NOTE]  
>  Aumentando il numero di riduzioni, aumenta anche il tempo necessario per l'esecuzione della convalida incrociata. È possibile che si verifichino problemi di prestazioni se il numero di case e il valore di **Conteggio di riduzione** sono grandi.  
  
 **Numero massimo di case**  
 Specificare il numero massimo di case da utilizzare per la convalida incrociata. Il numero di case in una determinata riduzione corrisponde al valore **Numero massimo di case** diviso per il valore **Conteggio di riduzione** .  
  
 Se **0**è il valore specificato, tutti i case nei dati di origine vengono usati per la convalida incrociata.  
  
 Nessun valore predefinito.  
  
> [!NOTE]  
>  Il tempo di elaborazione è direttamente proporzionale all'aumento del numero di case.  
  
 **Attributo di destinazione**  
 Selezionare una colonna dall'elenco di colonne stimabili presenti in tutti i modelli. Per ciascuna operazione di convalida incrociata è possibile selezionare solo una colonna stimabile.  
  
 Per testare solo i modelli di clustering, selezionare **Cluster**.  
  
 **Stato di destinazione**  
 Digitare un valore o selezionarne uno di destinazione da un elenco a discesa di valori.  
  
 Il valore predefinito è `null`, ad indicare che deve essere eseguito il test di tutti gli stati.  
  
 Opzione disabilitata per i modelli di clustering.  
  
 **Soglia**  **di destinazione**  
 Specificare un valore compreso tra 0 e 1 per indicare la probabilità di stima al di sopra della quale uno stato stimato viene considerato corretto. Il valore può essere impostato con incrementi di 0,1.  
  
 Il valore predefinito è `null`, ad indicare che la stima più probabile viene conteggiata come corretta.  
  
> [!NOTE]  
>  Anche se è possibile impostare 0,0, l'utilizzo di questo valore aumenta il tempo di elaborazione e non produce risultati significativi.  
  
 **Ottieni risultati**  
 Fare clic per avviare la convalida incrociata del modello mediante i parametri specificati.  
  
 Il modello viene partizionato nel numero specificato di riduzioni e viene eseguito il test di un modello distinto per ciascuna riduzione. La restituzione di risultati da parte della convalida incrociata potrebbe pertanto richiedere del tempo.  
  
 Per altre informazioni sull'interpretazione dei risultati del report di convalida incrociata, vedere [Misure nel report di convalida incrociata](data-mining/measures-in-the-cross-validation-report.md).  
  
## <a name="setting-the-accuracy-threshold"></a>Impostazione della soglia di accuratezza  
 È possibile controllare lo standard per valutare l'accuratezza della stima impostando un valore per l'opzione **Soglia** **di destinazione**. Una soglia rappresenta una sorta di barra di accuratezza. A ogni stima viene assegnata una probabilità di correttezza del valore stimato. Se si imposta pertanto **Soglia** **di destinazione** su un valore più prossimo a 1, si richiede che la probabilità per una determinata stima sia abbastanza elevata da essere considerata come affidabile. Viceversa, se si imposta il valore **Soglia** **di destinazione** più prossimo a 0, anche le stime con i valori di probabilità più bassi vengono considerate come affidabili.  
  
 Non esiste un valore soglia consigliato perché la probabilità di una stima dipende dalla quantità di dati e dal tipo di valutazione che si sta effettuando. È necessario esaminare le stime a livelli di probabilità diversi per determinare una barra di accuratezza appropriata per i dati. È importante seguire questa procedura perché il valore impostato per **Soglia** **di destinazione** influisce sull'accuratezza di misurazione del modello.  
  
 Si supponga ad esempio che vengano effettuate tre stime per un particolare stato di destinazione e che le probabilità di ogni stima siano 0,05, 0,15 e 0,8. Se si imposta la soglia su 0,5, solo una stima viene conteggiata come corretta. Se si imposta **Soglia** **di destinazione** su 0,10, due stime vengono conteggiate come corrette.  
  
 Quando **destinazione** **soglia** è impostato su `null`, che rappresenta il valore predefinito, la stima più probabile per ogni case è conteggiata come corretta. Nell'esempio precedente, 0,05, 0,15 e 0,8 sono le probabilità per le stime nei tre diversi case. Nonostante le probabilità siano molto diverse, ciascuna stima viene conteggiata come corretta, perché ogni case genera una sola stima. Si tratta inoltre delle stime migliori per tali case.  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)   
 [Convalida incrociata &#40;Analysis Services - Data mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [Misure nel Report di convalida incrociata](data-mining/measures-in-the-cross-validation-report.md)   
 [Stored procedure di data mining &#40;Analysis Services - Data mining&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  

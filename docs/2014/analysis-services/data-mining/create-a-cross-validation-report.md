---
title: Creazione di un report di convalida incrociata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- validating data mining models
- mining structures [Analysis Services], how-to topics
- cross-validation [data mining]
- statistical standard deviation
ms.assetid: 7b1fec4c-7053-41eb-b030-5179257967a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29a60a5b14b1d9a73e0a9a1bdc84a314b55cd1f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085531"
---
# <a name="create-a-cross-validation-report"></a>Creare un report di convalida incrociata
  In questo argomento viene illustrata la creazione di un report di convalida incrociata utilizzando la scheda Grafico di accuratezza in Progettazione modelli di data mining. Per informazioni generali sui report di convalida incrociata e sulle misure statistiche in esso contenute, vedere [Convalida incrociata &#40;Analysis Services - Data mining&#41;](cross-validation-analysis-services-data-mining.md).  
  
 Un report di convalida incrociata è fondamentalmente diverso da un grafico di accuratezza, ad esempio una matrice di classificazione.  
  
-   La convalida incrociata consente di valutare la distribuzione complessiva dei dati utilizzati in un modello o una struttura, pertanto non si specifica un set di dati di test. La convalida incrociata è sempre basata sull'utilizzo dei soli dati originali utilizzati per il training del modello o della struttura di data mining.  
  
-   La convalida incrociata può essere eseguita solo rispetto a un singolo risultato stimabile. Se la struttura supporta modelli con attributi stimabili diversi, è necessario creare report separati per ogni output stimabile.  
  
-   Solo i modelli correlati alla struttura attualmente selezionata sono disponibili per la convalida incrociata.  
  
-   Se la struttura attualmente selezionata supporta una combinazione di modelli di clustering e non, quando si fa clic su **Ottieni risultati**, la stored procedure di convalida incrociata caricherà automaticamente i modelli che presentano la stessa colonna stimata e ignorerà i modelli di clustering che non condividono lo stesso attributo stimabile.  
  
-   È possibile creare un report di convalida incrociata su un modello di clustering che non dispone di un attributo stimabile solo se la struttura di data mining non supporta altri attributi stimabili.  
  
### <a name="select-a-mining-structure"></a>Selezionare una struttura di data mining  
  
1.  Aprire Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  In Esplora soluzioni aprire il database che contiene la struttura o il modello per cui si desidera creare un report.  
  
3.  Fare doppio clic sulla struttura di data mining per aprire la struttura e i modelli correlati in Progettazione modelli di data mining.  
  
4.  Fare clic sulla scheda **Grafico accuratezza modello di data mining** .  
  
5.  Fare clic sulla scheda **Convalida incrociata** .  
  
### <a name="set-cross-validation-options"></a>Impostare le opzioni di convalida incrociata  
  
1.  Nella scheda **Convalida incrociata** per **FoldCount**fare clic sulla freccia giù per selezionare un numero compreso tra 1 e 10. Il valore predefinito è 10.  
  
     
  **FoldCount** rappresenta il numero di partizioni che verranno create all'interno del set di dati originali. Se si imposta FoldCount su 1, il set di training verrà utilizzato senza partizionamento.  
  
2.  Per **TargetAttribute**fare clic sulla freccia verso il basso e selezionare una colonna nell'elenco. Se si tratta di un modello di clustering, selezionare **#Cluster** per indicare che il modello non dispone di un modello stimabile. Si noti che il valore **#Cluster**è disponibile solo quando la struttura di data mining non supporta altri tipi di attributi stimabili.  
  
     È possibile selezionare solo un attributo stimabile per report. Per impostazione predefinita, tutti i modelli correlati che includono lo stesso attributo stimabile vengono inclusi nel report.  
  
3.  Per **MaxCases**digitare un numero sufficientemente elevato per fornire un esempio rappresentativo di dati quando questi sono suddivisi fra il numero specificato di riduzioni. Se il numero è maggiore del conteggio dei case nel set di training del modello, verranno utilizzati tutti i case.  
  
     Se il set di dati di training è di dimensioni molto elevate, l'impostazione del valore per **MaxCases** limita il numero totale di case elaborati e consente di completare il report più rapidamente. È tuttavia consigliabile non impostare **MaxCases** su un valore troppo basso. In questo caso, il numero di dati per la convalida incrociata potrebbe risultare insufficiente.  
  
4.  Per **TargetState**è possibile digitare il valore dell'attributo stimabile di cui eseguire la modellazione. Se, ad esempio, per la colonna [Bike Buyer] sono possibili due valori, ovvero 1 (Sì) e 2 (No), è possibile immettere il valore 1 per valutare l'accuratezza del modello per il risultato desiderato.  
  
    > [!NOTE]  
    >  Se non si immette alcun valore, l'opzione **TargetThreshold** non è disponibile e il modello viene valutato per tutti i valori possibili dell'attributo stimabile.  
  
5.  Per **TargetThreshold**è possibile digitare un numero decimale compreso tra 0 e 1 per specificare la probabilità minima da applicare a una stima affinché questa venga ritenuta accurata.  
  
     Per suggerimenti aggiuntivi sull'impostazione di soglie di probabilità, vedere [Misure nel report di convalida incrociata](measures-in-the-cross-validation-report.md).  
  
6.  Fare clic su **Ottieni risultati**.  
  
### <a name="print-the-cross-validation-report"></a>Stampare il report di convalida incrociata  
  
1.  Fare clic con il pulsante destro del mouse sul report completato nella scheda **Convalida incrociata** .  
  
2.  Scegliere **Stampa** o **Anteprima di stampa** dal menu di scelta rapida per controllare il report prima di stamparlo.  
  
### <a name="create-a-copy-of-the-report-in-microsoft-excel"></a>Creare una copia del report in Microsoft Excel  
  
1.  Fare clic con il pulsante destro del mouse sul report completato nella scheda **Convalida incrociata** .  
  
2.  Dal menu di scelta rapida scegliere **Seleziona tutto**.  
  
3.  Fare clic con il pulsante destro del mouse sul testo selezionato, quindi scegliere **Copia**.  
  
4.  Incollare la selezione in una cartella di lavoro di Excel aperta. Se si utilizza l'opzione **Incolla** , il report viene incollato in Excel in formato HTML, mantenendo la formattazione di righe e colonne. Se si usano le opzioni **Incolla speciale** per testo o testo Unicode, il report viene incollato in formato delimitato da righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Misure nel report di convalida incrociata](measures-in-the-cross-validation-report.md)  
  
  

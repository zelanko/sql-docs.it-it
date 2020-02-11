---
title: 'Lezione 3: elaborazione della struttura e dei modelli della serie temporale | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 16e27b57-eae1-47a7-a02c-47b6ed487d87
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 493d27c9836eb765c655eba5bbb004e4d48cde40
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042877"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>Lezione 3: Elaborazione di strutture e modelli Time Series
  In questa lezione verrà utilizzata l'istruzione [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) per elaborare le strutture di data mining e i modelli di data mining di serie temporali creati.  
  
 Quando si elabora una struttura di data mining, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] legge i dati di origine e compila le strutture che supportano i modelli di data mining. È sempre necessario elaborare i modelli e le strutture di data mining al momento della creazione. Se si specifica una struttura di data mining utilizzando INSERT INTO, l'istruzione elabora la struttura e tutti i modelli di data mining associati.  
  
 Quando si aggiunge un modello di data mining a una struttura di data mining già elaborata, è possibile utilizzare l'istruzione `INSERT INTO MINING MODEL` per elaborare solo il nuovo modello di data mining utilizzando i dati esistenti.  
  
 Per ulteriori informazioni sull'elaborazione dei modelli di data mining, vedere [requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining ](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
## <a name="insert-into-statement"></a>Istruzione INSERT INTO  
 Per eseguire il training della struttura di data mining Time Series e di tutti i modelli di data mining associati, utilizzare l'istruzione [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) . Il codice nell'istruzione può essere suddiviso nelle parti seguenti.  
  
-   Identificazione della struttura di data mining  
  
-   Creazione di un elenco delle colonne nella struttura di data mining  
  
-   Definizione dei dati di training  
  
 Di seguito è riportato un esempio generico di istruzione `INSERT INTO`:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY (<source data definition>)  
```  
  
 La prima riga del codice identifica la struttura di data mining di cui si eseguirà il training:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 Le successive righe del codice specificano le colonne definite dalla struttura di data mining. È necessario che siano elencate tutte le colonne nella struttura di data mining e ogni colonna deve essere associata a una colonna nei dati della query di origine.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 Le ultime righe del codice definiscono i dati che verranno utilizzati per il training della struttura di data mining.  
  
```  
OPENQUERY (<source data definition>)  
```  
  
 In questa lezione si utilizzerà `OPENQUERY` per definire i dati di origine. Per altre informazioni sugli altri metodi di definizione di una query sui dati di origine, vedere [&#60;query sui dati di origine&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verrà eseguita l'attività seguente:  
  
-   Elaborare la struttura di data mining Forecasting_MIXED_Structure  
  
-   Elaborare i modelli di data mining correlati Forecasting_MIXED, Forecasting_ARIMA e Forecasting_ARTXP  
  
## <a name="processing-the-time-series-mining-structure"></a>Elaborazione della struttura di data mining di serie temporali  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>Per elaborare la struttura e i relativi modelli di data mining utilizzando INSERT INTO.  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione INSERT INTO nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    [<mining structure>]  
    ```  
  
     con:  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining structure columns>  
    ```  
  
     con:  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     con:  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     La query di origine fa [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] riferimento all'origine dati definita nel progetto di esempio IntermediateTutorial. Utilizza tale origine dati per accedere alla vista vTimeSeries contenente i dati di origine che verranno utilizzati per il training del modello di data mining. Se non si ha familiarità con questo progetto o con queste viste, vedere[lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Forecasting_MIXED_Structure]  
    (  
       [ReportingDate],[ModelRegion],[Quantity],[Amount])  
    )  
    OPENQUERY(  
    [Adventure Works DW 2008R2],  
    'SELECT [ReportingDate],[ModelRegion],[Quantity],[Amount] FROM vTimeSeries ORDER BY [ReportingDate]'  
    )   
    ```  
  
6.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
7.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `ProcessForecastingAll.dmx`il nome.  
  
8.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
 Al termine dell'esecuzione della query, è possibile creare stime utilizzando i modelli di data mining elaborati. Nella lezione successiva verranno create diverse stime basate sui modelli di data mining creati.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Creazione di stime basate su serie temporali utilizzando DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;query sui dati di origine&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)  
  
  

---
title: 'Lezione 1: creazione di un modello di data mining e di una struttura di data mining Time Series | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2513bc3837dd224f6561eb0015ced538ea3add8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62678447"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>Lezione 1: Creazione di un modello di data mining Time Series e di una struttura di data mining
  In questa lezione verrà creato un modello di data mining che consente di eseguire una stima di valori nel tempo in base a dati cronologici. Al momento della creazione del modello, la struttura sottostante verrà generata automaticamente e potrà essere utilizzata come base per nuovi modelli di data mining.  
  
 Questa lezione presuppone che l'utente abbia familiarità con i modelli di previsione e con i requisiti dell'algoritmo Microsoft Time Series. Per altre informazioni, vedere [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
## <a name="create-mining-model-statement"></a>Istruzione CREATE MINING MODEL  
 Per creare direttamente un modello di data mining e generare automaticamente la struttura di data mining sottostante, è possibile utilizzare l'istruzione [create mining model &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx) . Il codice nell'istruzione può essere suddiviso nelle parti seguenti:  
  
-   Assegnazione di un nome al modello  
  
-   Definizione del timestamp  
  
-   Definizione della colonna chiave della serie facoltativa  
  
-   Definizione di uno o più attributi stimabili  
  
 Di seguito è riportato un esempio generico dell'istruzione CREATE MINING MODEL:  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 La prima riga del codice definisce il nome del modello di data mining:  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 Il nome della struttura sottostante viene generato automaticamente in Analysis Services aggiungendo il suffisso "_structure" al nome del modello, per assicurare l'utilizzo di un nome univoco derivato dal nome del modello. Per informazioni sulla denominazione di un oggetto in DMX, vedere [identificatori &#40;&#41;DMX ](/sql/dmx/identifiers-dmx).  
  
 La riga successiva definisce la colonna chiave del modello di data mining, che nel caso di un modello Time Series identifica in modo univoco un intervallo temporale nei dati di origine. L'intervallo temporale è identificato dalle parole chiave `KEY TIME` dopo il nome di colonna e i tipi di dati. Se il modello Time Series dispone di una chiave della serie separata, questa viene identificata tramite la parola chiave `KEY`.  
  
```  
<key columns>  
```  
  
 La riga successiva del codice viene utilizzata per definire le colonne del modello di cui verrà eseguita la stima. Un modello di data mining può contenere più attributi stimabili. In tal caso, l'algoritmo Microsoft Time Series genererà un'analisi distinta per ogni serie:  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Creazione di una nuova query vuota  
  
-   Modifica della query per creare il modello di data mining  
  
-   Esecuzione della query  
  
## <a name="creating-the-query"></a>Creazione della query  
 Il primo passaggio consiste nella connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e nella creazione di una nuova query DMX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Per creare una nuova query DMX in SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Nella finestra di dialogo **Connetti al server** selezionare **Analysis Services**per **tipo di server**. In **nome server**, digitare `LocalHost`o il nome dell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a cui si desidera connettersi per questa lezione. Fare clic su **Connetti**.  
  
3.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
## <a name="altering-the-query"></a>Modifica della query  
 Il passaggio successivo consiste nel modificare l'istruzione CREATE MINING MODEL per creare il modello di data mining utilizzato per la previsione, insieme alla struttura di data mining sottostante.  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>Per personalizzare l'istruzione CREATE MINING MODEL  
  
1.  Nell'editor di query copiare l'esempio generico dell'istruzione CREATE MINING MODEL nella query vuota.  
  
2.  Sostituire quanto segue:  
  
    ```  
    [mining model name]   
    ```  
  
     con:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  Sostituire quanto segue:  
  
    ```  
    <key columns>  
    ```  
  
     con:  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     La parola chiave `TIME KEY` indica che la colonna ReportingDate contiene i valori dell'intervallo temporale utilizzati per ordinare i valori. Gli intervalli temporali possono essere date e ore, numeri interi o qualsiasi tipo di dati ordinati, purché i valori siano univoci e i dati vengano ordinati.  
  
     Le parole chiave `TEXT` e `KEY` indicano che la colonna ModelRegion contiene una chiave della serie aggiuntiva. È consentita solo una chiave della serie e i valori della colonna devono essere distinti.  
  
4.  Sostituire quanto segue:  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     con:  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     con:  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     Il parametro `AUTO_DETECT_PERIODICITY` = 0,8 dell'algoritmo indica che si desidera che l'algoritmo rilevi cicli nei dati. L'impostazione di questo parametro su un valore prossimo a 1 consente di individuare numerosi modelli, ma può rallentare l'elaborazione.  
  
     Il parametro `FORECAST_METHOD` dell'algoritmo indica se si desidera che i dati vengano analizzati tramite ARTXP, ARIMA o una combinazione dei due algoritmi.  
  
     La parola chiave `WITH DRILLTHROUGH` specifica che si desidera essere in grado di visualizzare statistiche dettagliate nei dati di origine dopo il completamento del modello. È necessario aggiungere questa clausola se si desidera esplorare il modello tramite il Visualizzatore Microsoft Time Series. Tale clausola non è necessaria per l'esecuzione di stime.  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
7.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `Forecasting_MIXED.dmx`il nome.  
  
## <a name="executing-the-query"></a>Esecuzione della query  
 Il passaggio conclusivo consiste nell'esecuzione della query. Dopo la creazione e il salvataggio di una query, è necessario eseguirla per creare il modello di data mining e la relativa struttura sul server. Per ulteriori informazioni sull'esecuzione di query nell'editor di query, vedere [motore di database editor di query &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Per eseguire la query  
  
-   Nell'editor di query fare clic su **Esegui**sulla barra degli strumenti.  
  
     Lo stato della query viene visualizzato nella scheda **messaggi** nella parte inferiore dell'editor di query al termine dell'esecuzione dell'istruzione. Dovrebbero essere visualizzati i messaggi seguenti:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Nel server è presente una nuova struttura denominata **Forecasting_MIXED_Structure** , insieme al modello di data mining correlato **Forecasting_MIXED**.  
  
 Nella lezione successiva verrà aggiunto un modello di data mining alla struttura di data mining **Forecasting_MIXED** appena creata.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Aggiunta di modelli di data mining alla struttura di data mining Time Series](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto del modello di data mining per i modelli Time Series &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  

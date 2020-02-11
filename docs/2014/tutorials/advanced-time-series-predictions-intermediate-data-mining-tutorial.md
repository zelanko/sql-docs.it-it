---
title: Stime avanzate basate su serie temporali (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca144d1d473f7df49f73d5ed170052c61ce6107d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893697"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>Stime avanzate basate su serie temporali (Esercitazione intermedia sul data mining)
  Dall'esplorazione del modello di previsione è emerso che, benché le vendite nella maggior parte delle aree geografiche seguano uno schema analogo, alcune aree e alcuni modelli, ad esempio il modello M200 nell'area del Pacifico, mostrano tendenze molto diverse. Questo risultato non è sorprendente, in quanto è noto che differenze tra le diverse aree sono comuni e possono essere causate da numerosi fattori, tra cui promozioni marketing, produzione di report imprecisi o eventi geopolitici.  
  
 Gli utenti richiedono tuttavia un modello che possa essere applicato a livello mondiale. Per ridurre quindi l'influenza di questi singoli fattori sulle proiezioni, si decide di compilare un modello basato su misure aggregate di vendite mondiali. Sarà quindi possibile utilizzare questo modello per eseguire stime per le singole aree.  
  
 In questa attività si compileranno tutte le origini dati necessarie per eseguire le attività di stima avanzate. Verranno create due viste origine dati da utilizzare come input per la query di stima e una vista origine dati da utilizzare per la compilazione del nuovo modello.  
  
 **Passaggi**  
  
1.  [Preparare i dati di vendita estesi (per la stima)](#bkmk_newExtendData)  
  
2.  [Preparare i dati aggregati (per la compilazione del modello)](#bkmk_newReplaceData)  
  
3.  [Preparare i dati della serie (per la stima incrociata)](#bkmk_CrossData2)  
  
4.  [Eseguire la stima utilizzando EXTEND](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [Creare il modello di stima incrociata](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [Eseguire la stima utilizzando REPLACE](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [Rivedere le nuove stime](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="bkmk_newExtendData"></a>Creazione dei nuovi dati di vendita estesi  
 Per aggiornare i dati di vendita, sarà necessario ottenere le cifre di vendita più recenti. Sono di particolare interesse solo i dati dalla regione del Pacifico, dove è stata avviata una promozione di vendite regionali per richiamare l'attenzione sui nuovi punti vendita e generare consapevolezza dei prodotti.  
  
 Per questo scenario si presuppone che i dati siano stati importati da una cartella di lavoro di Excel che contiene solo tre mesi di nuovi dati per un paio di aree. Si creerà una tabella per i dati utilizzando uno script Transact-SQL e quindi si definirà una vista origine dati da utilizzare per la stima.  
  
#### <a name="create-the-table-with-new-sales-data"></a>Creare la tabella con i nuovi dati di vendita  
  
1.  In una finestra di query Transact-SQL eseguire l'istruzione seguente per aggiungere i dati di vendita al database AdventureWorksDW o a qualsiasi altro database.  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  Inserire i nuovi valori utilizzando lo script seguente.  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  Le virgolette vengono utilizzate con i valori di valuta per evitare problemi con il separatore virgola e il simbolo di valuta. È inoltre possibile passare i valori della valuta in questo formato: `130170.22`  
    >   
    >  Si noti che le date utilizzate nel database di esempio sono state modificate per questa versione. Se si utilizza una versione di AdventureWorks precedente, potrebbe essere necessario modificare le date inserite in modo appropriato.  
  
###  <a name="bkmk_newReplaceData"></a>Creare una vista origine dati utilizzando i nuovi dati di vendita  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **viste origine dati**, quindi scegliere **nuova vista origine dati**.  
  
2.  Nella Creazione guidata vista origine dati effettuare le selezioni seguenti:  
  
     **Origine dati**:[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selezione tabelle e viste**: selezionare la tabella appena creata, NewSalesData.  
  
3.  Fare clic su **Fine**.  
  
4.  Nell'area di progettazione della vista origine dati fare clic con il pulsante destro del mouse su NewSalesData, quindi scegliere **Esplora dati** per verificare i dati.  
  
> [!WARNING]  
>  Si utilizzeranno solo questi dati per la stima, pertanto non si importa se i dati sono incompleti.  
  
##  <a name="bkmk_CrossData2"></a>Creazione dei dati per il modello di stima incrociata  
 I dati utilizzati nel modello di previsione originale sono già raggruppati approssimativamente dalla vista vTimeSeries in cui diversi modelli di bicicletta sono stati compressi in un numero di categorie inferiore e i risultati di singoli paesi sono stati uniti in aree. Per creare un modello che possa essere utilizzato per le proiezioni mondiali, si creeranno direttamente alcune semplici aggregazioni aggiuntive nella finestra di progettazione Vista origine dati. La nuova vista origine dati contiene solo una somma e una media delle vendite di tutti i prodotti per tutte le aree.  
  
 Dopo avere creato l'origine dati per il modello, è necessario creare una nuova vista origine dati da utilizzare per la stima. Se si desidera ad esempio stimare le vendite per l'Europa utilizzando il nuovo modello mondiale, è necessario inserire i dati solo per l'area Europa. Si configurerà quindi una nuova vista origine dati che filtra i dati originali e si modificherà la condizione di filtro per ogni set di query di stima.  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>Per creare i dati del modello utilizzando una vista origine dati personalizzata  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **viste origine dati**, quindi scegliere **nuova vista origine dati**.  
  
2.  Nella pagina di benvenuto della procedura guidata fare clic su **Avanti**.  
  
3.  Nella pagina **Selezionare un'origine dati** selezionare [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], quindi scegliere **Avanti**.  
  
4.  Nella pagina **selezionare tabelle e viste**, non aggiungere alcuna tabella. fare semplicemente clic su **Avanti**.  
  
5.  Nella pagina **Completamento procedura guidata**Digitare il nome `AllRegions`e quindi fare clic su **fine**.  
  
6.  Fare quindi clic con il pulsante destro del mouse sull'area di progettazione della vista origine dati vuota, quindi scegliere **nuova query denominata**.  
  
7.  Nella finestra di dialogo **Crea query denominata** , per **nome**, digitare `AllRegions`e per **Descrizione**digitare **somma e media delle vendite per tutti i modelli e le aree**.  
  
8.  Nel riquadro Testo SQL digitare l'istruzione seguente, quindi scegliere OK:  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. Fare clic con il `AllRegions` pulsante destro del mouse sulla tabella, quindi scegliere **Esplora dati**.  
  
###  <a name="bkmk_CrossData"></a>Per creare i dati della serie per la stima incrociata  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **viste origine dati**, quindi scegliere **nuova vista origine dati**.  
  
2.  Nella Creazione guidata vista origine dati effettuare le selezioni seguenti:  
  
     **Origine dati**:[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selezione tabelle e viste**: non selezionare alcuna tabella  
  
     **Nome**:`T1000 Pacific Region`  
  
3.  Fare clic su **Fine**.  
  
4.  Fare clic con il pulsante destro del mouse sull'area di progettazione vuota per **T1000 Pacific Region. DSV**, quindi scegliere **nuova query denominata**.  
  
     Verrà visualizzata la finestra di dialogo **Crea query denominata** . Digitare nuovamente il nome e aggiungere la descrizione seguente:  
  
     **Nome**:`T1000 Pacific Region`  
  
     **Descrizione**: **filtrare`vTimeSeries`per area e modello**  
  
5.  Nel riquadro Testo digitare la query seguente, quindi scegliere OK:  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  Poiché è necessario creare stime separatamente per ogni serie, è possibile copiare il testo della query e salvarlo in un file di testo, in modo da poterlo riutilizzare per l'altra serie di dati.  
  
6.  Nell'area di progettazione della vista origine dati fare clic con il pulsante destro del mouse su T1000 Pacific, quindi scegliere **Esplora dati** per verificare che i dati vengano filtrati correttamente.  
  
     Si utilizzeranno questi dati come input del modello in caso di creazione di query di stima incrociata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Stime basate su serie temporali che utilizzano dati aggiornati &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Viste origine dati in modelli multidimensionali](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  

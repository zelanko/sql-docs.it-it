---
title: Advanced stime basate su serie temporali (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a45d0bf0878b472e4979c00a5a38e8b01974a22
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544332"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>Stime avanzate basate su serie temporali (Esercitazione intermedia sul data mining)
  Dall'esplorazione del modello di previsione è emerso che, benché le vendite nella maggior parte delle aree geografiche seguano uno schema analogo, alcune aree e alcuni modelli, ad esempio il modello M200 nell'area del Pacifico, mostrano tendenze molto diverse. Questo risultato non è sorprendente, in quanto è noto che differenze tra le diverse aree sono comuni e possono essere causate da numerosi fattori, tra cui promozioni marketing, produzione di report imprecisi o eventi geopolitici.  
  
 Gli utenti richiedono tuttavia un modello che possa essere applicato a livello mondiale. Per ridurre quindi l'influenza di questi singoli fattori sulle proiezioni, si decide di compilare un modello basato su misure aggregate di vendite mondiali. Sarà quindi possibile utilizzare questo modello per eseguire stime per le singole aree.  
  
 In questa attività si compileranno tutte le origini dati necessarie per eseguire le attività di stima avanzate. Verranno create due viste origine dati da utilizzare come input per la query di stima e una vista origine dati da utilizzare per la compilazione del nuovo modello.  
  
 **Passaggi**  
  
1.  [Preparare i dati di vendita estesi (per la stima)](#bkmk_newExtendData)  
  
2.  [Preparare i dati aggregati (per la compilazione del modello)](#bkmk_newReplaceData)  
  
3.  [Preparare i dati di serie (per la stima incrociata)](#bkmk_CrossData2)  
  
4.  [Eseguire la stima utilizzando EXTEND](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [Creare il modello di stima incrociata](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [Eseguire la stima utilizzando REPLACE](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [Rivedere le nuove stime](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="bkmk_newExtendData"></a> Creazione di nuovi dati di vendita estesi  
 Per aggiornare i dati di vendita, sarà necessario ottenere le cifre di vendita più recenti. Sono di particolare interesse solo i dati dalla regione del Pacifico, dove è stata avviata una promozione di vendite regionali per richiamare l'attenzione sui nuovi punti vendita e generare consapevolezza dei prodotti.  
  
 Per questo scenario, si partirà dal presupposto che i dati importati da una cartella di lavoro di Excel che contiene solo tre mesi di nuovi dati per un paio di aree. È possibile creare una tabella per i dati usando uno script Transact-SQL e quindi definire una vista origine dati da utilizzare per la stima.  
  
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
  
###  <a name="bkmk_newReplaceData"></a> Creare una vista origine dati usando i nuovi dati di vendita  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **viste origine dati**, quindi selezionare **nuova vista origine dati**.  
  
2.  Nella Creazione guidata vista origine dati effettuare le selezioni seguenti:  
  
     **Zdroj dat**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selezione tabelle e viste**: Selezionare la tabella appena creato, NewSalesData.  
  
3.  Scegliere **Fine**.  
  
4.  Nell'area di progettazione vista origine dati, fare doppio clic su NewSalesData e quindi selezionare **Esplora dati** per verificare i dati.  
  
> [!WARNING]  
>  Si utilizzeranno solo questi dati per la stima, pertanto non si importa se i dati sono incompleti.  
  
##  <a name="bkmk_CrossData2"></a> Creazione dei dati per il modello di stima incrociata  
 I dati che è stati usati nell'originale previsione modello è stato già raggruppati approssimativamente dalla vista vTimeSeries, compressi diversi modelli di biciclette in un numero minore di categorie e unire i risultati di singoli paesi in aree. Per creare un modello che possa essere utilizzato per le proiezioni mondiali, si creeranno direttamente alcune semplici aggregazioni aggiuntive nella finestra di progettazione Vista origine dati. La nuova vista origine dati contiene solo una somma e una media delle vendite di tutti i prodotti per tutte le aree.  
  
 Dopo avere creato l'origine dati per il modello, è necessario creare una nuova vista origine dati da utilizzare per la stima. Se si desidera ad esempio stimare le vendite per l'Europa utilizzando il nuovo modello mondiale, è necessario inserire i dati solo per l'area Europa. Si configurerà quindi una nuova vista origine dati che filtra i dati originali e si modificherà la condizione di filtro per ogni set di query di stima.  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>Per creare i dati del modello utilizzando una vista origine dati personalizzata  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **viste origine dati**, quindi selezionare **nuova vista origine dati**.  
  
2.  Nella pagina di benvenuto della procedura guidata fare clic su **Avanti**.  
  
3.  Nella pagina **Selezionare un'origine dati** selezionare [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], quindi scegliere **Avanti**.  
  
4.  Nella pagina **selezione tabelle e viste**, non aggiungere qualsiasi tabelle, fai clic **successivo**.  
  
5.  Nella pagina **Completamento procedura guidata**, digitare il nome `AllRegions`, quindi fare clic su **fine**.  
  
6.  Successivamente, l'area di progettazione vista origine dati vuota e quindi scegliere **nuova Query denominata**.  
  
7.  Nel **crea Query denominata** della finestra di dialogo per **nome**, digitare `AllRegions`e per **descrizione**, tipo **somma e Media delle vendite per tutti i modelli e aree**.  
  
8.  Nel riquadro Testo SQL digitare l'istruzione seguente, quindi scegliere OK:  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. Fare doppio clic il `AllRegions` tabella e quindi selezionare **Esplora dati**.  
  
###  <a name="bkmk_CrossData"></a> Per creare i dati della serie per la stima incrociata  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **viste origine dati**, quindi selezionare **nuova vista origine dati**.  
  
2.  Nella Creazione guidata vista origine dati effettuare le selezioni seguenti:  
  
     **Zdroj dat**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selezione tabelle e viste**: Non selezionare alcuna tabella  
  
     **Nome**: `T1000 Pacific Region`  
  
3.  Scegliere **Fine**.  
  
4.  Fare doppio clic su area di progettazione vuota per **T1000 Pacific Region. dsv**, quindi selezionare **nuova Query denominata**.  
  
     Verrà visualizzata la finestra di dialogo **Crea query denominata** . Digitare nuovamente il nome e aggiungere la descrizione seguente:  
  
     **Nome**: `T1000 Pacific Region`  
  
     **Descrizione**: **Filtro`vTimeSeries`per area e modello**  
  
5.  Nel riquadro Testo digitare la query seguente, quindi scegliere OK:  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  Poiché è necessario creare stime separatamente per ogni serie, è possibile copiare il testo della query e salvarlo in un file di testo, in modo da poterlo riutilizzare per l'altra serie di dati.  
  
6.  Nell'area di progettazione vista origine dati, fare doppio clic su T1000 Pacific e quindi selezionare **Esplora dati** per verificare che i dati vengano filtrati correttamente.  
  
     Si utilizzeranno questi dati come input del modello in caso di creazione di query di stima incrociata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Stime basate su serie utilizzando dati aggiornati di tempo &#40;esercitazione intermedia sul Data Mining dei dati&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Viste origine dati in modelli multidimensionali](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

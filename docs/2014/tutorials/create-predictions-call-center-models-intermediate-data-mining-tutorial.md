---
title: Creazione di stime per i modelli Call Center (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5be0cec7-f639-4eeb-835e-e3204ae619e9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30f24ab457669f572189d2eb13deca3f672f5e18
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217879"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>Creazione di stime per i modelli Call Center (Esercitazione intermedia sul data mining)
  Dopo aver appreso i concetti di base sulle interazioni tra turni, numero di operatori, chiamate e livello del servizio, è possibile creare alcune query di stima che possono essere utilizzate per l'analisi e la pianificazione aziendali. Verranno innanzitutto create alcune stime del modello esplorativo per testare alcune ipotesi. Verranno quindi create stime bulk utilizzando il modello di regressione logistica.  
  
 Per questa lezione si presuppone che l'utente abbia già acquisito familiarità con il concetto di query di stima.  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>Creazione di stime tramite il modello di rete neurale  
 Nell'esempio seguente viene illustrato come eseguire una stima singleton utilizzando il modello di rete neurale creato per l'esplorazione. Le stime singleton sono una soluzione valida per applicare valori diversi per visualizzarne l'effetto nel modello. In questo scenario si stimerà il livello del servizio per il turno di mezzanotte, senza specificare il giorno della settimana, se sei operatori esperti sono in servizio.  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>Per creare una query singleton utilizzando il modello di rete neurale  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire la soluzione contenente il modello che si desidera utilizzare.  
  
2.  Progettazione modelli di Data Mining, fare clic sui **stima modello di Data Mining** scheda.  
  
3.  Nel **modello di Data Mining** riquadro, fare clic su **Seleziona modello**.  
  
4.  Il **modello di Data Mining selezionare** nella finestra di dialogo Visualizza un elenco di strutture di data mining. Espandere la struttura di data mining per visualizzare un elenco dei modelli di data mining associati alla struttura.  
  
5.  Espandere la struttura di data mining Call Center Default e selezionare il modello di rete neurale Call Center - LR.  
  
6.  Scegliere **Query singleton** dal menu **Modello di data mining**.  
  
     Il **Input Query Singleton** verrà visualizzata la finestra di dialogo, con le colonne mappate alle colonne nel modello di data mining.  
  
7.  Nel **Input Query Singleton** finestra di dialogo, fare clic sulla riga Shift e quindi selezionare *mezzanotte*.  
  
8.  Fare clic sulla riga Lvl 2 Operators e tipo `6`.  
  
9. Nella parte inferiore della metà del **stima modello di Data Mining** , fare clic sulla prima riga nella griglia.  
  
10. Nel **origine** colonna, fare clic sulla freccia verso il basso e selezionare **funzione di stima**. Nel **campo** colonna, selezionare **PredictHistogram**.  
  
     Viene visualizzato un elenco di argomenti che è possibile usare con questa funzione di stima automaticamente nel **criteri/argomento** casella.  
  
11. Trascinare la colonna ServiceGrade dall'elenco di colonne nella **modello di Data Mining** riquadro per il **criteri/argomento** casella.  
  
     Il nome della colonna verrà inserito automaticamente come argomento. È possibile scegliere qualsiasi colonna di attributo stimabile e trascinarla in questa casella di testo.  
  
12. Fare clic sul pulsante **visualizzazione di risultati a query**, nell'angolo superiore del generatore di Query di stima.  
  
 I risultati previsti contengono i possibili valori stimati per ogni livello del servizio considerando questi input, nonché i valori di supporto e probabilità per ogni stima. È possibile tornare in qualsiasi momento alla visualizzazione di progettazione per modificare gli input o aggiungerne altri.  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>Creazione di stime tramite un modello di regressione logistica  
 Se si conoscono già gli attributi attinenti al problema aziendale, è possibile utilizzare un modello di regressione logistica per stimare l'effetto della modifica di alcuni attributi. La regressione logistica è un metodo statistico comunemente usato per eseguire stime in base alle modifiche nelle variabili indipendenti. Viene ad esempio usato negli scenari finanziari per prevedere il comportamento dei clienti in base ai relativi dati demografici.  
  
 In questa attività viene illustrato come creare un'origine dati che verrà utilizzata per le stime, quindi come eseguire stime per rispondere a diverse domande aziendali.  
  
### <a name="generating-data-used-for-bulk-prediction"></a>Generazione di dati utilizzati per la stima bulk  
 Esistono diversi modi per fornire dati di input: ad esempio, è possibile importare livelli del personale da un foglio di calcolo ed eseguire i dati tramite il modello per stimare la qualità del servizio per il mese successivo.  
  
 In questa lezione si utilizzerà la finestra di progettazione Vista origine dati per creare una query denominata. Questa query denominata è un'istruzione Transact-SQL personalizzata che per ogni turno nella pianificazione calcola il numero massimo di operatori che fanno parte del personale, il numero minimo di chiamate ricevute e il numero medio di problemi generati. Si inseriranno quindi i dati in un modello di data mining per eseguire stime su una serie di date imminenti.  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>Per generare dati di input per una query di stima bulk  
  
1.  In Esplora soluzioni fare doppio clic su **viste origine dati**, quindi selezionare **nuova vista origine dati**.  
  
2.  Nella procedura guidata vista origine dati, selezionare [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] come origine dati e quindi fare clic su **successivo**.  
  
3.  Nel **selezione tabelle e viste** pagina, fare clic su **successivo** senza selezionare alcuna tabella.  
  
4.  Nel **Completamento procedura guidata** , digitare il nome, `Shifts`.  
  
     Questo nome verrà visualizzato in Esplora soluzioni come nome della vista origine dati.  
  
5.  Fare clic sul riquadro di progettazione vuota e quindi selezionare **nuova Query denominata**.  
  
6.  Nel **crea Query denominata** della finestra di dialogo per **Name**, tipo `Shifts for Call Center`.  
  
     Questo nome verrà visualizzato solo in Progettazione vista origine dati come nome della query denominata.  
  
7.  Incollare l'istruzione di query seguente nel riquadro di testo SQL nella metà inferiore della finestra di dialogo.  
  
    ```  
    SELECT DISTINCT WageType, Shift,   
    AVG(Orders) as AvgOrders, MIN(Orders) as MinOrders, MAX(Orders) as MaxOrders,  
    AVG(Calls) as AvgCalls, MIN(Calls) as MinCalls, MAX(Calls) as MaxCalls,  
    AVG(LevelTwoOperators) as AvgOperators, MIN(LevelTwoOperators) as MinOperators, MAX(LevelTwoOperators) as MaxOperators,  
    AVG(IssuesRaised) as AvgIssues, MIN(IssuesRaised) as MinIssues, MAX(IssuesRaised) as MaxIssues  
    FROM dbo.FactCallCenter  
    GROUP BY Shift, WageType  
    ```  
  
8.  Nel riquadro di progettazione, fare clic sulla tabella turni per Call Center e selezionare **Esplora dati** per visualizzare in anteprima i dati restituiti dalla query T-SQL.  
  
9. Pulsante destro del mouse della scheda **turni. dsv (progettazione)** e quindi fare clic su **salvare** per salvare la nuova definizione della vista origine dati.  
  
### <a name="predicting-service-metrics-for-each-shift"></a>Stima delle metriche del servizio per ogni turno  
 Dopo aver generato alcuni valori per ogni turno, tali valori verranno utilizzati come input per il modello di regressione logistica compilato per generare alcune stime che è possibile utilizzare nelle pianificazioni aziendali.  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>Per utilizzare la nuova vista origine dati come di input per una query di stima  
  
1.  Progettazione modelli di Data Mining, fare clic sui **stima modello di Data Mining** scheda.  
  
2.  Nel **modello di Data Mining** riquadro, fare clic su **Seleziona modello**e scegliere Call Center - LR nell'elenco dei modelli disponibili.  
  
3.  Dal **modello di Data Mining** menu, deselezionare l'opzione **Query Singleton**. Verrà visualizzato un avviso che indica che gli input della query singleton andranno persi. Fare clic su **OK**.  
  
     Il **Input Query Singleton** finestra di dialogo viene sostituita con il **Seleziona tabelle di Input** nella finestra di dialogo.  
  
4.  Fare clic su **Seleziona tabella del case**.  
  
5.  Nel **Seleziona tabella** selectShifts dall'elenco di origini dati, la finestra di dialogo. Nel **nome tabella/vista** , selezionare turni per Call Center (potrebbe essere selezionato automaticamente) e quindi fare clic su **OK.**  
  
     Il **stima modello di Data Mining** nell'area di progettazione viene aggiornato per mostrare i mapping creati in base ai tipi di dati e i nomi delle colonne nei dati di input e nel modello.  
  
6.  Fare doppio clic su una delle linee di join e quindi selezionare **Modifica connessioni**.  
  
     In questa finestra di dialogo è possibile vedere esattamente di quali colonne è stato eseguito il mapping e di quali no. Il modello di data mining contiene le colonne Calls, Orders, IssuesRaised e LvlTwoOperators di cui è possibile eseguire il mapping a qualsiasi aggregazione creata in base a queste colonne nei dati di origine. In questo scenario si eseguirà il mapping alle medie.  
  
7.  Fare clic sulla cella vuota accanto a LevelTwoOperators e selezionare **turni per chiamare avgoperators**.  
  
8.  Fare clic sulla cella vuota accanto a Calls e selezionare **turni per chiamare avgcalls**. e quindi fare clic su **OK**.  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>Per creare le stime per ogni turno  
  
1.  Nella griglia posta nella parte inferiore della metà del **generatore Query di stima**, fare clic sulla cella vuota sotto **origine,** e selezionare turni per Call Center.  
  
2.  Nella cella vuota sotto **campo**, selezionare Shift.  
  
3.  Fare clic sulla riga vuota successiva nella griglia e ripetere la procedura sopra descritta per aggiungere un'altra riga per WageType.  
  
4.  Fare clic sulla riga vuota successiva nella griglia. Nel **origine** colonna, selezionare **funzione di stima**. Nel **campo** colonna, selezionare **Predict**.  
  
5.  Trascinare la colonna ServiceGrade dal **modello di Data Mining** riquadro alla griglia e competenti, per il **criteri/argomento** cella. Nel **Alias** , digitare **livello di servizio stimato**.  
  
6.  Fare clic sulla riga vuota successiva nella griglia. Nel **origine** colonna, selezionare **funzione di stima**. Nel **campo** colonna, selezionare **PredictProbability**.  
  
7.  Trascinare la colonna ServiceGrade dal **modello di Data Mining** riquadro alla griglia e competenti, per il **criteri/argomento** cella. Nel **Alias** , digitare **probabilità**.  
  
8.  Fare clic su **passare alla visualizzazione dei risultati della query** per visualizzare le stime.  
  
 Nella tabella seguente vengono illustrati i risultati dell'esempio per ogni turno.  
  
|Turno|WageType|Livello di servizio stimato|Probabilità|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|giorno festivo|0.165|0.377520666|  
|mezzanotte|giorno festivo|0.105|0.364105573|  
|PM1|giorno festivo|0.165|0.40056055|  
|PM2|giorno festivo|0.165|0.338532973|  
|AM|giorno feriale|0.165|0.370847617|  
|mezzanotte|giorno feriale|0.08|0.352999173|  
|PM1|giorno feriale|0.165|0.317419177|  
|PM2|giorno feriale|0.105|0.311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>Stima dell'effetto del tempo di risposta ridotto sul livello del servizio  
 Sono stati generati alcuni valori medi per ogni turno e tali valori sono stati utilizzati come input per il modello di regressione logistica. Tuttavia, considerato che l'obiettivo aziendale è mantenere la frequenza di abbandono tra 0,00 e 0,05, i risultati non sono incoraggianti.  
  
 Pertanto, in base al modello originale, che mostra un notevole impatto del tempo di risposta sul livello del servizio, il team di gestione decide di eseguire alcune stime per valutare se, riducendo il tempo medio per la risposta alle chiamate, la qualità del servizio può migliorare. È possibile, ad esempio, valutare le conseguenze per i valori del livello di servizio se si riduce il tempo di risposta alle chiamate al 90% o anche all'80% rispetto al tempo di risposta corrente.  
  
 La creazione di una vista origine dati per il calcolo dei tempi di risposta medi per ogni turno e la successiva aggiunta di colonne per il calcolo dell'80 o 90% del tempo medio di risposta sono operazioni semplici. È quindi possibile utilizzare la vista origine dati come input per il modello.  
  
 Anche se qui non sono illustrati i passaggi esatti, nella tabella seguente vengono confrontati gli effetti sul livello di servizio quando si riducono i tempi di risposta all'80 o a 90% di tempi di risposta correnti.  
  
 Da questi risultati è possibile concludere che sui turni interessati è necessario ridurre il tempo di risposta al 90% del valore attuale per migliorare la qualità del servizio.  
  
|Turno, retribuzione e giorno|Qualità del servizio stimata con il tempo di risposta medio corrente|Qualità del servizio stimata con il 90% di riduzione del tempo di risposta|Qualità del servizio stimata con l'80% di riduzione del tempo di risposta|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|Giorno festivo AM|0.165|0,05|0,05|  
|Giorno festivo PM1|0,05|0,05|0,05|  
|Mezzanotte del giorno festivo|0.165|0,05|0,05|  
  
 È possibile creare molte altre query di stima su questo modello. È ad esempio possibile stimare il numero di operatori necessari per garantire un determinato livello di servizio o per rispondere a un determinato numero di chiamate in ingresso. Poiché è possibile includere più output in un modello di regressione logistica, è facile provare a utilizzare variabili indipendenti e risultati diversi senza dover creare molti modelli distinti.  
  
## <a name="remarks"></a>Note  
 I componenti aggiuntivi Data mining per Excel 2007 forniscono procedure guidate di regressione logistica che semplificano la risoluzione di problemi complessi, ad esempio il numero di operatori di livello 2 necessari per migliorare il livello del servizio e raggiungere un livello desiderato per un turno specifico. I componenti aggiuntivi per il data mining sono disponibili gratuitamente per il download e includono procedure guidate basate su algoritmi di regressione logistica o rete neurale. Per ulteriori informazioni, vedere i seguenti collegamenti:  
  
-   [SQL Server 2005 Data Mining componente aggiuntivo per Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx): Ricerca obiettivo e cosa accade se analisi di Scenario  
  
-   [SQL Server 2008 Data Mining componente aggiuntivo per Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790): Ricerca obiettivo, cosa accade se analisi di Scenario e calcolo delle stime  
  
## <a name="conclusion"></a>Conclusione  
 In questa esercitazione si è imparato a creare, personalizzare e interpretare modelli di data mining basati sugli algoritmi Microsoft Neural Network e Microsoft Logistic Regression. Si tratta di tipi di modello sofisticati che consentono una varietà quasi infinita di analisi e pertanto possono essere complessi e difficili da gestire.  
  
 Questi algoritmi consentono tuttavia di scorrere molte combinazioni di fattori e identificare automaticamente le correlazioni maggiori, fornendo il supporto statistico per ottenere informazioni che sarebbe molto difficile individuare tramite l'esplorazione manuale dei dati utilizzando Transact-SQL o PowerPivot.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di query sul modello di regressione logistica](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Algoritmo Microsoft Logistic Regression](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft Neural Network Algorithm](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Esempi di query sul modello di rete neurale](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  

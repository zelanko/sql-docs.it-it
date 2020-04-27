---
title: Creazione di stime per i modelli del Call Center (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63217879"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>Creazione di stime per i modelli Call Center (Esercitazione intermedia sul data mining)
  Dopo aver appreso i concetti di base sulle interazioni tra turni, numero di operatori, chiamate e livello del servizio, è possibile creare alcune query di stima che possono essere utilizzate per l'analisi e la pianificazione aziendali. Verranno innanzitutto create alcune stime del modello esplorativo per testare alcune ipotesi. Verranno quindi create stime bulk utilizzando il modello di regressione logistica.  
  
 Per questa lezione si presuppone che l'utente abbia già acquisito familiarità con il concetto di query di stima.  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>Creazione di stime tramite il modello di rete neurale  
 Nell'esempio seguente viene illustrato come eseguire una stima singleton utilizzando il modello di rete neurale creato per l'esplorazione. Le stime singleton sono una soluzione valida per applicare valori diversi per visualizzarne l'effetto nel modello. In questo scenario si stimerà il livello del servizio per il turno di mezzanotte, senza specificare il giorno della settimana, se sei operatori esperti sono in servizio.  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>Per creare una query singleton utilizzando il modello di rete neurale  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire la soluzione contenente il modello che si desidera utilizzare.  
  
2.  In Progettazione modelli di data mining fare clic sulla scheda **Stima modello di data mining** .  
  
3.  Nel riquadro **modello di data mining** fare clic su **Seleziona modello**.  
  
4.  Nella finestra di dialogo **Seleziona modello di data mining** viene visualizzato un elenco di strutture di data mining. Espandere la struttura di data mining per visualizzare un elenco dei modelli di data mining associati alla struttura.  
  
5.  Espandere la struttura di data mining Call Center Default e selezionare il modello di rete neurale Call Center - LR.  
  
6.  Scegliere **Query singleton** dal menu **Modello di data mining**.  
  
     Viene visualizzata la finestra di dialogo **input query singleton** con le colonne di cui è stato eseguito il mapping alle colonne nel modello di data mining.  
  
7.  Nella finestra di dialogo **input query singleton** fare clic sulla riga per MAIUSC, quindi selezionare *mezzanotte*.  
  
8.  Fare clic sulla riga per gli operatori di LVL 2 `6`, quindi digitare.  
  
9. Nella metà inferiore della scheda **Stima modello di data mining** fare clic sulla prima riga della griglia.  
  
10. Nella colonna **origine** fare clic sulla freccia rivolta verso il basso e selezionare **funzione di stima**. Nella colonna **campo** selezionare **PredictHistogram**.  
  
     Un elenco di argomenti che è possibile utilizzare con questa funzione di stima viene visualizzato automaticamente nella casella **criteri/argomento** .  
  
11. Trascinare la colonna ServiceGrade dall'elenco di colonne nel riquadro **modello di data mining** alla casella **criteri/argomento** .  
  
     Il nome della colonna verrà inserito automaticamente come argomento. È possibile scegliere qualsiasi colonna di attributo stimabile e trascinarla in questa casella di testo.  
  
12. Fare clic sul pulsante **passa alla visualizzazione risultati query**, nell'angolo superiore del generatore di query di stima.  
  
 I risultati previsti contengono i possibili valori stimati per ogni livello del servizio considerando questi input, nonché i valori di supporto e probabilità per ogni stima. È possibile tornare in qualsiasi momento alla visualizzazione di progettazione per modificare gli input o aggiungerne altri.  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>Creazione di stime tramite un modello di regressione logistica  
 Se si conoscono già gli attributi attinenti al problema aziendale, è possibile utilizzare un modello di regressione logistica per stimare l'effetto della modifica di alcuni attributi. La regressione logistica è un metodo statistico comunemente usato per eseguire stime in base alle modifiche nelle variabili indipendenti. Viene ad esempio usato negli scenari finanziari per prevedere il comportamento dei clienti in base ai relativi dati demografici.  
  
 In questa attività viene illustrato come creare un'origine dati che verrà utilizzata per le stime, quindi come eseguire stime per rispondere a diverse domande aziendali.  
  
### <a name="generating-data-used-for-bulk-prediction"></a>Generazione di dati utilizzati per la stima bulk  
 Esistono diversi modi per fornire dati di input: ad esempio, è possibile importare livelli del personale da un foglio di calcolo ed eseguire i dati tramite il modello per stimare la qualità del servizio per il mese successivo.  
  
 In questa lezione si utilizzerà la finestra di progettazione Vista origine dati per creare una query denominata. Questa query denominata è un'istruzione Transact-SQL personalizzata che per ogni turno nella pianificazione calcola il numero massimo di operatori che fanno parte del personale, il numero minimo di chiamate ricevute e il numero medio di problemi generati. Si inseriranno quindi i dati in un modello di data mining per eseguire stime su una serie di date imminenti.  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>Per generare dati di input per una query di stima bulk  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **viste origine dati**, quindi scegliere **nuova vista origine dati**.  
  
2.  Nella creazione guidata vista origine dati selezionare [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] come origine dati, quindi fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione tabelle e viste** fare clic su **Avanti** senza selezionare alcuna tabella.  
  
4.  Nella pagina **Completamento procedura guidata** Digitare il nome `Shifts`.  
  
     Questo nome verrà visualizzato in Esplora soluzioni come nome della vista origine dati.  
  
5.  Fare clic con il pulsante destro del mouse sul riquadro di progettazione vuoto, quindi scegliere **nuova query denominata**.  
  
6.  Nella finestra di dialogo **Crea query denominata** Digitare `Shifts for Call Center`per **nome**.  
  
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
  
8.  Nel riquadro di progettazione fare clic con il pulsante destro del mouse sulla tabella, turni per Call Center e selezionare **Esplora dati** per visualizzare in anteprima i dati restituiti dalla query T-SQL.  
  
9. Fare clic con il pulsante destro del mouse sulla scheda **turni. DSV (progettazione),** quindi scegliere **Salva** per salvare la nuova definizione della vista origine dati.  
  
### <a name="predicting-service-metrics-for-each-shift"></a>Stima delle metriche del servizio per ogni turno  
 Dopo aver generato alcuni valori per ogni turno, tali valori verranno utilizzati come input per il modello di regressione logistica compilato per generare alcune stime che è possibile utilizzare nelle pianificazioni aziendali.  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>Per utilizzare la nuova vista origine dati come di input per una query di stima  
  
1.  In Progettazione modelli di data mining fare clic sulla scheda **Stima modello di data mining** .  
  
2.  Nel riquadro **modello di data mining** fare clic su **Seleziona modello**e scegliere Call Center-LR dall'elenco dei modelli disponibili.  
  
3.  Dal menu **modello di data mining** deselezionare l'opzione **query singleton**. Verrà visualizzato un avviso che indica che gli input della query singleton andranno persi. Fare clic su **OK**.  
  
     La finestra di dialogo **input query singleton** viene sostituita dalla finestra di dialogo **Seleziona tabella/** e di input.  
  
4.  Fare clic su **Seleziona tabella del case**.  
  
5.  Nella finestra di dialogo **Seleziona tabella** , selectShifts dall'elenco di origini dati. Nell'elenco **nome tabella/vista** selezionare turni per Call Center (potrebbe essere selezionato automaticamente), quindi fare clic su **OK.**  
  
     L'area di progettazione **Stima modello di data mining** viene aggiornata per visualizzare i mapping creati in base ai nomi e ai tipi di dati delle colonne nei dati di input e nel modello.  
  
6.  Fare clic con il pulsante destro del mouse su una delle linee di join e scegliere **modifica connessioni**.  
  
     In questa finestra di dialogo è possibile vedere esattamente di quali colonne è stato eseguito il mapping e di quali no. Il modello di data mining contiene le colonne Calls, Orders, IssuesRaised e LvlTwoOperators di cui è possibile eseguire il mapping a qualsiasi aggregazione creata in base a queste colonne nei dati di origine. In questo scenario si eseguirà il mapping alle medie.  
  
7.  Fare clic sulla cella vuota accanto a LevelTwoOperators e selezionare **turni per Call Center. AvgOperators**.  
  
8.  Fare clic sulla cella vuota accanto a chiamate e selezionare **turni per Call Center. AvgCalls**. e quindi fare clic su **OK**.  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>Per creare le stime per ogni turno  
  
1.  Nella griglia nella metà inferiore del **Generatore di query di stima**fare clic sulla cella vuota sotto **origine** e quindi selezionare turni per Call Center.  
  
2.  Nella cella vuota sotto **campo**selezionare MAIUSC.  
  
3.  Fare clic sulla riga vuota successiva nella griglia e ripetere la procedura sopra descritta per aggiungere un'altra riga per WageType.  
  
4.  Fare clic sulla riga vuota successiva nella griglia. Nella colonna **origine** selezionare funzione di **stima**. Nella colonna **campo** selezionare **stima**.  
  
5.  Trascinare la colonna ServiceGrade dal riquadro **modello di data mining** fino alla griglia e nella cella **criteri/argomento** . Nel campo **alias** digitare livello di **servizio stimato**.  
  
6.  Fare clic sulla riga vuota successiva nella griglia. Nella colonna **origine** selezionare funzione di **stima**. Nella colonna **campo** selezionare **PredictProbability**.  
  
7.  Trascinare la colonna ServiceGrade dal riquadro **modello di data mining** fino alla griglia e nella cella **criteri/argomento** . Nel campo **alias** digitare **probabilità**.  
  
8.  Fare clic su **passa alla visualizzazione dei risultati della query** per visualizzare le stime.  
  
 Nella tabella seguente vengono illustrati i risultati dell'esempio per ogni turno.  
  
|Turno|WageType|Livello di servizio stimato|Probabilità|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|giorno festivo|0,165|0,377520666|  
|mezzanotte|giorno festivo|0,105|0,364105573|  
|PM1|giorno festivo|0,165|0,40056055|  
|PM2|giorno festivo|0,165|0,338532973|  
|AM|giorno feriale|0,165|0,370847617|  
|mezzanotte|giorno feriale|0,08|0,352999173|  
|PM1|giorno feriale|0,165|0,317419177|  
|PM2|giorno feriale|0,105|0,311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>Stima dell'effetto del tempo di risposta ridotto sul livello del servizio  
 Sono stati generati alcuni valori medi per ogni turno e tali valori sono stati utilizzati come input per il modello di regressione logistica. Tuttavia, considerato che l'obiettivo aziendale è mantenere la frequenza di abbandono tra 0,00 e 0,05, i risultati non sono incoraggianti.  
  
 Pertanto, in base al modello originale, che mostra un notevole impatto del tempo di risposta sul livello del servizio, il team di gestione decide di eseguire alcune stime per valutare se, riducendo il tempo medio per la risposta alle chiamate, la qualità del servizio può migliorare. È possibile, ad esempio, valutare le conseguenze per i valori del livello di servizio se si riduce il tempo di risposta alle chiamate al 90% o anche all'80% rispetto al tempo di risposta corrente.  
  
 La creazione di una vista origine dati per il calcolo dei tempi di risposta medi per ogni turno e la successiva aggiunta di colonne per il calcolo dell'80 o 90% del tempo medio di risposta sono operazioni semplici. È quindi possibile utilizzare la vista origine dati come input per il modello.  
  
 Anche se qui non sono illustrati i passaggi esatti, nella tabella seguente vengono confrontati gli effetti sul livello di servizio quando si riducono i tempi di risposta all'80 o a 90% di tempi di risposta correnti.  
  
 Da questi risultati è possibile concludere che sui turni interessati è necessario ridurre il tempo di risposta al 90% del valore attuale per migliorare la qualità del servizio.  
  
|Turno, retribuzione e giorno|Qualità del servizio stimata con il tempo di risposta medio corrente|Qualità del servizio stimata con il 90% di riduzione del tempo di risposta|Qualità del servizio stimata con l'80% di riduzione del tempo di risposta|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|Giorno festivo AM|0,165|0.05|0.05|  
|Giorno festivo PM1|0.05|0.05|0.05|  
|Mezzanotte del giorno festivo|0,165|0.05|0.05|  
  
 È possibile creare molte altre query di stima su questo modello. È ad esempio possibile stimare il numero di operatori necessari per garantire un determinato livello di servizio o per rispondere a un determinato numero di chiamate in ingresso. Poiché è possibile includere più output in un modello di regressione logistica, è facile provare a utilizzare variabili indipendenti e risultati diversi senza dover creare molti modelli distinti.  
  
## <a name="remarks"></a>Osservazioni  
 I componenti aggiuntivi Data mining per Excel 2007 forniscono procedure guidate di regressione logistica che semplificano la risoluzione di problemi complessi, ad esempio il numero di operatori di livello 2 necessari per migliorare il livello del servizio e raggiungere un livello desiderato per un turno specifico. I componenti aggiuntivi per il data mining sono disponibili gratuitamente per il download e includono procedure guidate basate su algoritmi di regressione logistica o rete neurale. Per ulteriori informazioni, vedere i seguenti collegamenti:  
  
-   [SQL Server 2005 componenti aggiuntivi Data mining per Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx): ricerca obiettivo e analisi dello scenario What If  
  
-   [SQL Server 2008 componenti aggiuntivi Data mining per Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790): ricerca obiettivo, analisi dello scenario What If e calcolo stime  
  
## <a name="conclusion"></a>Conclusioni  
 In questa esercitazione si è imparato a creare, personalizzare e interpretare modelli di data mining basati sugli algoritmi Microsoft Neural Network e Microsoft Logistic Regression. Si tratta di tipi di modello sofisticati che consentono una varietà quasi infinita di analisi e pertanto possono essere complessi e difficili da gestire.  
  
 Questi algoritmi consentono tuttavia di scorrere molte combinazioni di fattori e identificare automaticamente le correlazioni maggiori, fornendo il supporto statistico per ottenere informazioni che sarebbe molto difficile individuare tramite l'esplorazione manuale dei dati utilizzando Transact-SQL o PowerPivot.  
  
## <a name="see-also"></a>Vedi anche  
 [Esempi di query sul modello di regressione logistica](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Algoritmo di regressione logistica Microsoft](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Algoritmo Microsoft Neural Network](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Esempi di query sul modello di rete neurale](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  

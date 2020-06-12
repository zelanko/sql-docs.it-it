---
title: Aggiunta modello a struttura (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
ms.openlocfilehash: 606d453235529fbfed4dc0f07178ce2ae7132067
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528257"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Aggiunta modello a struttura (componenti aggiuntivi Data mining per Excel)
  ![Pulsante Aggiunta modello a struttura](media/dmc-addmodel.gif "Pulsante Aggiunta modello a struttura")  
  
 Quando si fa clic su **Aggiungi modello a struttura**, viene avviata una procedura guidata che consente di creare un nuovo modello di data mining da utilizzare con una struttura di data mining esistente. Questa opzione è utile perché consente di confrontare i modelli basati sugli stessi dati o di creare modelli personalizzati.  
  
 Se l'istanza di Analysis Services non contiene ancora i dati necessari, utilizzare la procedura guidata [crea struttura di data mining &#40;SQL Server componenti aggiuntivi Data Mining&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) per configurare una struttura di data mining. In alternativa, è possibile avviare una delle modellazioni guidate, quindi aggiungere un nuovo modello alla struttura creata dalla procedura guidata.  
  
 Per creare modelli avanzati utilizzando algoritmi non supportati dalle procedure guidate, creare una struttura di data mining e quindi aggiungere un modello utilizzando l' **Editor avanzato query di data mining**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Aggiungere un nuovo modello a una struttura esistente  
  
1.  Sulla barra multifunzione **data mining** fare clic sulla freccia sotto **Avanzate**, quindi selezionare **Aggiungi modello a struttura**.  
  
2.  Nella finestra di dialogo **Seleziona struttura** scegliere la struttura contenente i dati che si desidera utilizzare, quindi fare clic su **Avanti**.  
  
     **Suggerimento**: se non si è certi della struttura di data mining che contiene i dati necessari, utilizzare la procedura guidata **modello di documento** per visualizzare le colonne e le statistiche di base sui dati.  
  
     Se non è possibile trovare una struttura di data mining, controllare la connessione attualmente in uso. Potrebbe essere necessario aprire una connessione a un server diverso.  
  
3.  Nella finestra di dialogo **Seleziona algoritmo di data** mining scegliere un algoritmo di data mining da utilizzare nel nuovo modello di data mining.  
  
     Si noti che nella finestra di dialogo sono disponibili diverse opzioni che verranno visualizzate nelle procedure guidate. È possibile creare un modello utilizzando qualsiasi algoritmo supportato nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], se i dati sono compatibili.  
  
4.  Si consiglia inoltre di fare clic sul pulsante **parametri** per aprire la finestra di dialogo **parametri algoritmo** e personalizzare i parametri dell'algoritmo. Questa opzione rappresenta la modalità più semplice per creare modelli di data mining personalizzati.  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella finestra di dialogo **Seleziona colonne** esaminare l'elenco di colonne e, se necessario, modificare l'utilizzo delle colonne con uno dei valori seguenti:  
  
    -   **Input**. Indica che nella colonna sono contenute variabili che possono influire sul risultato e che devono essere utilizzate come input per il modello.  
  
    -   **Input e stima**. Indica che i dati devono essere utilizzati come input e che inoltre si desidera eseguire la stima di questi valori.  
  
    -   **Solo stima**. Indica che i dati non devono essere utilizzati come input per il modello.  
  
    -   **Chiave**. A ogni modello deve essere associata almeno una chiave. A seconda del tipo di modello, è possibile che sia presente anche l'opzione per chiavi speciali aggiuntive, ad esempio **SequenceKey** o **TimeKey**.  
  
    -   Non **usare**. Indica che i dati non devono essere utilizzati nel modello, anche se presenti nella struttura.  
  
7.  Fare clic sul pulsante Sfoglia **(...)** per aprire la finestra di dialogo **Imposta flag di modellazione colonna** .  
  
     È opportuno verificare che l'utilizzo di ogni colonna di dati sia appropriato per il modello. Si tratta di un passaggio importante per evitare errori quando si tenta di elaborare il modello.  
  
     Ad esempio, se si riutilizza una struttura creata per un modello di albero delle decisioni e vi si applica l'algoritmo Naïve Bayes, le colonne con il tipo di dati `Numeric` e il tipo di contenuto `Continuous` dovranno essere suddivise o modificate in variabili discrete.  
  
     Se le colonne della struttura non sono applicabili al nuovo algoritmo, è possibile ignorarle selezionando non **utilizzare**.  
  
8.  Nella finestra di dialogo **Imposta flag di modellazione colonna** esaminare o impostare i flag di modellazione, se presenti.  
  
     I flag di modellazione consentono di controllare, tra l'altro, la modalità con cui vengono gestiti i valori Null. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Al termine, fare clic su **OK** per chiudere la finestra di dialogo.  
  
9. Nella finestra di dialogo **fine** Digitare un nome e una descrizione per il nuovo modello di data mining.  
  
     A seconda del tipo di modello compilato, è inoltre possibile che siano disponibili le opzioni seguenti:  
  
    -   Esplorazione del modello di data mining completato dopo la compilazione.  
  
    -   Utilizzo del drill-through dal modello ai dati di origine.  
  
         Per ulteriori informazioni, vedere [drill-through sui modelli di data mining](data-mining/drillthrough-on-mining-models.md).  
  
10. Fare clic su **Fine** per salvare le modifiche. Dopo aver eseguito questa operazione, il nuovo modello viene distribuito nel server e viene elaborato.  
  
### <a name="related-options"></a>Opzioni correlate  
  
|Opzione|Commenti|  
|------------|--------------|  
|Finestra di dialogo **Seleziona struttura o modello**|Scegliere una struttura di data mining esistente da utilizzare come base per la compilazione di un nuovo modello.  La struttura selezionata deve trovarsi nella connessione corrente. In caso contrario, modificare le connessioni utilizzando lo strumento [Connetti a dati di origine &#40;client di data mining per&#41;Excel](connect-to-source-data-data-mining-client-for-excel.md) .|  
|**Selezione algoritmo di data mining** -finestra di dialogo|L'elenco di algoritmi di data mining dipende dal server a cui si è connessi. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce algoritmi diversi nelle versioni Standard ed Enterprise. Inoltre, è possibile che l'amministratore abbia aggiunto algoritmi personalizzati.<br /><br /> Se non è possibile visualizzare alcun algoritmo, verificare di essere connessi a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Parametri dell'algoritmo** Finestra di dialogo|In queste impostazioni è possibile personalizzare ogni algoritmo utilizzando parametri specifici del metodo analitico. È inoltre possibile impostare un valore di inizializzazione per garantire che i risultati del modello possano essere riprodotti in più sessioni di training.<br /><br /> Per ulteriori informazioni, vedere [parametri algoritmo &#40;SQL Server componenti aggiuntivi Data Mining&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Imposta flag di modellazione colonna** Finestra di dialogo|Con i flag di modellazione è possibile migliorare il modello specificando la modalità con cui i dati mancanti devono essere gestiti. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="setting-column-usage"></a><a name="Bkmk_mdlcolumn"></a>Impostazione dell'utilizzo delle colonne  
 Quando si aggiunge un nuovo modello a una struttura di data mining esistente, è necessario specificare in che modo il modello utilizzerà le singole colonne di dati della struttura di data mining. Probabilmente si osserverà che le opzioni di questa procedura guidata sono molto più dettagliate delle opzioni della struttura di data mining. Perché?  
  
 Il motivo è che quando si creano contemporaneamente un modello e una struttura tramite una procedura guidata, molte delle opzioni con cui viene controllata la modalità di utilizzo dei dati da parte dell'algoritmo vengono impostate automaticamente. Tuttavia, quando si aggiunge un nuovo modello a una struttura esistente, è necessario verificare queste opzioni manualmente e specificare se i dati devono essere utilizzati per l'analisi, se il tipo di dati è corretto e così via.  
  
 È possibile che vengano visualizzati messaggi di errore quando si applicano nuovi algoritmi ai dati esistenti. Tuttavia, questi messaggi forniscono in genere informazioni dettagliate sulle correzioni che devono essere apportate per consentire l'elaborazione del modello. Tra i problemi tipici sono inclusi i seguenti:  
  
-   Il modello prevede un tipo di dati diverso rispetto a quello contenuto dalla struttura.  
  
     Alcuni algoritmi possono funzionare solo con i numeri, altri solo con del testo. Se i dati sono di un tipo non corretto per il nuovo modello, potrebbe essere necessario modificare la struttura per consentire l'elaborazione del modello.  
  
-   Nella struttura di data mining non sono inclusi attributi stimabili.  
  
     I modelli di clustering possono essere compilati senza valori stimabili, tuttavia per altri modelli è in genere necessario specificare una singola colonna per la stima.  
  
-   La composizione dei dati non è compatibile con l'algoritmo scelto.  
  
     Per alcuni tipi di analisi sono necessari dati strutturati con attenzione in base a regole univoche, ad esempio i modelli di previsione e i modelli di associazione. È possibile aggiungere facilmente nuovi modelli dello stesso tipo, ad esempio con personalizzazioni, tuttavia i dati potrebbero non funzionare con altri algoritmi.  
  
### <a name="requirements"></a>Requisiti  
 Per creare modelli di data mining, è necessario disporre di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per ulteriori informazioni su come creare o modificare una connessione, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Se non è possibile visualizzare la struttura di data mining desiderata, è possibile che la struttura sia stata salvata in un'istanza o in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] diverso. Per informazioni su come passare a una connessione data mining diversa, vedere [connettersi a un server di data mining](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   

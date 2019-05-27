---
title: Aggiunta modello a struttura (componenti aggiuntivi Data Mining per Excel i dati) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ce68071f27897e181063299e561dfaa7d9f8aab7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062880"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Aggiunta modello a struttura (componenti aggiuntivi Data mining per Excel)
  ![Aggiungere modello di pulsante di struttura](media/dmc-addmodel.gif "aggiunta modello a pulsante struttura")  
  
 Quando fa clic su **aggiunta modello a struttura**, viene avviata una procedura guidata che consente di crea un nuovo modello di data mining da utilizzare con una struttura di data mining esistente. Questa opzione è utile perché consente di confrontare i modelli basati sugli stessi dati o di creare modelli personalizzati.  
  
 Se l'istanza di Analysis Services non contiene già i dati necessari, usare il [Crea struttura di Data Mining &#40;componenti aggiuntivi Data Mining di SQL Server&#41; ](create-mining-structure-sql-server-data-mining-add-ins.md) guidata consente di configurare una struttura di data mining. In alternativa, è possibile avviare una delle modellazioni guidate, quindi aggiungere un nuovo modello alla struttura creata dalla procedura guidata.  
  
 Per creare modelli avanzati con algoritmi non supportati dalle procedure guidate, creare una struttura di data mining e quindi aggiungere un modello utilizzando il **Editor avanzato Query di Data Mining**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Aggiungere un nuovo modello a una struttura esistente  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic sulla freccia sotto **Advanced**e quindi selezionare **aggiunta modello a struttura**.  
  
2.  Nel **Seleziona struttura** finestra di dialogo scegliere la struttura che contiene i dati da usare e quindi fare clic su **successivo**.  
  
     **Suggerimento**: Se non si conosce la struttura di data mining contiene i dati necessari, usare il **modello di documento** guidata consente di visualizzare le colonne e le statistiche di base sui dati.  
  
     Se non è possibile trovare una struttura di data mining, controllare la connessione attualmente in uso. Potrebbe essere necessario aprire una connessione a un server diverso.  
  
3.  Nel **algoritmo di Data Mining selezionare** finestra di dialogo, scegliere un algoritmo di data mining da utilizzare nel nuovo modello di data mining.  
  
     Si noti che la finestra di dialogo offre molte più opzioni rispetto a verrà visualizzato nelle procedure guidate. È possibile creare un modello utilizzando qualsiasi algoritmo supportato nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], se i dati sono compatibili.  
  
4.  È consigliabile selezionare anche il **parametri** per aprire il **i parametri dell'algoritmo** finestra di dialogo casella e personalizzare i parametri dell'algoritmo. Questa opzione rappresenta la modalità più semplice per creare modelli di data mining personalizzati.  
  
5.  Scegliere **Avanti**.  
  
6.  Nel **Seleziona colonne** finestra di dialogo, rivedere l'elenco di colonne e se necessario, modificare l'utilizzo delle colonne a uno dei valori seguenti:  
  
    -   **Input**. Indica che nella colonna sono contenute variabili che possono influire sul risultato e che devono essere utilizzate come input per il modello.  
  
    -   **Input e stima**. Indica che i dati devono essere utilizzati come input e che inoltre si desidera eseguire la stima di questi valori.  
  
    -   **Solo stima**. Indica che i dati non devono essere utilizzati come input per il modello.  
  
    -   **Key**. A ogni modello deve essere associata almeno una chiave. A seconda del tipo di modello, potrebbe anche essere l'opzione per chiavi speciali aggiuntive, ad esempio la **SequenceKey** oppure **TimeKey**.  
  
    -   **Non usare**. Indica che i dati non devono essere utilizzati nel modello, anche se presenti nella struttura.  
  
7.  Fare clic su Sfoglia **(...)**  per aprire la **imposta flag di modellazione colonna** nella finestra di dialogo.  
  
     È opportuno verificare che l'utilizzo di ogni colonna di dati sia appropriato per il modello. Si tratta di un passaggio importante per evitare errori quando si tenta di elaborare il modello.  
  
     Ad esempio, se si riutilizza una struttura creata per un modello di albero delle decisioni e vi si applica l'algoritmo Naïve Bayes, le colonne con il tipo di dati `Numeric` e il tipo di contenuto `Continuous` dovranno essere suddivise o modificate in variabili discrete.  
  
     Se le colonne della struttura non sono applicabili per il nuovo algoritmo, è possibile ignorarle selezionando **non usare**.  
  
8.  Nel **imposta flag di modellazione colonna** nella finestra di dialogo, rivedere o impostare i flag di modellazione, se presente.  
  
     I flag di modellazione consentono di controllare, tra l'altro, la modalità con cui vengono gestiti i valori Null. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Fare clic su **OK** al termine per chiudere la finestra di dialogo.  
  
9. Nel **fine** finestra di dialogo digitare un nome e una descrizione per il nuovo modello di data mining.  
  
     A seconda del tipo di modello compilato, è inoltre possibile che siano disponibili le opzioni seguenti:  
  
    -   Esplorazione del modello di data mining completato dopo la compilazione.  
  
    -   Utilizzo del drill-through dal modello ai dati di origine.  
  
         Per altre informazioni, vedere [drill-through sui modelli di Data Mining](data-mining/drillthrough-on-mining-models.md).  
  
10. Fare clic su **fine** per salvare le modifiche. Dopo aver eseguito questa operazione, il nuovo modello viene distribuito nel server e viene elaborato.  
  
### <a name="related-options"></a>Opzioni correlate  
  
|Opzione|Commenti|  
|------------|--------------|  
|**Selezione struttura o modello** nella finestra di dialogo|Scegliere una struttura di data mining esistente da utilizzare come base per la compilazione di un nuovo modello.  La struttura selezionata deve trovarsi nella connessione corrente. In caso contrario, modificare le connessioni con il [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41; ](connect-to-source-data-data-mining-client-for-excel.md) dello strumento.|  
|**Selezione algoritmo di Data Mining** della finestra di dialogo|L'elenco di algoritmi di data mining dipende dal server a cui si è connessi. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce algoritmi diversi nelle versioni Standard ed Enterprise. Inoltre, è possibile che l'amministratore abbia aggiunto algoritmi personalizzati.<br /><br /> Se non è possibile visualizzare tutti gli algoritmi, verificare di essere connessi a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|**I parametri dell'algoritmo** nella finestra di dialogo|In queste impostazioni è possibile personalizzare ogni algoritmo utilizzando parametri specifici del metodo analitico. È inoltre possibile impostare un valore di inizializzazione per garantire che i risultati del modello possano essere riprodotti in più sessioni di training.<br /><br /> Per altre informazioni, vedere [i parametri dell'algoritmo &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Imposta flag di modellazione colonna** nella finestra di dialogo|Con i flag di modellazione è possibile migliorare il modello specificando la modalità con cui i dati mancanti devono essere gestiti. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="Bkmk_mdlcolumn"></a> Impostazione utilizzo colonne  
 Quando si aggiunge un nuovo modello a una struttura di data mining esistente, è necessario specificare in che modo il modello utilizzerà le singole colonne di dati della struttura di data mining. Probabilmente si osserverà che le opzioni in questa procedura guidata sono molto più dettagliate rispetto alle opzioni nella struttura di data mining. Per quale motivo?  
  
 Il motivo è che quando si creano contemporaneamente un modello e una struttura tramite una procedura guidata, molte delle opzioni con cui viene controllata la modalità di utilizzo dei dati da parte dell'algoritmo vengono impostate automaticamente. Tuttavia, quando si aggiunge un nuovo modello a una struttura esistente, è necessario verificare queste opzioni manualmente e specificare se i dati devono essere utilizzati per l'analisi, se il tipo di dati è corretto e così via.  
  
 È possibile che vengano visualizzati messaggi di errore quando si applicano nuovi algoritmi ai dati esistenti. Tuttavia, questi messaggi forniscono in genere informazioni dettagliate sulle correzioni che devono essere apportate per consentire l'elaborazione del modello. Tra i problemi tipici sono inclusi i seguenti:  
  
-   Il modello prevede un tipo di dati diverso rispetto a quello contenuto dalla struttura.  
  
     Alcuni algoritmi possono funzionare solo con i numeri, altri solo con del testo. Se i dati sono di un tipo non corretto per il nuovo modello, potrebbe essere necessario modificare la struttura per consentire l'elaborazione del modello.  
  
-   Nella struttura di data mining non sono inclusi attributi stimabili.  
  
     I modelli di clustering possono essere compilati senza valori stimabili, tuttavia per altri modelli è in genere necessario specificare una singola colonna per la stima.  
  
-   La composizione dei dati è incompatibile con l'algoritmo scelto.  
  
     Per alcuni tipi di analisi sono necessari dati strutturati con attenzione in base a regole univoche, ad esempio i modelli di previsione e i modelli di associazione. È possibile aggiungere facilmente nuovi modelli dello stesso tipo, ad esempio con personalizzazioni, tuttavia i dati potrebbero non funzionare con altri algoritmi.  
  
### <a name="requirements"></a>Requisiti  
 Per creare modelli di data mining, è necessario disporre di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per altre informazioni su come creare o modificare una connessione, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Se non è possibile visualizzare la struttura di data mining desiderata, è possibile che la struttura sia stata salvata in un'istanza o in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] diverso. Per informazioni sulla modifica di una connessione di data mining di dati diversi, vedere [Connetti al Server di Data Mining](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   

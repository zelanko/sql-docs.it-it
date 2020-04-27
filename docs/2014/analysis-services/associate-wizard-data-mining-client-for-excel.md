---
title: Procedura guidata associazione (client di data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- nested tables, in association models
- association [data mining]
ms.assetid: 4db6462f-93c7-443f-8ff7-39474dc7029e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15a86cc55e67b2000eabee62d02fa04de4874f59
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062310"
---
# <a name="associate-wizard-data-mining-client-for-excel"></a>Procedura guidata Associazione (client di data mining per Excel)
  ![Procedura guidata Associazione sulla barra multifunzione Data mining](media/dmc-associate.gif "Procedura guidata Associazione sulla barra multifunzione Data mining")  
  
 La procedura guidata Associazione consente di creare un modello di data mining utilizzando l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules. Questi modelli di data mining sono particolarmente utili per la creazione di *sistemi di raccomandazione*.  
  
 L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules esegue l'analisi di un set di dati costituito da transazioni o eventi e trova le combinazioni che sono di frequente abbinate. Potrebbero esistere molte migliaia di combinazioni, ma l'algoritmo può essere personalizzato per trovarne di più o di meno e conservare solo le combinazioni più probabili.  
  
 È possibile applicare l'analisi di associazione a molti problemi. L'applicazione più comune di questo metodo è Market basket analysis, che trova singoli prodotti acquistati spesso insieme. È quindi possibile utilizzare tali informazioni per consigliare prodotti ai clienti in base agli elementi che hanno già acquistato.  
  
## <a name="using-the-associate-wizard"></a>Utilizzo della procedura guidata Associazione  
  
1.  Sulla barra multifunzione **data mining** fare clic su **associa**.  
  
2.  Nella pagina **selezione dati di origine** scegliere una tabella o un intervallo di dati di Excel e fare clic su **Avanti**.  
  
     La cartella di lavoro dei dati di esempio contiene un esempio, nella scheda Associazione, di come i dati delle transazioni vengono in genere disposti se, ad esempio, sono presenti più prodotti in ogni transazione o più record di acquisto per ogni cliente che si desidera analizzare.  
  
     Se si desidera utilizzare dati esterni per compilare un modello di associazione utilizzando la procedura guidata associazione, è prima necessario aggiungere i dati a Excel e rendere *Flat* i dati. Per ulteriori informazioni sulla preparazione dei dati per la modellazione dell'associazione, vedere [tabelle nidificate &#40;Analysis Services-Data Mining&#41;](data-mining/nested-tables-analysis-services-data-mining.md), in documentazione online di SQL Server.  
  
3.  Nella pagina **associazione** scegliere la colonna che identifica la transazione.  
  
     Per i modelli Market Basket, questo identificatore rappresenta l'unità che si desidera modellare. Si desidera analizzare gli elementi che singoli clienti hanno acquistato nel corso del tempo o si desidera analizzare molte transazioni che interessano più clienti? Nel primo caso, scegliere l'ID cliente; nel secondo caso, scegliere l'ordine di acquisto o un altro ID transazione  
  
4.  Per **elemento**selezionare la colonna che contiene gli elementi tra cui è necessario trovare le associazioni.  
  
     Ad esempio, in un modello Market Basket, scegliere un campo dei prodotti per analizzare i prodotti acquistati spesso insieme. Se è presente un numero di singoli prodotti troppo elevato per garantire un'efficiente correlazione, è possibile scegliere un campo relativo a una categoria o sottocategoria di prodotto.  
  
5.  Nelle **soglie**è possibile impostare valori che controllano o influiscono sull'output del modello:  
  
    -   **Supporto minimo.** Specifica il numero di volte che un gruppo di elementi deve essere presente per essere considerato importante. Verranno ignorate dall'algoritmo tutte le eventuali combinazioni di elementi che non soddisfano questo criterio. Ad esempio, potrebbe essere necessario visualizzare solo i set di elementi in cui gli elementi risultavano abbinati almeno 10 volte complessivamente.  
  
    -   **Probabilità della regola minima**. Specifica il valore di probabilità minima richiesto per il salvataggio di una regola. L'intero set di dati viene analizzato per trovare tutte le combinazioni e quindi viene calcolata la probabilità. Se si imposta un valore di soglia basso, la procedura guidata potrebbe associare elementi con correlazioni deboli. Se il valore di soglia è troppo alto, invece, alcune associazioni potrebbero essere omesse a causa di dati di supporto insufficienti.  
  
     In generale, la modifica di questi valori ha gli effetti seguenti:  
  
    -   Diminuendo il valore di supporto, aumenta il numero di combinazioni individuate.  
  
    -   Diminuendo il supporto massimo, vengono esclusi tramite filtro gli elementi con una frequenza di occorrenza elevata e pertanto poco significativi.  
  
    -   Diminuendo la probabilità di una regola, si riducono i requisiti che una combinazione deve soddisfare per essere considerata importante nel contesto del set di dati complessivo.  
  
     **Suggerimento:** È consigliabile creare più modelli di data mining utilizzando combinazioni diverse di supporto e probabilità. Per tenere traccia delle impostazioni utilizzate per ogni modello, è possibile utilizzare la procedura guidata **modello di documento** , disponibile nel client di data mining per Excel, e utilizzare l'opzione report **dettagliato** . Per ulteriori informazioni, vedere la documentazione relativa ai [modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md).  
  
6.  Facoltativamente, fare clic su **parametri** per modificare i parametri dell'algoritmo e personalizzare il comportamento del modello di data mining.  
  
     La finestra di dialogo Parametri algoritmo include tutti i parametri impostati nella procedura guidata, nonché alcuni utilizzati meno di frequente, ad esempio MAXIMUM_SUPPORT. Per informazioni sull'utilizzo di questi parametri, vedere [riferimento tecnico per l'algoritmo Microsoft Association](data-mining/microsoft-association-algorithm-technical-reference.md).  
  
7.  Nella pagina **fine** Digitare un nome univoco per il set di dati e il modello.  
  
8.  In **Opzioni**è possibile definire il modo in cui si desidera utilizzare il modello dopo che è stato completato:  
  
    -   **Sfoglia**.  Quando il modello è pronto, tramite la procedura guidata viene aperta una finestra nella quale vengono visualizzati le regole, i set di elementi e un grafico della rete di dipendenze che illustra le associazioni.  
  
         Per ulteriori informazioni su come interpretare i dati nel Visualizzatore modello di associazione, vedere [esplorazione di un modello Association Rules](browsing-an-association-rules-model.md).  
  
    -   **Abilitare il drill-through**. Selezionare questa opzione per accedere ai dati sottostanti, tramite il modello.  
  
         Il drill-through è utile, ad esempio, se si desidera fare clic su un set di elementi specifico e visualizzare i dati di origine.  
  
    -   **Usa modello temporaneo**. Selezionare questa opzione se non si desidera che il modello venga salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
9. Tramite la procedura guidata vengono analizzate tutte le possibili combinazioni e viene creato un report contenente i set di elementi e le regole.  
  
## <a name="more-about-association-models"></a>Ulteriori informazioni sui modelli di associazione  
 L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules esamina il set di dati di training per individuare gli elementi che compaiono insieme in una transazione. Ogni gruppo di elementi costituisce un *set di elementi*. Tramite l'algoritmo viene quindi contato quante volte è presente ogni set di elementi e viene calcolata l'importanza relativa di ogni set di elementi in tutte le transazioni.  
  
 L'algoritmo utilizza queste informazioni sui set di elementi per generare regole che possono essere utilizzate per stimare associazioni o generare indicazioni. Una regola potrebbe ad esempio indicare che se l'utente ha acquistato un libro di Autore 1 e un libro di Autore 2, è probabile che acquisti anche un libro di Autore 3. A ogni indicazione viene assegnata una probabilità basata sul livello di attendibilità delle associazioni.  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata Associazione, è necessario disporre di una connessione a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 I dati di origine devono essere organizzati come una tabella di transazioni e includere una colonna che contiene l'identificatore della transazione. Tale colonna consente di identificare ogni gruppo di elementi. La colonna delle transazioni deve essere collegata con una relazione uno-a-molti a una seconda colonna contenente l'ID degli elementi, nella quale vengono archiviati i nomi o i numeri di ID dei singoli elementi nel gruppo.  
  
 Per chiarire questi concetti può essere utile ricorrere all'esempio di un carrello acquisti. Se si assegna un ID al carrello acquisti, l'ID del carrello acquisti funge da identificatore della transazione. Ogni elemento nel carrello acquisti, ad esempio un libro o un DVD, è un membro della transazione. L'algoritmo di associazione consente di esaminare gli elementi in più transazioni, ad esempio per individuare il numero di occorrenze degli elementi libro e DVD all'interno di una singola transazione.  
  
 I dati di origine devono essere ordinati in base alla colonna di identificazione delle transazioni.  
  
## <a name="see-also"></a>Vedi anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Esplorazione di un modello Association Rules](browsing-an-association-rules-model.md)   
 [Shopping Basket Analysis &#40;Table AnalysisTools per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)   
 [Diagramma della rete di dipendenze procedura dettagliata &#40;componenti aggiuntivi Data mining&#41;](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
  

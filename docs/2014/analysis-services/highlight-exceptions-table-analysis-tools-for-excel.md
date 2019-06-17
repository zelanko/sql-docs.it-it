---
title: Evidenzia eccezioni (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- highlight exceptions
ms.assetid: d90a12f8-7bc3-4fdb-95a1-7c89058f0d9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 18bf54b7b97598c6c61d7e282ad5791d926cc25a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080760"
---
# <a name="highlight-exceptions-table-analysis-tools-for-excel"></a>Evidenzia eccezioni (Strumenti di analisi tabelle per Excel)
  ![Pulsante Evidenzia eccezioni sulla barra multifunzione](media/tat-highlightex.gif "pulsante Evidenzia eccezioni sulla barra multifunzione")  
  
 Talvolta i dati potrebbero contenere valori particolari. Potrebbe, ad esempio, essere indicata un'età di 5 anni per un proprietario di un immobile. Questi valori, spesso chiamati *outlier*, potrebbero essere errati a causa di un errore di input dei dati o potrebbero indicare tendenze anomale. In entrambi i casi, le eccezioni possono influire negativamente sulla qualità dell'analisi. Il **evidenzia eccezioni** strumento consente di trovare questi valori e controllarle per un'ulteriore azione.  
  
 Il **evidenzia eccezioni** possibile utilizzare lo strumento con l'intero intervallo di dati in una tabella di dati di Excel, oppure è possibile selezionare solo alcune colonne. È inoltre possibile modificare il valore di soglia che determina l'intervallo di variabilità dei dati, in modo da individuare un numero maggiore o minore di eccezioni.  
  
 Al termine dell'analisi da parte dello strumento, viene creato un nuovo foglio di lavoro contenente un report di riepilogo del numero di outlier individuati in ogni colonna analizzata. Lo strumento evidenzia inoltre le eccezioni nella tabella dati originale. Poiché lo strumento analizza le tendenze generali, potrebbe considerare normale la maggior parte dei valori in una riga ed evidenziare una sola cella in tale riga. Nell'esempio proprietario di immobile citato sopra, solo il **età** colonna potrebbe essere evidenziata.  
  
 È inoltre possibile modificare il **soglia di eccezione** valore nel **Report di riepilogo**. Questo valore indica la probabilità che una determinata cella contenga un valore anomalo. Pertanto, se si aumenta il valore, verrà evidenziato un minor numero di valori come outlier. Viceversa, con la diminuzione del valore verrà evidenziato un numero maggiore di celle.  
  
## <a name="using-the-highlight-exceptions-tool"></a>Utilizzo dello strumento Evidenzia eccezioni  
  
1.  Aprire una tabella di Excel e fare clic su **evidenzia eccezioni**.  
  
2.  Specificare le colonne da analizzare.  
  
3.  Fare clic su **Esegui**.  
  
4.  Aprire il foglio di lavoro denominato \<nome tabella > Outlier per visualizzare un riepilogo degli outlier che sono stati trovati.  
  
5.  Per modificare il numero di celle evidenziate, fare clic sulla freccia e freccia in giù nella **soglia di eccezione** riga della **Report eccezioni evidenziate**.  
  
### <a name="requirements"></a>Requisiti  
 È possibile includere colonne che non contengono valori errati, se tali valori contengono informazioni potenzialmente utili per la stima di altre righe. È tuttavia necessario deselezionare le colonne che contengono numerosi valori mancanti o zero.  
  
 Poiché tutte le colonne selezionate sono utilizzate per creare un modello generale, è necessario evitare di utilizzare colonne di input con informazioni insufficienti, come nei casi seguenti:  
  
-   Colonne che contengono valori univoci, ad esempio ID.  
  
-   Colonne che contengono una percentuale elevata di valori errati.  
  
-   Colonne con numerosi valori mancanti.  
  
     In alcuni casi può essere utile includere colonne di input con numerosi valori mancanti. Se ad esempio il valore del campo dell'indirizzo è sempre mancante quando il cliente acquista tramite un rivenditore, l'algoritmo di data mining può utilizzare queste informazioni per identificare altri clienti simili. È necessario determinare caso per caso se i dati sono mancanti a causa di un'omissione o se lo stato mancante è significativo.  
  
-   Colonne che probabilmente non sono utili per la creazione di un modello. Una colonna con lo stesso valore in ogni riga non fornisce ad esempio informazioni utili per la creazione di modelli.  
  
## <a name="understanding-the-highlight-exceptions-report"></a>Informazioni sul report dello strumento Evidenzia eccezioni  
 Quando fa clic su **eseguire**, lo strumento esegue tre operazioni:  
  
-   Creazione di una struttura di data mining in base ai dati correnti nella tabella.  
  
-   Creazione di un nuovo modello di data mining utilizzando l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering.  
  
-   Creazione di una query di stima basata sui modelli per determinare se eventuali valori nel foglio di lavoro sono improbabili.  
  
 Il valore di soglia iniziale per le eccezioni è sempre 75 e indica che l'algoritmo ha calcolato una probabilità del 75% che i dati evidenziati siano errati. Questo valore di soglia viene impostato automaticamente per il passaggio di analisi iniziale, ma è possibile modificare il valore nel report.  
  
 Il **evidenzia eccezioni** strumento Evidenzia le celle della tabella dati originale sospetti. Un'evidenziazione scura indica che la riga richiede attenzione. Un'evidenziazione chiara indica che il valore nella cella specifica è stato identificato come sospetto. Se si modifica il valore di soglia per le eccezioni, i valori evidenziati cambiano di conseguenza.  
  
 Nel grafico di riepilogo viene indicato il numero di celle in ogni colonna con valori superiori alla soglia specificata.  
  
## <a name="related-tools"></a>Strumenti correlati  
 Durante le operazioni di pulizia o verifica dei dati in preparazione dei processi di data mining, è inoltre possibile provare le funzionalità di esplorazione dei dati disponibili nel client di data mining per Excel. Questo componente aggiuntivo include ulteriori strumenti avanzati per la ricerca di outlier, la modifica delle etichette dei dati o la visualizzazione della distribuzione dei dati. Per altre informazioni sugli strumenti di esplorazione dei dati nel Client di Data Mining per Excel, vedere [esplorazione e pulizia dei dati](exploring-and-cleaning-data.md).  
  
 Il **evidenzia eccezioni** dello strumento viene utilizzato il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Clustering. Un modello di clustering consente di rilevare gruppi di righe che condividono caratteristiche simili. Il Client di Data Mining per Excel offre una **esplorare** finestra in cui vengono utilizzati grafici e profili delle caratteristiche per consentire l'esplorazione di modelli di data mining creati con l'algoritmo clustering. Per informazioni su come selezionare il modello di clustering creato per il **evidenzia eccezioni** dello strumento, vedere [Esplora modello (Client Data Mining per Excel)](highlight-exceptions-table-analysis-tools-for-excel.md).  
  
 Per ulteriori informazioni sull'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering, vedere l'argomento "Algoritmo Microsoft Clustering" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  

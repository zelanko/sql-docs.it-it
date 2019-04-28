---
title: Scelta di un modello | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d91e282ebfe0299fd6015530e8af1b6d10e6547
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681098"
---
# <a name="choosing-a-model"></a>Scelta di un modello
  **Algoritmo di data mining:** Modelli di data mining *algoritmo* è il meccanismo che consente di creare modelli dai dati. L'algoritmo definisce come vengono conteggiati i dati, come vengono derivate le relazioni e come vengono archiviati i modelli. La scelta di un algoritmo dipende parzialmente dal tipo di dati che si desidera analizzare. Alcuni algoritmi, ad esempio, possono essere utilizzati solo con numeri continui, mentre altri sono più adatti ad essere utilizzati con un numero limitato di valori distinct.  
  
 **Modello di data mining:** Il risultato dell'analisi dei dati tramite un algoritmo viene salvato un *modello di data mining*. Un modello di data mining è una raccolta di regole, statistiche e modelli. Il *contenuto* del modello di data mining dipende dall'algoritmo utilizzato per elaborare i dati, ma possono includere quanto segue:  
  
-   Regole if-then che descrivono in che modo i prodotti vengono raggruppati in una transazione.  
  
-   Un albero delle decisioni in cui sono tracciati i percorsi che portano a un risultato, con le probabilità di occorrenza di ciascun percorso.  
  
-   Un modello matematico con equazioni per il modello nel suo complesso o per i segmenti del modello.  
  
-   Raccolte di elementi simili (chiamati *cluster* oppure *segmenti*) che sono definiti dalle caratteristiche che condividono e da un punteggio di somiglianza.  
  
-   *I nodi* in una rete, collegata da *bordi*. I nodi rappresentano elementi o gruppi di elementi. Ai bordi sono assegnati dei punteggi a seconda della forza delle relazioni tra i nodi.  
  
 **Usando il modello:** Dopo aver creato un modello, è possibile utilizzare i visualizzatori forniti per esplorarlo oppure è possibile creare una query sul modello. È possibile utilizzare le query per:  
  
-   Stimare valori futuri.  
  
-   Generare un set di prodotti correlati o di prodotti consigliati.  
  
-   Restituire regole, modelli o formule nel modello.  
  
-   Ottenere metadati dal modello.  
  
-   Fornire punteggi di supporto e di probabilità per tutte o alcune stime.  
  
## <a name="types-of-machine-learning-algorithms"></a>Tipi di algoritmi di apprendimento automatico  
 Poiché tipi differenti di algoritmi utilizzano i dati in modo diverso, quando si crea un modello è necessario selezionare l'algoritmo appropriato per gli obiettivi prefissati e per i dati che si desidera analizzare.  
  
 I componenti aggiuntivi Data mining per Excel includono i seguenti tipi diffusi di algoritmi:  
  
-   *Gli algoritmi di classificazione*.  
  
     Consentono di stimare una o più variabili discrete, in base agli altri attributi del set di dati.  
  
-   *Algoritmi di regressione*  
  
     Consentono di stimare una o più variabili continue, ad esempio profitto o perdita, in base ad altri attributi del set di dati.  
  
-   *Algoritmi di segmentazione*  
  
     Consentono di dividere i dati in gruppi, o cluster, di elementi con proprietà simili.  
  
-   *Algoritmi di associazione*  
  
     Consentono di trovare le correlazioni tra attributi diversi in un set di dati. Questo è il tipo di algoritmo più comunemente utilizzato per la creazione di regole di associazione. È possibile utilizzare le regole di associazione in un'analisi di tipo Market basket analysis.  
  
-   *Algoritmi di analisi delle sequenze*  
  
     Consentono di riepilogare le sequenze o gli episodi frequenti nei dati, ad esempio i percorsi seguiti dagli utenti per l'esplorazione di un sito Web.  
  
 Gli algoritmi utilizzati dai componenti aggiuntivi Data mining di SQL Server per Office sono basati sugli algoritmi disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile usare gli algoritmi di terze parti conformi con la specifica OLE DB per Data Mining, anche se l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a cui è connessi è stato configurato per consentire gli algoritmi di terze parti.  
  
## <a name="requirements"></a>Requisiti  
 Ciascun algoritmo differisce nel genere di dati con cui può essere utilizzato.  
  
-   Un modello di regressione lineare può modellare solo valori numerici. Sia le variabili di input che i risultati di destinazione devono essere tipi di numeri continui. Utilizzare un albero delle decisioni o un modello di stima se occorre combinare insieme variabili continue e discrete.  
  
-   Un modello Naïve Bayes richiede che tutti i numeri siano suddivisi. Se si utilizza una delle procedure guidate basate su questo algoritmo, la suddivisione viene effettuata automaticamente.  
  
-   Un albero delle decisioni può contenere sia variabili discrete sia variabili continue. Tuttavia, i numeri verranno suddivisi automaticamente in base alle divisioni nell'albero.  
  
-   Le reti neurali e i modelli di regressione logica suddividono automaticamente i numeri utilizzati come risultati o come variabili di input. Se si desidera raggruppare i numeri secondo altri criteri, utilizzare lo strumento Modifica etichette per creare i raggruppamenti prima di creare il modello. Ad esempio, è possibile raggruppare valori in un' **età** colonna (10 e 20, 21-30 e così via), anziché i raggruppamenti statisticamente significativi trovati dal modello (un esempio potrebbe essere fascia di età 35,6-41,8).  
  
-   Un modello di associazione richiede che i dati siano raggruppati in transazioni, ognuna facente riferimento a più elementi o righe. Se si usa la [associare guidata &#40;Client di Data Mining per Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) guidata o il [market Basket Analysis &#40;strumenti di analisi tabelle per Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) strumento, i dati è opportuno prevedere come illustrato nella **associare** scheda della cartella di lavoro di esempio.  
  
     Se si desidera utilizzare tabelle nidificate in un'origine dati esterna, è necessario usare il [modellazione avanzata &#40;componenti aggiuntivi di Data Mining per Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) modellazione opzioni per creare una struttura di data mining e un modello di data mining che viene salvato nel server. In Excel non sono supportate le tabelle nidificate.  
  
## <a name="feature-selection"></a>Selezione caratteristiche  
 A seconda del set di dati, l'algoritmo potrebbe applicare *selezione delle caratteristiche*, per eliminare le colonne inutili e determinare quali colonne di dati sono statisticamente significative rispetto al risultato.  
  
 Ogni algoritmo utilizza metodi leggermente diversi di selezione delle funzionalità (come l'entropia o vari punteggi informativi) per determinare le tendenze importanti e le differenze che possono essere ignorate.  
  
 Nei componenti aggiuntivi Data Mining per Excel, la selezione della funzionalità viene applicata automaticamente utilizzando un metodo di assegnazione del punteggio adatto a ciascun algoritmo. Se si desidera influire sui risultati della selezione di funzionalità, utilizzare le procedure guidate nel **Data Mining** sulla barra multifunzione e fare clic su **avanzate** per impostare i parametri usando la **i parametri dell'algoritmo**finestra di dialogo.  
  
 Per un elenco di selezione della funzionalità i metodi utilizzati da ciascun algoritmo vedere l'argomento sul [Selezione funzionalità &#40;Data Mining&#41; ](data-mining/feature-selection-data-mining.md) nella documentazione Online di SQL Server.  
  
## <a name="list-of-supported-algorithms"></a>Elenco degli algoritmi supportati  
 I seguenti algoritmi sono forniti per impostazione predefinita.  
  
|Nome algoritmo|Descrizione|Campo di utilizzo|  
|--------------------|-----------------|-------------|  
|Microsoft Association Rules|Consente di compilare regole che descrivono gli elementi che hanno maggiore probabilità di comparire insieme in una transazione.|[Procedura guidata associazione &#40;Client di Data Mining per Excel&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [Market Basket Analysis &#40;strumenti di analisi di tabelle per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft Clustering|Consente di identificare in un set di dati le relazioni che non è possibile derivare in modo logico tramite l'osservazione casuale. L'algoritmo utilizza tecniche iterative per raggruppare i record in cluster con caratteristiche simili.|[Rileva categorie &#40;strumenti di analisi tabelle per Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [Creazione guidata del cluster &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft Decision Trees|Consente di eseguire stime in base alle relazioni esistenti tra le colonne nel set di dati e di modellare le relazioni come serie di divisioni su valori specifici, rappresentate in una struttura ad albero.<br /><br /> Questo algoritmo supporta la stima sia di attributi discreti che di attributi continui.|[Procedura guidata classificazione &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [Procedura guidata stima &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft Linear Regression|Se esiste una dipendenza lineare tra la variabile di destinazione e le variabili esaminate, consente di individuare la relazione più efficiente tra la destinazione e i relativi input.<br /><br /> Questo algoritmo supporta la stima di attributi continui.|Questo algoritmo è disponibile in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nei componenti aggiuntivi Data mining per Office è possibile creare un modello che utilizza questo algoritmo creando una struttura, quindi aggiungendo manualmente un modello.<br /><br /> Per altre informazioni, vedere [modellazione avanzata &#40;aggiuntivi di Data Mining per Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Microsoft Logistic Regression|Consente di analizzare i fattori che contribuiscono al raggiungimento di un risultato limitato a due valori, in genere il verificarsi o il non verificarsi di un evento.<br /><br /> Questo algoritmo supporta la stima sia di attributi discreti che di attributi continui.|[Estendi da esempio &#40;strumenti di analisi tabelle per Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [Ricerca obiettivo &#40;strumenti di analisi tabelle per Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Scenario di simulazione &#40;strumenti di analisi tabelle per Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Calcolo stime &#40;strumenti di analisi tabelle per Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft Naive Bayes|Consente di individuare la probabilità che esista una relazione tra tutte le colonne di input e stimabili. Questo algoritmo è utile per generare rapidamente modelli di data mining per l'individuazione di relazioni.<br /><br /> Sono supportati solo attributi discreti o discretizzati.<br /><br /> Tutti gli attributi di input vengono considerati indipendenti.|[Analizza fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Microsoft Neural Network|Consente di analizzare dati di input complessi oppure problemi aziendali per i quali è disponibile una quantità significativa di dati di training, ma non è possibile derivare facilmente regole specifiche tramite altri algoritmi.<br /><br /> Questo algoritmo supporta la stima di più attributi.<br /><br /> È possibile utilizzare questo algoritmo per la classificazione di attributi discreti e la regressione di attributi continui.|Questo algoritmo è disponibile in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nei componenti aggiuntivi Data mining per Office è possibile creare un modello che utilizza questo algoritmo creando una struttura, quindi aggiungendo manualmente un modello.<br /><br /> Per altre informazioni, vedere [modellazione avanzata &#40;aggiuntivi di Data Mining per Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Microsoft Sequence Clustering|Consente di identificare i cluster di eventi ordinati in modo analogo in una sequenza.<br /><br /> Offre una combinazione delle funzionalità di clustering e analisi delle sequenze.|Questo algoritmo è disponibile solo in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Tuttavia, nei componenti aggiuntivi Data mining per Office è possibile creare un modello che utilizza questo algoritmo creando una struttura, quindi aggiungendo manualmente un modello.<br /><br /> Per altre informazioni, vedere [modellazione avanzata &#40;aggiuntivi di Data Mining per Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Microsoft Time Series|Consente di analizzare dati temporali mediante un albero delle decisioni lineare.<br /><br /> È possibile utilizzare modelli per stimare valori futuri nelle serie temporali.|[Prevedere la &#40;strumenti di analisi tabelle per Excel&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [Procedura guidata previsione &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi inclusi nei componenti aggiuntivi Data mining per Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  

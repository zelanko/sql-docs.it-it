---
title: Visualizzare un modello usando il visualizzatore Microsoft Association Rules | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7c3764d18d26d739023bbbb744236273e5cfd1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086162"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Visualizzare un modello utilizzando il Visualizzatore Microsoft Association Rules
  Il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules disponibile in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di visualizzare i modelli di data mining compilati con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules è un algoritmo di associazione per la creazione dei modelli di data mining che è possibile utilizzare per l'analisi di mercato sugli acquisti. Per ulteriori informazioni su questo algoritmo, vedere [Microsoft Association Algorithm](microsoft-association-algorithm.md).  
  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules viene utilizzato principalmente per gli scopi seguenti:  
  
-   Per trovare set di elementi che descrivono gli elementi che in genere ricorrono insieme in una transazione.  
  
-   Per individuare le regole che consentono di stimare la presenza di altri elementi di una transazione in base agli elementi esistenti.  
  
> [!NOTE]  
>  Per visualizzare informazioni dettagliate sulle equazioni utilizzate nel modello e sui modelli individuati, utilizzare il visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer. Per altre informazioni, vedere [Visualizzare un modello usando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Per una procedura dettagliata per creare, esplorare e usare un modello di data mining di associazione, vedere [lezione 3: Creazione di uno Scenario Market Basket &#40;esercitazione intermedia sul Data Mining&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Schede del visualizzatore  
 Per la visualizzazione di un modello di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]viene utilizzato il visualizzatore appropriato nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining. Il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules include le schede seguenti:  
  
-   [Set di elementi](#BKMK_Itemsets)  
  
-   [Regole](#BKMK_Rules)  
  
-   [Rete di dipendenze](#BKMK_Dependency)  
  
 Ogni scheda contiene la casella di controllo **Mostra nomi lunghi** , che consente di visualizzare o nascondere la tabella di origine del set di elementi nella regola o nel set di elementi.  
  
###  <a name="BKMK_Itemsets"></a> Set di elementi  
 Nella scheda **Set di elementi** viene visualizzato l'elenco di set di elementi identificati dal modello come gruppi rilevati spesso insieme. La scheda viene visualizzata una griglia con le colonne seguenti: **Supporto tecnico**, **dimensioni**, e **set di elementi**. Per ulteriori informazioni sul supporto, vedere [Microsoft Association Algorithm](microsoft-association-algorithm.md). Nella colonna **Dimensioni** viene visualizzato il numero di elementi inclusi nel set di elementi. Nella colonna **Set di elementi** viene visualizzato il set di elementi effettivo individuato dal modello. È possibile controllare il formato del set di elementi impostando l'elenco **Mostra** sulle opzioni seguenti:  
  
-   **Mostra nome e valore dell'attributo**  
  
-   **Mostra solo il valore dell'attributo**  
  
-   **Mostra solo il nome dell'attributo**  
  
 È possibile filtrare il numero di set di elementi visualizzati nella scheda tramite le caselle di testo **Supporto minimo** e **Dimensioni minime set di elementi**. È possibile limitare ulteriormente il numero di set di elementi visualizzati tramite la casella di testo **Filtra set di elementi** e l'immissione di una caratteristica necessariamente esistente del set di elementi. Se ad esempio si digita "Water Bottle = existing", è possibile limitare i set di elementi solo a quelli che contengono una bottiglia di acqua. L'opzione **Filtra set di elementi** consente inoltre di visualizzare un elenco dei filtri utilizzati in precedenza.  
  
 Per ordinare le righe nella griglia, fare clic su un'intestazione di colonna.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Regole  
 Nella scheda **Regole** vengono visualizzate le regole individuate dall'algoritmo di associazione. Il **regole** scheda include una griglia che contiene le colonne seguenti: **Probabilità**, **importanza**, e **regola**. La probabilità descrive la possibilità di occorrenza del risultato di una regola. La priorità viene designata per misurare l'utilità di una regola. Anche se la probabilità di occorrenza di una regola è elevata, l'utilità della regola in sé potrebbe non essere prioritaria. La colonna Priorità consente di risolvere questo problema. Se ad esempio ogni set di elementi contiene uno stato specifico di un attributo, una regola che consente di eseguire la stima dello stato è superflua, anche se la probabilità è estremamente alta. Maggiore è la priorità, più importante è la regola.  
  
 È possibile filtrare le regole tramite le caselle di testo **Probabilità minima** e **Priorità minima** , in modo analogo al filtraggio eseguito nella scheda **Set di elementi** . È inoltre possibile filtrare una regola in base agli stati degli attributi che contiene tramite la casella di testo **Filtra regola** .  
  
 Per ordinare le righe nella griglia, fare clic su un'intestazione di colonna.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Rete di dipendenze  
 La scheda **Rete di dipendenze** include il Visualizzatore rete di dipendenze. Ogni nodo del visualizzatore rappresenta un elemento, ad esempio "state = WA". La freccia tra i nodi rappresenta l'associazione tra gli elementi. La direzione della freccia stabilisce l'associazione tra gli elementi in base alle regole individuate dall'algoritmo. Ad esempio, se il visualizzatore contiene tre elementi, A, B e C e C sia stimato in base A e B, se si seleziona il nodo C, due frecce rivolte verso il nodo C - da A C e B e C.  
  
 Il dispositivo di scorrimento a sinistra del visualizzatore svolge la funzione di filtro correlato alla probabilità delle regole. Se si sposta il dispositivo di scorrimento verso il basso, vengono visualizzati solo i collegamenti più attendibili.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Association Algorithm](microsoft-association-algorithm.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Strumenti di data mining](data-mining-tools.md)   
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
  

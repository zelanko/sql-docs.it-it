---
title: Aggiunta di modelli di data mining a una struttura (Analysis Services-Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], creating
- mining models [Analysis Services], creating
- mining models [Analysis Services], modifying
ms.assetid: a175daa5-58ea-474c-a82f-9648c5155dc8
author: minewiskan
ms.author: owend
ms.openlocfilehash: f1284d160ca828f75ec39112d614640fcb3ab1cb
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525698"
---
# <a name="add-mining-models-to-a-structure-analysis-services---data-mining"></a>Aggiungere modelli di data mining a una struttura (Analysis Services - Data mining)
  Una struttura di data mining può supportare più modelli di data mining. Pertanto dopo avere completato la procedura guidata è possibile aprire la struttura e aggiungere nuovi modelli di data mining. Ogni volta che si crea un modello, è possibile utilizzare un algoritmo diverso, modificare i parametri o applicare filtri per utilizzare un subset di dati diverso.  
  
## <a name="adding-new-mining-models"></a>Aggiunta di nuovi modelli di data mining  
 Quando si utilizza Creazione guidata modello di data mining per creare un nuovo modello di data mining, per impostazione predefinita è sempre necessario creare prima una struttura di data mining. Tramite la procedura guidata è quindi possibile aggiungere un modello di data mining iniziale alla struttura. Tuttavia, non è necessario creare immediatamente un modello. Se si crea solo la struttura, non è necessario prendere una decisione in merito alla colonna da utilizzare come attributo stimabile o su come utilizzare i dati in un determinato modello. Al contrario, è sufficiente impostare la struttura dei dati generale da utilizzare in futuro e in seguito utilizzare [Data Mining Designer](data-mining-designer.md) per aggiungere nuovi modelli di data mining basati su tale struttura.  
  
> [!NOTE]  
>  In DMX l'istruzione CREATE MINING MODEL inizia con il modello di data mining. Ovvero, si definisce il modello di data mining prescelto e la struttura sottostante viene automaticamente generata in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In un secondo momento è possibile continuare ad aggiungere nuovi modelli di data mining alla struttura usando l'istruzione ALTER STRUCTURE... Aggiungi istruzione del modello.  
  
## <a name="choosing-an-algorithm"></a>Scelta di un algoritmo  
 Quando si aggiunge un nuovo modello a una struttura esistente, la prima operazione da eseguire è la selezione di un algoritmo di data mining da utilizzare in tale modello. La scelta dell'algoritmo è importante perché ogni algoritmo esegue un tipo diverso di analisi e presenta requisiti diversi.  
  
 Quando si seleziona un algoritmo incompatibile con i dati, viene visualizzato un avviso. In alcuni casi, potrebbe essere necessario ignorare le colonne che non è possibile elaborare tramite l'algoritmo. In altri casi le modifiche verranno effettuate automaticamente dall'algoritmo. Ad esempio, se la struttura contiene dati numerici e l'algoritmo può funzionare solo con valori discreti, i valori numerici verranno automaticamente raggruppati in intervalli discreti. In alcuni casi, potrebbe essere necessario correggere prima i dati manualmente, scegliendo una chiave o un attributo stimabile.  
  
 Non è necessario modificare l'algoritmo quando si crea un nuovo modello. Spesso con lo stesso algoritmo si possono ottenere risultati molto diversi, ma occorre applicare un filtro ai dati o modificare un parametro come il metodo di clustering o le dimensioni minime del set di elementi. È consigliabile provare a utilizzare più modelli per individuare i parametri che consentono di ottenere risultati migliori.  
  
 Si noti che tutti i nuovi modelli devono essere elaborati prima di poterli utilizzare.  
  
## <a name="specifying-the-usage-of-columns-in-a-new-mining-model"></a>Specifica dell'utilizzo di colonne in un nuovo modello di data mining  
 Quando si aggiungono nuovi modelli di data mining a una struttura di data mining esistente, è necessario specificare come ciascuna colonna di dati dovrà essere utilizzata dal modello. A seconda del tipo di algoritmo scelto per il modello, è possibile che alcune scelte siano effettuate per impostazione predefinita. Le colonne di cui non si specifica la modalità di utilizzo non vengono incluse nella struttura di data mining. Tuttavia, i dati nella colonna possono essere ancora disponibili per il drill-through, se è supportato dal modello.  
  
 Le colonne della struttura di data mining utilizzate dal modello (se non impostate su Ignora) devono essere una chiave, una colonna di input, una colonna stimabile o una colonna stimabile i cui valori vengono anche utilizzati come input nel modello.  
  
-   Le colonne chiave contengono l'identificatore univoco di ogni riga di una tabella. Alcuni modelli di data mining, ad esempio quelli basati sul clustering delle sequenze o gli algoritmi Time Series, possono includere più colonne chiave. Queste chiavi tuttavia non sono chiavi composte nel senso relazionale, ma devono essere selezionate per supportare l'analisi delle serie temporali e del clustering delle sequenze.  
  
-   Le colonne di input contengono informazioni per l'esecuzione di stime. Nella Creazione guidata modello di data mining è disponibile la funzionalità **Suggerisci** , che risulta abilitata quando si seleziona una colonna stimabile. Se si fa clic su questo pulsante, nella procedura guidata verranno campionati i valori stimabili e verrà determinato quali altre colonne della struttura possono fungere da variabili. Verranno rifiutate le colonne chiave o altre colonne con molti valori univoci e verranno suggerite le colonne che risultano essere correlate con il risultato.  
  
     Questa funzionalità è particolarmente utile quando i set di dati contengono un numero di colonne più elevato di quanto sia necessario per compilare un modello di data mining. La funzionalità **Suggerisci** calcola un valore numerico compreso tra 0 e 1 che descrive la relazione tra ogni colonna del set di dati e la colonna stimabile. In base a questo valore vengono indicate le colonne da utilizzare come input per il modello. Se si utilizza la funzionalità **Suggerisci** , è possibile utilizzare la selezione di colonne indicate, modificare la selezione in base alle specifiche esigenze o ignorare la selezione di colonne suggerita.  
  
-   Le colonne stimabili contengono le informazioni che vengono stimate nel modello di data mining. È possibile selezionare più colonne come attributi stimabili. I modelli di clustering costituiscono un'eccezione in quanto un attributo stimabile è facoltativo.  
  
     A seconda del tipo di modello, può essere necessario che la colonna stimabile sia un tipo di dati specifico: ad esempio un modello di regressione lineare richiede una colonna numerica come valore stimato; l'algoritmo Naive Bayes richiede un valore discreto (anche tutti gli input devono essere discreti).  
  
## <a name="specifying-column-content"></a>Specifica del contenuto delle colonne  
 In alcuni casi può anche essere necessario specificare il *contenuto della colonna*. Nel data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la proprietà Tipo di contenuto di ogni colonna di dati indica all'algoritmo come devono essere elaborati i dati in tale colonna. Se ad esempio i dati includono una colonna Income, è necessario specificare che la colonna contiene numeri continui impostando il tipo di contenuto su Continuous. Tuttavia, è anche possibile specificare che i numeri della colonna Income devono essere raggruppati in bucket impostando il tipo di contenuto su Discretized e, se si desidera, specificando il numero esatto di bucket. È possibile creare modelli diversi che gestiscono le colonne in modo diverso. Ad esempio, è possibile provare con un modello che raggruppa i clienti in tre bucket di età e un altro che li raggruppa in 10 bucket di età.  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](mining-structures-analysis-services-data-mining.md)   
 [Creare una struttura di data mining relazionale](create-a-relational-mining-structure.md)   
 [Proprietà modello di data mining](mining-model-properties.md)   
 [Colonne del modello di data mining](mining-model-columns.md)  
  
  

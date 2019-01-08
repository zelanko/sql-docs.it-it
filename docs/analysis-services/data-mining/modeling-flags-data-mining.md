---
title: Flag di modellazione (Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f644f882d1a252f678d868d3492b4aed4e11006f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531904"
---
# <a name="modeling-flags-data-mining"></a>Flag di modellazione (data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile usare flag di modellazione per offrire a un algoritmo di data mining informazioni aggiuntive sui dati definiti in una tabella del case. L'algoritmo può utilizzare tali informazioni per compilare un modello di data mining più accurato.  
  
 Alcuni flag di modellazione sono definiti al livello della struttura di data mining, mentre altri al livello della colonna del modello di data mining. Ad esempio, il flag di modellazione **NOT NULL** viene usato con le colonne della struttura di data mining. È possibile definire flag di modellazione aggiuntivi sulle colonne del modello di data mining, a seconda dell'algoritmo utilizzato per creare il modello.  
  
> [!NOTE]  
>  È possibile che i plug-in di terze parti includano flag di modellazione diversi, in aggiunta a quelli predefiniti in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="list-of-modeling-flags"></a>Elenco dei flag di modellazione  
 Nell'elenco seguente sono descritti i flag di modellazione supportati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per informazioni sui flag di modellazione supportati da algoritmi specifici, vedere l'argomento di riferimento tecnico per l'algoritmo utilizzato per creare il modello.  
  
 **NOT NULL**  
 Indica che i valori per la colonna attributo non devono mai contenere valori null. Se durante il processo di training del modello [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rileva un valore null per la colonna attributo, verrà generato un errore.  
  
 **MODEL_EXISTENCE_ONLY**  
 Indica che la colonna verrà considerata come se presentasse due stati: **Mancano** e **esistenti**. Se il valore è **NULL**, viene considerata come Mancante. Il flag MODEL_EXISTENCE_ONLY viene applicato all'attributo stimabile ed è supportato dalla maggior parte degli algoritmi.  
  
 In effetti, l'impostazione del flag MODEL_EXISTENCE_ONLY **True** cambia la rappresentazione dei valori in modo che siano presenti solo due stati: **Mancano** e **esistenti**. Tutti gli stati non mancanti sono combinati in un solo valore **Esistente** .  
  
 Questo flag di modellazione viene tipicamente usato negli attributi in cui lo stato **NULL** ha un significato implicito e il valore esplicito dello stato **NOT NULL** può essere meno importante del fatto che la colonna contenga un valore. Ad esempio, una colonna [DateContractSigned] potrebbe essere **NULL** se non è mai stato firmato un contratto e **NOT NULL** se il contratto è stato firmato. Pertanto, se lo scopo del modello è quello di stimare se un contratto verrà firmato, è possibile usare il flag MODEL_EXISTENCE_ONLY per ignorare il valore esatto relativo alla data nei case **NOT NULL** e distinguere solo tra case in cui il contratto è **Mancante** o **Esistente**.  
  
> [!NOTE]  
>  Missing è uno stato speciale utilizzato dall'algoritmo e si distingue dal valore di testo "Mancante" in una colonna. Per altre informazioni, vedere [Valori mancanti &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
 **REGRESSOR**  
 Indica che la colonna può essere utilizzata come regressore durante l'elaborazione. Questo flag è definito in una colonna del modello di data mining e può essere applicato solo a colonne con tipo di dati numerico continuo. Per altre informazioni sull'utilizzo di questo flag, vedere la sezione in questo argomento, [Utilizzi del flag di modellazione REGRESSOR](#bkmk_UseRegressors).  
  
## <a name="viewing-and-changing-modeling-flags"></a>Visualizzazione e modifica dei flag di modellazione  
 È possibile visualizzare i flag di modellazione associati a una colonna della struttura di data mining o del modello in Progettazione modelli di data mining visualizzando le proprietà della struttura o del modello.  
  
 Per determinare quali flag di modellazione sono stati applicati alla struttura di data mining corrente, è possibile creare una query sul set di righe dello schema di data mining che restituisce i flag di modellazione solo per le colonne della struttura, tramite una query analoga alla seguente:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 È possibile aggiungere o modificare i flag di modellazione utilizzati in un modello utilizzando Progettazione modelli di data mining e modificando le proprietà delle colonne associate. Tali modifiche richiedono la rielaborazione della struttura o del modello.  
  
 È possibile specificare flag di modellazione in una nuova struttura o in un nuovo modello di data mining tramite DMX o script AMO o XMLA. Non è tuttavia possibile modificare i flag di modellazione utilizzati in un modello e in una struttura di data mining esistenti tramite DMX. È necessario creare un nuovo modello di data mining usando la sintassi `ALTER MINING STRUCTURE....ADD MINING MODEL`.  
  
##  <a name="bkmk_UseRegressors"></a> Utilizzi del flag di modellazione REGRESSOR  
 Quando si imposta il flag di modellazione REGRESSOR in una colonna, si indica all'algoritmo che la colonna contiene potenziali regressori. I regressore effettivi utilizzati nel modello sono determinati dall'algoritmo. Un regressore potenziale può essere ignorato se non modella l'attributo stimabile.  
  
 Quando si compila un modello utilizzando Creazione guidata modello di data mining, tutte le colonne di input continue sono contrassegnate come possibili regressori. Anche se non si imposta in modo esplicito il flag REGRESSOR in una colonna, pertanto, tale colonna potrebbe essere utilizzata come regressore nel modello.  
  
 È possibile determinare i regressori effettivamente utilizzati nel modello elaborato eseguendo una query sul set di righe dello schema per il modello di data mining, come illustrato nell'esempio seguente:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **Nota** Se si modifica un modello di data mining e si cambia il tipo di contenuto di una colonna da continuo a discreto, è necessario modificare manualmente il flag nella colonna di data mining, quindi rielaborare il modello.  
  
### <a name="regressors-in-linear-regression-models"></a>Regressori nei modelli di regressione lineare  
 I modelli di regressione lineare si basano sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees. Anche se non si utilizza l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression, qualsiasi modello di albero delle decisioni può contenere un albero o nodi che rappresentano una regressione su un attributo continuo.  
  
 In questi modelli, pertanto, non è necessario specificare che una colonna continua rappresenta un regressore. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees suddividerà il set di dati in aree con modelli significativi anche se non si imposta il flag REGRESSOR nella colonna. La differenza è data dal fatto che quando si imposta il flag di modellazione, l'algoritmo tenterà di trovare equazioni di regressione nel formato seguente per adattare i modelli nei nodi dell'albero.  
  
 a*C1 + b\*C2 +...  
  
 Viene quindi calcolata la somma dei residui e, se la deviazione è eccessiva, nell'albero viene imposta una divisione.  
  
 Ad esempio, se si stima il comportamento di acquisto dei clienti usando **Reddito** come attributo e si imposta il flag di modellazione REGRESSOR nella colonna, per prima cosa l'algoritmo tenterà di adattare i valori **Reddito** usando una formula di regressione standard. Se la deviazione è eccessiva, la formula di regressione viene abbandonata e l'albero viene diviso in base a un altro attributo. L'algoritmo Decision Trees tenta quindi di adattare un regressore per il reddito in ognuno dei rami dopo la divisione.  
  
 È possibile utilizzare il parametro FORCED_REGRESSOR per garantire che l'algoritmo utilizzi un determinato regressore. Questo parametro può essere utilizzato con l'algoritmo Decision Trees e con l'algoritmo Linear Regression.  
  
## <a name="related-tasks"></a>Attività correlate  
 Utilizzare i collegamenti seguenti per ulteriori informazioni sull'utilizzo dei flag di modellazione.  
  
|Attività|Argomento|  
|----------|-----------|  
|Modificare i flag di modellazione tramite Progettazione modelli di data mining|[Visualizzare o modificare flag di modellazione &#40;Data mining&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Specificare un hint all'algoritmo per segnalare i probabili regressori|[Specificare una colonna da usare come regressore in un modello](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Vedere i flag di modellazione supportati da algoritmi specifici nella sezione Flag di modellazione dell'argomento di riferimento per ogni algoritmo|[Algoritmi di Data Mining &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|Vengono fornite ulteriori informazioni sulle colonne della struttura di data mining e sulle proprietà che è possibile impostare su di esse|[Colonne della struttura di data mining](../../analysis-services/data-mining/mining-structure-columns.md)|  
|Vengono fornite ulteriori informazioni sulle colonne del modello di data mining e sui flag di modellazione che è possibile applicare a livello del modello|[Colonne del modello di data mining](../../analysis-services/data-mining/mining-model-columns.md)|  
|Vedere la sintassi per l'utilizzo dei flag di modellazione nelle istruzioni DMX|[Flag di modellazione &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Vengono illustrati i valori mancanti e la relativa modalità di utilizzo|[Valori mancanti &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)|  
|Vengono fornite informazioni sulla gestione di modelli e strutture e sull'impostazione delle proprietà di utilizzo|[Spostamento di oggetti di data mining](../../analysis-services/data-mining/moving-data-mining-objects.md)|  
  
  

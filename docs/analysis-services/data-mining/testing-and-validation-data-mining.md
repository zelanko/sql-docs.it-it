---
title: Test e convalida (Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e4ce983ed5d5a645f32466ab38d5c67ff1c68897
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182312"
---
# <a name="testing-and-validation-data-mining"></a>Test e convalida (Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La convalida è il processo che consente di valutare le prestazioni dei modelli di data mining rispetto ai dati reali. Per convalidare in modo corretto i modelli di data mining, è importante comprenderne la qualità e le caratteristiche prima di distribuirli in un ambiente di produzione.  
  
 Questa sezione introduce alcuni concetti di base relativi alla qualità dei modelli e descrive le strategie per la convalida dei modelli fornite in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per una panoramica sullo scopo della convalida dei modelli nel contesto più ampio del processo di data mining, vedere [Soluzioni di data mining](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>Metodi di test e convalida dei modelli di data mining  
 La valutazione della qualità e delle caratteristiche di un modello di data mining può essere eseguita in base ad approcci diversi.  
  
-   Utilizzare varie misure della validità statistica per determinare se sono presenti problemi nei dati o nel modello.  
  
-   Separare i dati in set di training e di testing per valutare l'accuratezza delle stime.  
  
-   Chiedere agli esperti aziendali di esaminare i risultati del modello di data mining per determinare se i modelli individuati sono significativi nello scenario aziendale di destinazione.  
  
 Tutti questi metodi risultano utili nella metodologia di data mining e vengono utilizzati in maniera iterativa durante la creazione, l'esecuzione di test e l'ottimizzazione di modelli per rispondere a un problema specifico. Non esiste alcuna regola completa in grado di stabilire quando un modello è affidabile o quando si dispone di dati sufficienti.  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>Definizione dei criteri per la convalida dei modelli di data mining  
 Le misure relative al data mining rientrano generalmente nelle categorie di accuratezza, affidabilità e utilità.  
  
 L'*accuratezza* consente di misurare il livello di correlazione tra il risultato e gli attributi nei dati specificati fornito dal modello. Sebbene siano disponibili diverse misure di accuratezza, tutte dipendono dai dati utilizzati. Nelle situazioni reali i valori potrebbero non essere disponibili o essere approssimati oppure è possibile che i dati siano stati modificati da più processi. In particolare, nella fase di esplorazione e sviluppo è possibile decidere di accettare una certa quantità di errore nei dati, soprattutto se questi ultimi sono equamente uniformi nelle caratteristiche. Ad esempio, un modello che stima le vendite per un negozio specifico in base alle vendite precedenti può essere strettamente correlato ed estremamente accurato, anche se tale negozio ha utilizzato in modo costante un metodo contabile non corretto. Di conseguenza, le misure dell'accuratezza devono essere bilanciate da valutazioni dell'affidabilità.  
  
 L'*affidabilità* consente di valutare le prestazioni di un modello di data mining rispetto a set di dati diversi. Un modello di data mining è affidabile se genera lo stesso tipo di stime o individua gli stessi tipi generali di modelli indipendentemente dai dati di prova forniti. Il modello generato ad esempio per il negozio che ha utilizzato il metodo contabile non corretto non consentirebbe una generalizzazione accurata rispetto agli altri negozi e pertanto non sarebbe affidabile.  
  
 L'*utilità* include diverse metriche che indicano se il modello fornisce informazioni vantaggiose. Un modello di data mining che correla ad esempio l'ubicazione di un negozio con le vendite potrebbe essere accurato e affidabile, ma potrebbe non essere utile, poiché non è possibile generalizzare tale risultato aggiungendo altri negozi nella stessa ubicazione. Tale modello inoltre non risponde alla domanda aziendale fondamentale, ovvero non indica perché a ubicazioni specifiche è associato un numero maggiore di vendite. È possibile anche rilevare che un modello apparentemente positivo non è in effetti significativo, poiché si basa su correlazioni incrociate dei dati.  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>Strumenti per il test e la convalida dei modelli di data mining  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta più approcci per la convalida di soluzioni di data mining e consente di gestire tutte le fasi della metodologia di test del data mining.  
  
-   Partizionamento dei dati in set di training e di testing.  
  
-   Applicazione di filtri ai modelli per eseguire il training e il testing di diverse combinazioni degli stessi dati di origine.  
  
-   Misurazione di *accuratezza* e *miglioramento*. Un *grafico di accuratezza* consente di visualizzare il miglioramento che si ottiene mediante l'uso di un modello di data mining confrontato con un'ipotesi casuale.  
  
-   Esecuzione della *convalida incrociata* dei set di dati  
  
-   Generazione di *matrici di classificazione*. Questi grafici consentono di ordinare ipotesi accurate e non corrette in una tabella, in modo che sia possibile valutare rapidamente e semplicemente il livello di accuratezza della stima del valore di destinazione effettuata dal modello.  
  
-   Creazione di *grafici a dispersione* per valutare l'adeguatezza di una formula di regressione.  
  
-   Creazione di *grafici dei profitti* che consentono di associare il guadagno o il costo finanziario all'uso di un modello di data mining in modo da poter valutare le indicazioni.  
  
 L'obiettivo di questa metrica non è rilevare se il modello di data mining risponde alle esigenze aziendali, bensì ottenere misure obiettive utilizzabili per valutare l'affidabilità dei dati per l'analisi predittiva e supportare l'utente nella decisione di utilizzare o meno una particolare iterazione nel processo di sviluppo.  
  
 Negli argomenti di questa sezione viene fornita una panoramica di ogni metodo e viene descritto il processo di misurazione dell'accuratezza di modelli compilati utilizzando Data mining di SQL Server.  
  
### <a name="related-topics"></a>Argomenti correlati  
  
|Argomento|Collegamenti|  
|------------|-----------|  
|Informazioni sulla configurazione di un set di dati di test tramite una procedura guidata o comandi DMX|[Set di dati di training e di testing](../../analysis-services/data-mining/training-and-testing-data-sets.md)|  
|Informazioni sul test della distribuzione e della rappresentatività dei dati in una struttura di data mining|[Convalida incrociata &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Informazioni sui tipi di grafico di accuratezza forniti.|[Grafico di accuratezza &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Grafico dei profitti &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Grafico a dispersione &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Informazioni sulla creazione di una matrice di classificazione, talvolta denominata matrice di confusione, per valutare il numero di veri e falsi positivi e di veri e falsi negativi.|[Matrice di classificazione &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di data mining](../../analysis-services/data-mining/data-mining-tools.md)   
 [Soluzioni di data mining](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Attività e procedure di test e convalida &#40;data mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  

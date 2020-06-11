---
title: Progettazione modelli di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
author: minewiskan
ms.author: owend
ms.openlocfilehash: 98176d54f6cdf29be5c06563ec1dbd7fd6275724
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523168"
---
# <a name="data-mining-designer"></a>Data Mining Designer
  Progettazione modelli di data mining è l'ambiente principale in cui si utilizzano i modelli di data mining in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . È possibile accedere alla finestra di progettazione selezionando una struttura di data mining esistente o utilizzando la Creazione guidata modello di data mining per creare una nuova struttura e un nuovo modello di data mining. Progettazione modelli di data mining consente di eseguire le attività seguenti:  
  
-   Modificare la struttura e il modello di data mining creati inizialmente dalla Creazione guidata modello di data mining.  
  
-   Creare nuovi modelli basati su una struttura di data mining esistente.  
  
-   Eseguire il training dei modelli di data mining e visualizzarli.  
  
-   Confrontare i modelli mediante grafici di accuratezza.  
  
-   Creare query di stima basate sui modelli di data mining.  
  
## <a name="mining-structure-tab"></a>Scheda Struttura di data mining  
 Usare la scheda **Struttura di data mining** per aggiungere colonne e modificare le proprietà di una struttura di data mining esistente. Negli argomenti e nelle attività seguenti sono disponibili ulteriori informazioni sull'utilizzo delle strutture di data mining:  
  
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)  
  
 [Attività e procedure relative alla struttura di data mining](mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Scheda Modelli di data mining  
 La scheda **Modelli di data mining** consente di gestire i modelli di data mining esistenti e di creare nuovi modelli. I modelli di data mining sono sempre basati su una struttura di data mining esistente.  
  
 Nella scheda **Modelli di data mining** è possibile modificare il tipo di algoritmo, aggiungere o rimuovere le colonne associate alla struttura del modello, modificare le proprietà delle colonne specifiche dell'algoritmo, specificare l'utilizzo delle colonne del modello di data mining e modificare i parametri dell'algoritmo associati al modello di data mining. È inoltre possibile elaborare la struttura di data mining insieme ai modelli selezionati o a tutti i modelli associati.  
  
 Per ulteriori informazioni su come utilizzare i modelli di data mining, vedere gli argomenti seguenti:  
  
 [Modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-models-analysis-services-data-mining.md)  
  
 [Attività e procedure relative al modello di data mining](mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Scheda Visualizzatore modello di data mining  
 La scheda **Visualizzatore modello di data mining** consente l'esplorazione visiva dei modelli di data mining. Ogni modello di data mining è associato a un visualizzatore personalizzato che mostra il contenuto specifico di tale modello. È inoltre possibile visualizzare il contenuto del modello di data mining tramite il visualizzatore del contenuto.  
  
 Per ulteriori informazioni su come esplorare i modelli di data mining con i visualizzatori di data mining, vedere gli argomenti seguenti:  
  
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Scheda Grafico accuratezza modello di data mining  
 La scheda **Grafico accuratezza modello di data mining** consente di eseguire il test di accuratezza predittiva di un singolo modello di data mining o di confrontare la validità di più modelli di data mining contenuti in una struttura di data mining. La scheda contiene strumenti per il filtraggio dei dati, la selezione dei modelli di data mining e la visualizzazione dei risultati in un grafico di accuratezza, in un grafico dei profitti o in una matrice di classificazione.  
  
 Per ulteriori informazioni sull'esecuzione di test e la convalida di modelli di data mining, vedere gli argomenti seguenti:  
  
 [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md)  
  
 [Attività e procedure di test e convalida &#40;data mining&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Scheda Stima modello di data mining  
 La scheda **Stima modello di data mining** include il generatore delle query di stima, che consente di creare query di stima DMX (Data Mining Extensions). La scheda contiene strumenti per l'impostazione dei modelli di data mining e delle tabelle di input, il mapping tra le colonne del modello di data mining e le colonne della tabella di input, l'aggiunta di funzioni a una query e l'impostazione di criteri per ogni colonna.  
  
 Dopo aver progettato una query, è possibile utilizzare viste diverse nella scheda per visualizzare i risultati della query e modificarla manualmente. È inoltre possibile salvare i risultati della query in una tabella di un database.  
  
 Per ulteriori informazioni sulla creazione di query di data mining, vedere gli argomenti seguenti:  
  
 [Query di data mining](data-mining-queries.md)  
  
 [Attività e procedure relative alle query di data mining](data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Soluzioni di data mining](data-mining-solutions.md)  
  
  

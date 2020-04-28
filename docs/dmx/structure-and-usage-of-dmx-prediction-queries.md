---
title: Struttura e utilizzo di query di stima DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 99d8ef98ad4e86bce0e1beff819a8d140662aaf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938066"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Struttura e utilizzo di query di stima DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]è possibile utilizzare la query di stima in DMX (Data Mining Extensions) per stimare i valori di colonna sconosciuti in un nuovo set di dati, in base ai risultati di un modello di data mining.  
  
 Il tipo di query da utilizzare dipende dal tipo di informazioni che si desidera ottenere dal modello. Per creare semplici stime in tempo reale, ad esempio per sapere se il profilo di un potenziale cliente su un sito Web è quello di un acquirente di biciclette, è necessario utilizzare una query singleton. Se si desidera creare un batch di stime da un set di case contenuti in un'origine dati, utilizzare una query di stima regolare.  
  
## <a name="prediction-types"></a>Tipi di stima  
 È possibile utilizzare DMX per creare i tipi di stima seguenti:  
  
 Prediction join  
 Consente di creare stime sui dati di input in base ai modelli esistenti nel modello di data mining. Questa istruzione di query deve essere seguita da una clausola on che fornisce le condizioni **di** join tra le colonne del modello di data mining e le colonne di input.  
  
 Natural prediction join  
 Consente di creare stime basate sui nomi di colonna del modello di data mining che corrispondono esattamente a quelli nella tabella su cui si esegue la query. Questa istruzione di query non richiede una clausola on, perché la condizione di join viene generata automaticamente in base ai nomi corrispondenti tra le colonne del modello di data mining e le colonne **di** input.  
  
 Prediction join vuoto  
 Consente di individuare le stime più probabili, senza che sia necessario specificare dati di input. Viene così restituita una stima basata unicamente sul contenuto del modello di data mining.  
  
 Query singleton  
 Consente di creare una stima inviando i dati direttamente alla query. Questa istruzione è utile perché consente di inviare un singolo case alla query, per ottenere i risultati più rapidamente. È ad esempio possibile utilizzare questa query per stimare la probabilità che una donna sposata di 35 anni acquisti una bicicletta. Questa query non richiede un'origine dati esterna.  
  
## <a name="query-structure"></a>Struttura della query  
 Per compilare una query di stima in DMX è necessario combinare gli elementi seguenti:  
  
-   **SELECT [FLATD]**  
  
-   **TOP**  
  
-   **FROM***Da\<Model>* **PREDICTION JOIN**      
  
-   **IN**  
  
-   **IN cui**  
  
-   **ORDER BY**  
  
 L'elemento **Select** di una query di stima definisce le colonne e le espressioni che verranno visualizzate nel set di risultati e può includere i dati seguenti:  
  
-   **Stimare** o **PredictOnly** le colonne del modello di data mining.  
  
-   Qualsiasi colonna dei dati di input utilizzata per creare le stime.  
  
-   Funzioni mediante le quali viene restituita una colonna di dati.  
  
 L'elemento **from** * \<Model>* **PREDICTION JOIN** definisce i dati di origine da utilizzare per creare la stima. Per una query singleton tale origine è costituita da una serie di valori assegnati alle colonne. Per un prediction join vuoto l'origine dei dati viene lasciata vuota.  
  
 L'elemento **on** esegue il mapping delle colonne definite nel modello di data mining alle colonne di un set di dati esterno. Questo elemento non è necessario per la creazione di una query con prediction join vuoto o natural prediction join.  
  
 È possibile utilizzare la clausola **where** per filtrare i risultati di una query di stima. È possibile utilizzare una clausola **Top** o **Order by** per selezionare le stime più probabili. Per ulteriori informazioni sull'utilizzo di queste clausole, vedere [SELECT &#40;DMX&#41;](../dmx/select-dmx.md).  
  
 Per ulteriori informazioni sulla sintassi di un'istruzione di stima, vedere [Select from &#60;model&#62; PREDICTION JOIN &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) e [Select from &#60;model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

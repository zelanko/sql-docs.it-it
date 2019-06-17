---
title: Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f44c1cb014ca9abcd6122f6db6ee0e33407b7d1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678865"
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer visualizza informazioni dettagliate sui modelli individuati dall'algoritmo di data mining e fornisce anche l'accesso a varie statistiche generate durante il processo di analisi. La quantità e il tipo di informazioni variano a seconda dell'algoritmo utilizzato, ma è possibile includere le categorie seguenti:  
  
-   Segmenti di dati e relative caratteristiche.  
  
-   Statistiche descrittive su ogni gruppo o sull'intero set di dati.  
  
-   Numero di rami o nodi figlio in un albero.  
  
-   Calcoli, ad esempio varianza e media, relativi a un cluster o a un intero set di dati.  
  
 La visualizzazione di queste informazioni consente di interpretare in modo più efficace i risultati dell'analisi. È inoltre possibile identificare le modalità per ottimizzare il modello e quindi ripeterne il training. In alternativa, è possibile decidere di ripetere il training utilizzando un algoritmo diverso.  
  
## <a name="viewing-mining-model-content"></a>Visualizzazione del contenuto di un modello di data mining  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer vengono visualizzati elementi quali colonne, regole, proprietà, attributi, nodi e altro contenuto dal *set di righe dello schema relativo al contenuto* del modello di data mining. Il set di righe dello schema relativo al contenuto è un framework generico per la presentazione di informazioni dettagliate sul contenuto di un modello di data mining.  
  
 Queste informazioni dettagliate sono contenute in una tabella HTML che rappresenta gli schemi, i cluster o gli alberi del modello come nodi. È possibile fare clic su ogni nodo ed espanderlo per visualizzare più dettagli, ad esempio le formule o il conteggio di valori distinti per un attributo numerico. È anche possibile esplorare le relazioni padre-figlio tra i nodi.  
  
 Per altre informazioni sul significato generale dei termini usato nel contenuto di un modello di data mining, vedere [Contenuto del modello di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md). In questo argomento sono inoltre contenuti i collegamenti a informazioni sul contenuto del modello di data mining per tipi di modelli specifici. Poiché ogni tipo di modello di data mining contiene informazioni specifiche dell'algoritmo e degli schemi trovati nei dati, si consiglia di consultare l'argomento di riferimento tecnico per ogni tipo di modello per comprendere pienamente ogni tipo di modello.  
  
## <a name="querying-mining-model-content"></a>Esecuzione di query sul contenuto di un modello di data mining  
 Le stesse informazioni fornite in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer sono anche disponibili eseguendo una query sul modello di data mining. È possibile creare query sul contenuto del modello di data mining tramite istruzioni DMX (Data Mining Extension). Ad esempio, in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]è possibile eseguire una query sul contenuto tramite l'istruzione DMX seguente:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Per altre informazioni, vedere [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  

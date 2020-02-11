---
title: Modellazione avanzata (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 669fa1fcd9e4802a4d4102120a373dd615741017
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062740"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>Modellazione avanzata (componenti aggiuntivi Data mining per Excel)
  È possibile usare le opzioni **Avanzate** di modellazione dei dati per creare strutture e modelli di data mining personalizzati con parametri diversi da quelli creati dalle procedure guidate. Le due procedure guidate descritte in questa sezione consentono di creare una struttura di data mining completamente nuova e un nuovo modello di data mining da applicare a una struttura di data mining esistente.  
  
## <a name="create-mining-structure"></a>Crea struttura di data mining  
 ![Pulsante Crea la struttura di data mining, barra multifunzione Data mining](media/dmc-createstruct.gif "Pulsante Crea la struttura di data mining, barra multifunzione Data mining")  
  
 La **procedura guidata crea struttura di data mining** consente di compilare una nuova struttura di data mining. Una struttura è una raccolta dei dati estratti da un'origine dati specificata.  Una struttura di data mining può essere aggiornata con nuovi dati di origine, ma quando si crea la struttura di data mining, è necessario definire i tipi di dati e i nomi che definiscono il modo in cui i dati vengono utilizzati per l'analisi.  
  
 È possibile utilizzare le seguenti origini dati per compilare la struttura: una tabella di Excel, un intervallo di Excel o tutti i dati in un'origine dati esterna che è già stata definita come vista origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ogni struttura, è possibile destinare alcuni dati al testing e alla convalida. Creando questo *set di dati* di controllo quando si configurano le origini dati, è possibile garantire che tutti i modelli basati sulla struttura siano in grado di utilizzare un set di dati coerente per il test.  
  
 Dopo avere creato una struttura di data mining, è possibile aggiungere più modelli per applicare metodi di analisi differenti.  
  
 Per ulteriori informazioni sull'utilizzo della creazione **guidata struttura**di data mining, vedere creare una struttura di data mining [&#40;SQL Server componenti aggiuntivi Data mining&#41;](create-mining-structure-sql-server-data-mining-add-ins.md).  
  
## <a name="add-model-to-structure"></a>Aggiunta modello a struttura  
 ![Pulsante Aggiunta modello a struttura](media/dmc-addmodel.gif "Pulsante Aggiunta modello a struttura")  
  
 Quando si aggiunge un nuovo modello a una struttura, si analizzano i dati con un algoritmo diverso o con parametri diversi. Questa opzione risulta particolarmente utile se si desidera creare un modello utilizzando uno degli algoritmi non esposti negli strumenti del Client di data mining.  
  
 Ad esempio, è possibile utilizzare uno qualsiasi degli algoritmi supportati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], ad esempio:  
  
-   Linear regression  
  
-   Sequence Clustering  
  
-   Analisi di associazione sui set di dati nidificati  
  
 Per visualizzare il tipo di strutture di data mining disponibili, è possibile esplorare i modelli e le strutture [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] archiviati in facendo clic su **Gestisci modelli** o **Sfoglia**.  
  
 È possibile utilizzare solo le strutture di data mining create durante la sessione corrente oppure quelle salvate a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ulteriori informazioni, vedere la pagina relativa [all'aggiunta di un modello a una struttura &#40;componenti aggiuntivi Data mining per Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire i modelli &#40;SQL Server componenti aggiuntivi Data mining&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  

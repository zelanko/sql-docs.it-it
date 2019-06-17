---
title: Advanced modellazione (Data componenti aggiuntivi Data Mining per Excel) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062740"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>Modellazione avanzata (componenti aggiuntivi Data mining per Excel)
  È possibile usare la **avanzate** opzioni per creare diversi da quelli creati tramite le procedure guidate modelli e strutture di data mining dei dati personalizzate con i parametri di modellazione dati. Le due procedure guidate descritte in questa sezione consentono di creare una struttura di data mining completamente nuova e un nuovo modello di data mining da applicare a una struttura di data mining esistente.  
  
## <a name="create-mining-structure"></a>Crea struttura di data mining  
 ![Pulsante Crea struttura di Data Mining, barra multifunzione Data Mining](media/dmc-createstruct.gif "pulsante Crea struttura di Data Mining, barra multifunzione Data Mining")  
  
 Il **Creazione guidata di struttura di Data Mining** consente di creare una nuova struttura di data mining. Una struttura è una raccolta dei dati estratti da un'origine dati specificata.  Una struttura di data mining può essere aggiornata con nuovi dati di origine, ma quando si crea la struttura di data mining, è necessario definire i tipi di dati e i nomi che definiscono il modo in cui i dati vengono utilizzati per l'analisi.  
  
 È possibile utilizzare le seguenti origini dati per compilare la struttura: una tabella di Excel, un intervallo di Excel o tutti i dati in un'origine dati esterna che è già stata definita come vista origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ogni struttura, è possibile destinare alcuni dati al testing e alla convalida. Creando ciò *set di dati di controllo* quando configuri le origini dati, è possibile assicurarsi che tutti i modelli basati sulla struttura siano in grado di usare un set di dati coerente per il test.  
  
 Dopo avere creato una struttura di data mining, è possibile aggiungere più modelli per applicare metodi di analisi differenti.  
  
 Per altre informazioni su come usare il **procedura guidata Crea struttura di Data Mining**, vedere [Create Mining Structure &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md).  
  
## <a name="add-model-to-structure"></a>Aggiunta modello a struttura  
 ![Aggiungere modello di pulsante di struttura](media/dmc-addmodel.gif "aggiunta modello a pulsante struttura")  
  
 Quando si aggiunge un nuovo modello a una struttura, si analizzano i dati con un algoritmo diverso o con parametri diversi. Questa opzione risulta particolarmente utile se si desidera creare un modello utilizzando uno degli algoritmi non esposti negli strumenti del Client di data mining.  
  
 Ad esempio, è possibile utilizzare uno qualsiasi degli algoritmi supportati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], ad esempio:  
  
-   Linear Regression  
  
-   Sequence Clustering  
  
-   Analisi di associazione sui set di dati nidificati  
  
 Per vedere quali tipi di strutture di data mining sono disponibili, è possibile esplorare i modelli e le strutture archiviati in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] facendo **Gestione modelli** oppure **Sfoglia**.  
  
 È possibile utilizzare solo le strutture di data mining create durante la sessione corrente oppure quelle salvate a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per altre informazioni, vedere [aggiunta modello a struttura &#40;aggiuntivi di Data Mining per Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire i modelli &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  

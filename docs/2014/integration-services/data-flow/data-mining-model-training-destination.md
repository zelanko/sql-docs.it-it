---
title: Destinazione Training modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingmodeltrainingdest.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5dac84fe42185806ae468593876a6bd439c1c689
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890649"
---
# <a name="data-mining-model-training-destination"></a>Training modello di data mining - destinazione
  La destinazione Training modello di data mining consente di eseguire il training dei modelli di data mining passando i dati ricevuti dalla destinazione agli algoritmi dei modelli di data mining. È possibile eseguire il training di più modelli di data mining con una singola destinazione, se i modelli sono compilati in base alla stessa struttura di data mining. Per altre informazioni, vedere [Colonne della struttura di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-structure-columns) e [Colonne del modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>Configurazione della destinazione Training modello di data mining  
 Se una colonna livello case della struttura di destinazione e i modelli compilati sulla struttura presentano il tipo di contenuto KEY TIME o KEY SEQUENCE, i dati di input devono essere ordinati in base a questa colonna. I modelli compilati utilizzando l'algoritmo Microsoft Time Series, ad esempio, hanno tipo di contenuto KEY TIME. Se i dati di input non sono ordinati, non sarà possibile elaborare il modello. Se sono necessari dati ordinati, sarà possibile inserire una trasformazione Ordinamento in un punto precedente del flusso di dati per ordinare i dati. Questo non è vale per le colonne con tipo di contenuto KEY. Per altre informazioni, vedere [Tipi di contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining) e [Trasformazione ordinamento](transformations/sort-transformation.md).  
  
> [!NOTE]  
>  L'input della destinazione Training modello di data mining deve essere ordinato. Per ordinare i dati è possibile includere una trasformazione Ordinamento in un punto a monte della destinazione Training modello di data mining nel flusso di dati. Per altre informazioni, vedere [Trasformazione Ordinamento](transformations/sort-transformation.md).  
  
 Questa destinazione include un input e nessun output.  
  
 La destinazione Training modello di data mining utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una gestione connessione per connettersi al [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto di o all'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di che contiene la struttura di data mining e i modelli di data mining trainati dalla destinazione. Per altre informazioni, vedere [Gestione connessione Analysis Services](../connection-manager/analysis-services-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor training modelli di data mining** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor training modello di data mining &#40;scheda connessione&#41;](../data-mining-model-training-editor-connection-tab.md)  
  
-   [Editor training modelli di data mining &#40;scheda colonne&#41;](../data-mining-model-training-editor-columns-tab.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate della destinazione Training modello di data mining](data-mining-model-training-destination-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
  

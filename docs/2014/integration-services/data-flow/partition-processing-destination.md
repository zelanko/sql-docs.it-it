---
title: Destinazione elaborazione partizione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 53ef09d19b62c0e6ce7742c41581d3cdefdfc374
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890558"
---
# <a name="partition-processing-destination"></a>Destinazione elaborazione partizione
  La destinazione Elaborazione partizione consente di caricare ed elaborare una partizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulle partizioni, vedere [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data).  
  
 La destinazione elaborazione partizione include le funzionalità seguenti:  
  
-   Opzioni per l'esecuzione di elaborazioni incrementali, complete o di aggiornamento.  
  
-   Configurazione degli errori, per specificare se l'elaborazione deve ignorare gli errori o arrestarsi dopo un numero di errori specificato.  
  
-   Mapping di colonne di input a colonne di partizione.  
  
 Per altre informazioni sull'elaborazione degli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services).  
  
> [!NOTE]  
>  Le attività qui descritte non si applicano ai modelli tabulari di Analysis Services.  Non è possibile eseguire il mapping di colonne di input a colonne di partizione per i modelli tabulari. È possibile utilizzare invece l'attività Esegui DDL Analysis Services [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) per elaborare la partizione.  
  
## <a name="configuration-of-the-partition-processing-destination"></a>Configurazione della destinazione Elaborazione partizione  
 Nella destinazione Elaborazione partizione viene usata una gestione connessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene le partizioni e i cubi elaborati dalla destinazione. Per altre informazioni, vedere [Gestione connessione Analysis Services](../connection-manager/analysis-services-connection-manager.md).  
  
 Questa destinazione include un input. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor destinazione elaborazione partizione** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione elaborazione partizione &#40;pagina Gestione connessione&#41;](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione elaborazione partizione &#40;pagina Mapping&#41;](../partition-processing-destination-editor-mappings-page.md)  
  
-   [Editor destinazione elaborazione partizione &#40;pagina Avanzate&#41;](../partition-processing-destination-editor-advanced-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate della destinazione elaborazione partizione](partition-processing-destination-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
  

---
title: Destinazione elaborazione dimensione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fadfc8b700ab575582a61388a9b641aa9a01f010
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916001"
---
# <a name="dimension-processing-destination"></a>destinazione elaborazione dimensione
  La destinazione elaborazione dimensione consente di caricare ed elaborare una dimensione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulle dimensioni, vedere [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data).  
  
 La destinazione elaborazione dimensione include le caratteristiche seguenti:  
  
-   Opzioni per l'esecuzione di elaborazioni incrementali, complete o di aggiornamento.  
  
-   Configurazione degli errori, per specificare se l'elaborazione della dimensione deve ignorare gli errori o arrestarsi dopo un numero di errori specificato.  
  
-   Mapping di colonne di input a colonne nelle tabelle delle dimensioni.  
  
 Per altre informazioni sull'elaborazione degli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configurazione della destinazione Elaborazione dimensione  
 La destinazione Elaborazione dimensione utilizza una gestione connessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene le dimensioni elaborate dalla destinazione. Per altre informazioni, vedere [Gestione connessione Analysis Services](../connection-manager/analysis-services-connection-manager.md).  
  
 Questa destinazione include un input. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor destinazione elaborazione dimensione** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione elaborazione dimensione &#40;pagina Gestione connessione&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione elaborazione dimensione &#40;pagina Mapping&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [Editor destinazione elaborazione dimensione &#40;pagina Avanzate&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di programmazione, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](data-flow.md)   
 [Trasformazioni di Integration Services](transformations/integration-services-transformations.md)  
  
  

---
title: Architettura logica (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b6b33ffbf59cf05bc5455d3daac437e9e79407c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165606"
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>Informazioni sull'architettura logica Microsoft OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Usa componenti server e client per fornire l'elaborazione analitica online (OLAP) e funzionalità di data mining per applicazioni di business intelligence:  
  
-   Il componente server di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] viene implementato come un servizio di Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] supporta più istanze nello stesso computer, con ogni istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementata come istanza separata del servizio Windows.  
  
-   I client comunicano con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante lo standard pubblico XML for Analysis (XMLA), un protocollo basato su SOAP per l'esecuzione di comandi e la ricezione di risposte che viene esposto come un servizio Web. Tramite XMLA vengono inoltre offerti modelli a oggetti client a cui è possibile accedere usando un provider gestito, ad esempio ADOMD.NET, o un provider OLE DB nativo.  
  
-   I comandi di query possono essere eseguiti utilizzando le seguenti lingue: SQL; MDX (Multidimensional Expressions), un linguaggio di query standard del settore per l'analisi. o di Data Mining Extensions (DMX), un linguaggio di query standard del settore orientato al data mining. e il linguaggio ASSL (Analysis Services Scripting Language), che consente di gestire gli oggetti di database [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] supporta anche un motore dei cubi locali che permette alle applicazioni in client senza connessione di esplorare dati multidimensionali archiviati localmente. Per altre informazioni, vedere [requisiti di architettura Client per sviluppo Analysis Services](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>In questa sezione  
 **Panoramica dell'architettura logica**  
 [Panoramica dell'architettura logica &#40;Analysis Services - dati multidimensionali&#41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Oggetti server**  
 [Oggetti del server &#40;Analysis Services - dati multidimensionali&#41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti di database**  
 [Oggetti di database &#40;Analysis Services - Dati multidimensionali&#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti Dimension**  
 [Oggetti dimensione &#40;Analysis Services - dati multidimensionali&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti Cube**  
 [Oggetti cubo &#40;Analysis Services - dati multidimensionali&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Sicurezza dall'accesso utente**  
 [Architettura di sicurezza di accesso utente](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sull'architettura Microsoft OLAP](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Architettura fisica &#40;Analysis Services - dati multidimensionali&#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  

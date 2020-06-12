---
title: Architettura logica (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
author: minewiskan
ms.author: owend
ms.openlocfilehash: d93361fb14bc6544ffa7376439c2da0c8e06c3fb
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545953"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>Architettura logica (Analysis Services - Dati multidimensionali)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa componenti server e client per fornire Online Analytical Processing (OLAP) e data mining funzionalità per le applicazioni business intelligence:  
  
-   Il componente server di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] viene implementato come un servizio di Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]supporta più istanze di nello stesso computer, ognuna delle quali è [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementata come istanza separata del servizio Windows.  
  
-   I client comunicano con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante lo standard pubblico XML for Analysis (XMLA), un protocollo basato su SOAP per l'esecuzione di comandi e la ricezione di risposte che viene esposto come un servizio Web. Tramite XMLA vengono inoltre offerti modelli a oggetti client a cui è possibile accedere usando un provider gestito, ad esempio ADOMD.NET, o un provider OLE DB nativo.  
  
-   I comandi di query possono essere eseguiti tramite i linguaggi seguenti: SQL, MDX (Multidimensional Expressions), un linguaggio di query standard del settore per l'analisi, o DMX (Data Mining Extensions), un linguaggio di query standard del settore orientato al data mining. e il linguaggio ASSL (Analysis Services Scripting Language), che consente di gestire gli oggetti di database [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] supporta anche un motore dei cubi locali che permette alle applicazioni in client senza connessione di esplorare dati multidimensionali archiviati localmente. Per ulteriori informazioni, vedere [requisiti dell'architettura client per lo sviluppo di Analysis Services](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 **Panoramica dell'architettura logica**  
 [Cenni preliminari sull'architettura logica &#40;Analysis Services-Dati multidimensionali&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Oggetti Server**  
 [Oggetti server &#40;Analysis Services-Dati multidimensionali&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti di database**  
 [Oggetti di database &#40;Analysis Services - Dati multidimensionali&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti Dimension**  
 [Oggetti Dimension &#40;Analysis Services-Dati multidimensionali&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Oggetti cubo**  
 [Oggetti Cube &#40;Analysis Services-Dati multidimensionali&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Sicurezza dall'accesso utente**  
 [Architettura di sicurezza dall'accesso utente](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sull'architettura Microsoft OLAP](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [Architettura fisica &#40;Analysis Services - Dati multidimensionali&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  

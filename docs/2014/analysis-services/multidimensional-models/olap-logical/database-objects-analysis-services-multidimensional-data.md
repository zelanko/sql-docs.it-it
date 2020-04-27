---
title: Oggetti di database (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], about objects
- SQL Server Analysis Services, objects
- Analysis Services objects, about Analysis Services objects
- SSAS, objects
- Analysis Services objects
- objects [Analysis Services]
ms.assetid: f76d869b-fc1d-4807-9f28-da09c7be382d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39116b4bf8c4c361dfa82ca0d8a38dc6977de217
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62725656"
---
# <a name="database-objects-analysis-services---multidimensional-data"></a>Oggetti di database (Analysis Services - Dati multidimensionali)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Un' [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] istanza di contiene gli assembly e gli oggetti di database da utilizzare con Online Analytical Processing (OLAP) e data mining.  
  
-   I database contengono oggetti OLAP e di data mining, ad esempio origini dei dati, viste origine dati, cubi, misure, gruppi di misure, dimensioni, attributi, gerarchie, strutture di data mining, modelli di data mining e ruoli.  
  
-   Gli assembly contengono le funzioni definite dall'utente che estendono la funzionalità delle funzioni intrinseche disponibili nei linguaggi MDX (Multidimensional Expressions) e DMX (Data Mining Extensions).  
  
 L'oggetto <xref:Microsoft.AnalysisServices.Database> è il contenitore per tutti gli oggetti dati necessari per un progetto Business Intelligence, ad esempio cubi, dimensioni e strutture di data mining OLAP, e per gli oggetti di supporto, ad esempio <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Account> e <xref:Microsoft.AnalysisServices.Role>.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Database> fornisce l'accesso agli oggetti e agli attributi che includono quanto segue:  
  
-   Tutti i cubi a cui è possibile accedere, sotto forma di raccolta.  
  
-   Tutte le dimensioni a cui è possibile accedere, sotto forma di raccolta.  
  
-   Tutte le strutture di data mining a cui è possibile accedere, sotto forma di raccolta.  
  
-   Tutte le origini dati e le viste origine dati, sotto forma di due raccolte.  
  
-   Tutti i ruoli e le autorizzazioni per il database, sotto forma di due raccolte.  
  
-   I valori delle regole di confronto per il database.  
  
-   Le dimensioni stimate del database.  
  
-   Il valore della lingua del database.  
  
-   L'impostazione di visibilità per il database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Negli argomenti seguenti vengono descritti gli oggetti condivisi sia dalle caratteristiche OLAP che da quelle di data mining in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Origini dati nei modelli multidimensionali](../data-sources-in-multidimensional-models.md)|Descrive un'origine dei dati in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Viste origine dati in modelli multidimensionali](../data-source-views-in-multidimensional-models.md)|Descrive un modello di dati logico basato su una o più origini dei dati in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Cubi nei modelli multidimensionali](../cubes-in-multidimensional-models.md)|Descrive i cubi e gli oggetti dei cubi, inclusi gruppi di misure, misure, relazioni tra l'utilizzo delle dimensioni, calcoli, indicatori di prestazioni chiavi, azioni, traduzioni, partizioni e prospettive.|  
|[Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|Descrive le dimensioni e gli oggetti delle dimensioni, inclusi attributi, relazioni tra attributi, gerarchie, livelli e membri.|  
|[Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../data-mining/mining-structures-analysis-services-data-mining.md)|Descrive le strutture e gli oggetti di data mining, inclusi i modelli di data mining.|  
|[Ruoli di sicurezza &#40;Analysis Services - Dati multidimensionali&#41;](security-roles-analysis-services-multidimensional-data.md)|Descrive un ruolo, ovvero il meccanismo di sicurezza utilizzato per controllare l'accesso agli oggetti in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gestione di assembly di modelli multidimensionali](../multidimensional-model-assemblies-management.md)|Descrive un assembly, ovvero una raccolta di funzioni definite dall'utente utilizzate per estendere i linguaggi MDX e DMX in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Vedi anche  
 [Origini dati supportate &#40;SSAS multidimensionale&#41;](../supported-data-sources-ssas-multidimensional.md)   
 [Soluzioni di modelli multidimensionali &#40;SSAS&#41;](../multidimensional-model-solutions-ssas.md)   
 [Soluzioni di data mining](../../data-mining/data-mining-solutions.md)  
  
  

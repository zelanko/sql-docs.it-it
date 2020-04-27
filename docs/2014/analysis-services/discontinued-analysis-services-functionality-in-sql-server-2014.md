---
title: Funzionalità di Analysis Services sospese in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 616c39d03ff8081c209a80dcca912d831bcef1ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081680"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>Funzionalità di Analysis Services non più utilizzate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non più disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-sssql14"></a>Funzionalità non più disponibili in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|Category|Funzionalità deprecata|Sostituzione|  
|--------------|------------------------|-----------------|  
|Cubi locali|Proprietà della stringa di connessione InsertInto|La sintassi della stringa di connessione originale per il popolamento di cubi locali viene sostituita dall'istruzione Create Global Cube. Per ulteriori informazioni, vedere [istruzione CREATE GLOBAL CUBE &#40;&#41;MDX ](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Cubi locali|Proprietà della stringa di connessione CreateCube|La sintassi della stringa di connessione originale per il popolamento di cubi locali viene sostituita dall'istruzione Create Global Cube. Per ulteriori informazioni, vedere [istruzione CREATE GLOBAL CUBE &#40;&#41;MDX ](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Data Mining|SQL Server 2000 PMML|Tramite la funzionalità SQL Server 2000 PMML veniva prodotto un formato di PMML con estensioni proprietarie per supportare funzionalità univoche fornite da algoritmi di Data mining non disponibili nella specifica PMML. In SQL Server 2005, tramite Analysis Services è stato effettuare l'aggiornamento della funzionalità PMML allo standard più recente PMML 2.1. Di conseguenza, le estensioni proprietarie aggiunte in SQL Server 2000 non sono più necessarie, sebbene siano ancora supportate in questa versione.|  
|Istruzione MDX|Istruzione Create Action|Questa istruzione è stata inclusa per compatibilità con le versioni precedenti. Viene sostituita dall'oggetto Azione. Per ulteriori informazioni su come creare azioni nelle versioni recenti di, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]vedere [azioni &#40;Analysis Services-&#41;di dati multidimensionali ](multidimensional-models/actions-analysis-services-multidimensional-data.md).|  
  
## <a name="discontinued-features-in-previous-releases"></a>Funzionalità non più supportate delle versioni precedenti  
 La Migrazione guidata, utilizzata per la migrazione dei database di SQL Server 2000 Analysis Services a versioni più recenti non è più disponibile in quanto SQL Server 2000 non è più supportato.  
  
 Anche la libreria DSO (Decision Support Objects), che forniva compatibilità con i database di SQL Server 2000 Analysis Services non è più disponibile e non fa più parte di SQL Server.  
  
## <a name="see-also"></a>Vedi anche  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  

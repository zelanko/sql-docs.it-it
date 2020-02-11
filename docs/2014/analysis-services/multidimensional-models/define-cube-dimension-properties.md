---
title: Definire le proprietà delle dimensioni del cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecf47eff045aa379a8e67332a82b2045a8569a2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075685"
---
# <a name="define-cube-dimension-properties"></a>Definire le proprietà delle dimensioni del cubo
  Una dimensione del cubo è un'istanza della dimensione del database all'interno di un cubo. Una dimensione del database può essere utilizzata in più cubi e più dimensioni del cubo possono essere basate su una singola dimensione del database. Nella tabella seguente vengono descritte le proprietà della dimensione di un cubo.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`AllMemberAggregationUsage`|Controlla il modo in cui le aggregazioni sono progettate dalla [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]finestra di progettazione delle aggregazioni in. I possibili valori della proprietà sono i seguenti:<br /><br /> **Completo**: ogni aggregazione del cubo deve includere il membro totale.<br /><br /> **None**: nessuna aggregazione per il cubo può includere il membro totale. Si tratta del valore predefinito.<br /><br /> Senza **restrizioni**: nessuna restrizione viene posizionata nella finestra di progettazione delle aggregazioni.<br /><br /> **Impostazione predefinita**: la stessa funzionalità di senza restrizioni.|  
|`Description`|Fornisce un nome descrittivo per il livello.|  
|`DimensionID`|Contiene l'identificatore univoco (ID) della dimensione del database.|  
|`HierarchyUniqueNameStyle`|Determina il modo in cui vengono generati i nomi univoci delle gerarchie contenute all'interno della dimensione del cubo. I possibili valori della proprietà sono i seguenti:<br /><br /> 
  `IncludeDimensionName`: il nome della dimensione fa parte del nome della gerarchia. Si tratta del valore predefinito.<br /><br /> 
  `ExcludeDimensionName`: il nome della dimensione non fa parte del nome della gerarchia.|  
|`ID`|Contiene l'identificatore univoco della dimensione del cubo.|  
|`MemberUniqueNameStyle`|Determina il modo in cui vengono generati i nomi univoci dei membri delle gerarchie contenuti all'interno della dimensione del cubo. I possibili valori della proprietà sono i seguenti:<br /><br /> 
  `Native`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automaticamente i nomi univoci dei membri. Si tratta del valore predefinito.<br /><br /> 
  `NamePath`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un nome composto costituito dal nome di ogni livello e dalla didascalia del membro.|  
|`Name`|Contiene il nome descrittivo della dimensione del cubo. Per impostazione predefinita, il nome di una dimensione del cubo è uguale al nome della dimensione del database, a meno che non sia già stata definita un'altra dimensione del cubo con lo stesso nome.|  
|`Visible`|Determina se la dimensione del cubo è visibile. Il valore predefinito è `True`.|  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni &#40;Analysis Services Dati multidimensionali&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  

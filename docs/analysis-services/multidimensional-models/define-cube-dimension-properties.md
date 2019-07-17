---
title: Definire le proprietà di dimensione cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4401055a15afe73a1f33ee43354f7ee45f887a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178756"
---
# <a name="define-cube-dimension-properties"></a>Definire le proprietà delle dimensioni del cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una dimensione del cubo è un'istanza della dimensione del database all'interno di un cubo. Una dimensione del database può essere utilizzata in più cubi e più dimensioni del cubo possono essere basate su una singola dimensione del database. Nella tabella seguente vengono descritte le proprietà della dimensione di un cubo.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|Controlla il modo in cui vengono progettate le aggregazioni con Progettazione aggregazioni in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. I possibili valori della proprietà sono i seguenti:<br /><br /> **Full**: Ogni aggregazione del cubo deve includere il membro Totale.<br /><br /> **Nessuno**: Nessuna aggregazione del cubo può includere il membro totale. Rappresenta il valore predefinito.<br /><br /> **Unrestricted**: Non esistono restrizioni in Progettazione aggregazioni.<br /><br /> **Default**: La stessa funzionalità di senza restrizioni.|  
|**Descrizione**|Fornisce un nome descrittivo per il livello.|  
|**DimensionID**|Contiene l'identificatore univoco (ID) della dimensione del database.|  
|**HierarchyUniqueNameStyle**|Determina il modo in cui vengono generati i nomi univoci delle gerarchie contenute all'interno della dimensione del cubo. I possibili valori della proprietà sono i seguenti:<br /><br /> **IncludeDimensionName**:<br />                    Il nome della dimensione fa parte del nome della gerarchia. Rappresenta il valore predefinito.<br /><br /> **ExcludeDimensionName**:<br />                    Il nome della dimensione non fa parte del nome della gerarchia.|  
|**ID**|Contiene l'identificatore univoco della dimensione del cubo.|  
|**MemberUniqueNameStyle**|Determina il modo in cui vengono generati i nomi univoci dei membri delle gerarchie contenuti all'interno della dimensione del cubo. I possibili valori della proprietà sono i seguenti:<br /><br /> **Native**:<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automaticamente i nomi univoci dei membri. Rappresenta il valore predefinito.<br /><br /> **NamePath**: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un nome composto costituito dal nome di ogni livello e dalla didascalia del membro.|  
|**Name**|Contiene il nome descrittivo della dimensione del cubo. Per impostazione predefinita, il nome di una dimensione del cubo è uguale al nome della dimensione del database, a meno che non sia già stata definita un'altra dimensione del cubo con lo stesso nome.|  
|**Visible**|Determina se la dimensione del cubo è visibile. Il valore predefinito è **True**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  

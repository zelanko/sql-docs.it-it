---
title: Definire le proprietà di attributo del cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e84c49055a1fdb5b11487ab17af19762f86686c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726415"
---
# <a name="define-cube-attribute-properties"></a>Definire le proprietà degli attributi dei cubi
  Le proprietà degli attributi dei cubi consentono di specificare impostazioni univoche per gli attributi delle dimensioni dei cubi basate sulla stessa dimensione di database. Nella tabella seguente vengono descritte le proprietà di un attributo del cubo.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`AggregationUsage`|Specifica come verranno progettate le aggregazioni per l'attributo tramite la Progettazione guidata aggregazioni. I possibili valori della proprietà sono i seguenti:<br /><br /> `Default`: Valore predefinito. Nella Progettazione guidata aggregazioni viene applicata una regola predefinita in base al tipo di attributo (Full per le chiavi, Unrestricted negli altri casi).<br /><br /> `None`: Nessuna aggregazione del cubo deve includere l'attributo.<br /><br /> `Unrestricted`: Non esistono restrizioni nella progettazione guidata aggregazioni.<br /><br /> `Full`: Ogni aggregazione del cubo deve includere l'attributo.|  
|`AttributeHierarchyEnabled`|Identifica se la gerarchia dell'attributo è abilitata in questa dimensione del cubo. Questa proprietà consente di disabilitare le gerarchie in cubi o ruoli di dimensione specifici. Questa impostazione non produce alcun effetto se la gerarchia dell'attributo sottostante è disabilitata. Il valore predefinito è `True`.|  
|`OptimizedState`|Indica se la gerarchia dell'attributo è ottimizzata in questa dimensione del cubo. Questa proprietà consente di ottimizzare le gerarchie in cubi o ruoli di dimensione specifici. Questa impostazione non produce alcun effetto se la gerarchia dell'attributo sottostante non è ottimizzata. I possibili valori della proprietà sono i seguenti:<br /><br /> `FullyOptimized`: Valore predefinito. L'istanza compila indici per la gerarchia allo scopo di migliorare le prestazioni di esecuzione delle query. Rappresenta il valore predefinito.<br /><br /> `NotOptimized`: L'istanza non compila indici aggiuntivi.|  
|`AttributeHierarchyVisible`|Indica se la gerarchia dell'attributo è visibile in questa dimensione del cubo. Questa proprietà consente di rendere visibili le gerarchie in cubi o ruoli di dimensione specifici. Questa impostazione non produce alcun effetto se la gerarchia dell'attributo sottostante non è visibile. Il valore predefinito è `True`.|  
|`AttributeID`|Contiene l'identificatore univoco (ID) dell'attributo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Definire le proprietà delle dimensioni del cubo](define-cube-dimension-properties.md)   
 [Definire le proprietà della gerarchia del cubo](define-cube-hierarchy-properties.md)  
  
  

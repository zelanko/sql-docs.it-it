---
title: Definire le proprietà della gerarchia del cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ace708cc4ee09295380b814bbf21f5a1c350974
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075710"
---
# <a name="define-cube-hierarchy-properties"></a>Definire le proprietà della gerarchia del cubo
  Le proprietà delle gerarchie dei cubi consentono di specificare impostazioni univoche per gerarchie definite dall'utente in dimensioni del cubo basate sulla stessa dimensione del database. Nella tabella seguente vengono descritte le proprietà della gerarchia di un cubo.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`Enabled`|Determina l'eventuale abilitazione della gerarchia per la dimensione del cubo.|  
|`HierarchyID`|Contiene l'identificatore univoco (ID) della gerarchia.|  
|`OptimizedState`|Determina il livello di ottimizzazione applicato alla gerarchia. I possibili valori della proprietà sono i seguenti:<br /><br /> `FullyOptimized`: l'istanza compila indici per la gerarchia allo scopo di migliorare le prestazioni delle query. Questo è il valore predefinito.<br /><br /> `NotOptimized`: l'istanza non compila indici aggiuntivi.|  
|`Visible`|Determina la visibilità della gerarchia del cubo. Il valore predefinito è `True`.|  
  
## <a name="see-also"></a>Vedi anche  
 [Gerarchie definite dall'utente](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  

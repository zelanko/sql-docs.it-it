---
title: Oggetti ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d568ca20cca6c12a04c0f3d54a2c134d59a0d7fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930578"
---
# <a name="ado-md-objects"></a>Oggetti ADO MD

|||  
|-|-|  
|[Asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Rappresenta un asse posizionale o di filtro di un oggetto Cell, contenente i membri selezionati di una o più dimensioni.|  
|[Catalogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contiene informazioni di schema multidimensionali, ovvero cubi e dimensioni sottostanti, gerarchie, livelli e membri, specifiche di un provider di dati multidimensionali (MDP).|  
|[Cell (Cella)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Rappresenta i dati in corrispondenza dell'intersezione tra le coordinate dell'asse, contenute in un oggetto Cell.|  
|[Celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Rappresenta i risultati di una query multidimensionale. Si tratta di una raccolta di celle selezionate da cubi o altri celle.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Rappresenta un cubo da uno schema multidimensionale, contenente un set di dimensioni correlate.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Rappresenta una delle dimensioni di un cubo multidimensionale che contiene una o più gerarchie di membri.|  
|[Gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Rappresenta un modo in cui i membri di una dimensione possono essere aggregati o sottoposti a rollup. Una dimensione può essere aggregata in una o più gerarchie.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contiene un set di membri, ognuno dei quali ha lo stesso rango all'interno di una gerarchia.|  
|[Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Rappresenta un membro di un livello in un cubo, gli elementi figlio di un membro di un livello o un membro di una posizione lungo un asse di un insieme di celle.|  
|[Posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Rappresenta un set di uno o più membri di dimensioni diverse che definiscono un punto lungo un asse.|  
  
 Inoltre, l'oggetto **Catalogo** è connesso a un oggetto **connessione** ADO, incluso nella libreria ADO standard:  
  
|Oggetto|Descrizione|  
|------------|-----------------|  
|[Connessione](../../../ado/reference/ado-api/connection-object-ado.md)|Rappresenta una connessione aperta a un'origine dati.|  
  
 Le relazioni tra questi oggetti sono illustrate nel [modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Molti oggetti ADO MD possono essere contenuti in una raccolta corrispondente. Un oggetto [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) , ad esempio, può essere contenuto in una raccolta [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) di un **Catalogo**. Per ulteriori informazioni, vedere [ADO MD Collections](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Esempi di codice ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Raccolte di ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD costanti enumerate](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Metodi di ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Proprietà ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)

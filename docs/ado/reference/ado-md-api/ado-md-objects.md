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
manager: jroth
ms.openlocfilehash: c06214d23441782cbe5e14433b16928224d5d48c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709845"
---
# <a name="ado-md-objects"></a>Oggetti ADO MD

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Rappresenta un posizionali o asse di filtro di un set di celle, che contiene i membri selezionati di una o più dimensioni.|  
|[Catalogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contiene informazioni sullo schema multidimensionale (vale a dire, i cubi e sottostante dimensioni, gerarchie, livelli e membri) specifiche di un provider di dati multidimensionali (dati Multidimensionali).|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Rappresenta i dati in corrispondenza dell'intersezione di coordinate assiali, contenuti in un set di celle.|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Rappresenta i risultati di una query multidimensionale. È una raccolta di celle selezionate da cubi o altri set di celle.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Rappresenta un cubo da uno schema multidimensionale, contenente un set di dimensioni correlate.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Rappresenta una delle dimensioni di un cubo multidimensionale, contenente una o più gerarchie dei membri.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Rappresenta uno dei modi in cui i membri di una dimensione possono essere aggregati o "raggruppati". Una dimensione può essere aggregata una o più gerarchie.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contiene un set di membri, ognuno dei quali ha lo stesso rango all'interno di una gerarchia.|  
|[Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Rappresenta un membro di un livello in un cubo, gli elementi figlio di un membro di un livello o un membro di una posizione lungo un asse di un set di celle.|  
|[Posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Rappresenta un set di uno o più membri di dimensioni diverse che definisce un punto lungo un asse.|  
  
 Inoltre, il **catalogo** l'oggetto è connesso a un oggetto ADO **connessione** oggetto, che è incluso con la libreria ADO standard:  
  
|Object|Descrizione|  
|------------|-----------------|  
|[Connessione](../../../ado/reference/ado-api/connection-object-ado.md)|Rappresenta una connessione aperta a un'origine dati.|  
  
 Le relazioni tra tali oggetti sono illustrate nella [modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Numero di oggetti ADO MD può essere contenuti in una raccolta corrispondente. Ad esempio, un [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) oggetto può essere contenuto in un [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) raccolta di un **Catalog**. Per altre informazioni, vedere [raccolte ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API di ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Esempi di codice ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Raccolte ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [Costanti enumerate ADO MD](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Metodi ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Proprietà di ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)

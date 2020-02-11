---
title: Oggetto Level (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a44060ae4ffd9399c34d4cd8133f5ad7404ed5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949609"
---
# <a name="level-object-ado-md"></a>Oggetto Level (ADO MD)
Contiene un set di membri, ognuno dei quali ha lo stesso rango all'interno di una gerarchia.  
  
## <a name="remarks"></a>Osservazioni  
 Con le raccolte e le proprietà di un oggetto **livello** , è possibile eseguire le operazioni seguenti:  
  
-   Identificare il **livello** con le proprietà [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Restituisce una stringa da usare quando si Visualizza il **livello** con la proprietà [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Restituisce una stringa significativa che descrive il **livello** con la proprietà [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Restituire gli oggetti [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) che costituiscono il **livello** con la raccolta [Members](../../../ado/reference/ado-md-api/members-collection-ado-md.md) .  
  
-   Restituisce il numero di livelli dalla radice del **livello** con la proprietà [Depth](../../../ado/reference/ado-md-api/depth-property-ado-md.md) .  
  
-   Utilizzare la raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) ADO standard per ottenere informazioni aggiuntive sull'oggetto **Level** .  
  
 La raccolta **Properties** contiene proprietà fornite dal provider. Nella tabella seguente sono elencate le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare a seconda dell'implementazione del provider. Per un elenco più completo delle proprietà disponibili, vedere la documentazione relativa al provider.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Nome del catalogo a cui appartiene il cubo.|  
|CubeName|Nome del cubo.|  
|Descrizione|Descrizione significativa del livello.|  
|DimensionUniqueName|Nome non ambiguo della [dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Nome non ambiguo della gerarchia.|  
|LevelCaption|Etichetta o didascalia associata al livello.|  
|LevelCardinality|Numero di membri nel livello.|  
|LevelGUID|GUID del livello.|  
|LevelName|Nome del livello.|  
|LevelNumber|Distanza tra il livello e la radice della gerarchia.|  
|LevelType|Tipo di livello.|  
|LevelUniqueName|Nome non ambiguo del livello.|  
|SchemaName|Nome dello schema a cui appartiene il cubo.|  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Raccolta levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

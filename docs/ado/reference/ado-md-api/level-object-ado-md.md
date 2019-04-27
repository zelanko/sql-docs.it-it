---
title: Il livello di oggetto (ADO MD) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 27e789c4eb34ed275d6f18f62325287febb73422
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740191"
---
# <a name="level-object-ado-md"></a>Oggetto Level (ADO MD)
Contiene un set di membri, ognuno dei quali ha lo stesso rango all'interno di una gerarchia.  
  
## <a name="remarks"></a>Note  
 Con le raccolte e le proprietà di un **livello** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Identificare il **livello** con il [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) proprietà.  
  
-   Restituire una stringa da usare quando vengono visualizzati i **livello** con il [didascalia](../../../ado/reference/ado-md-api/caption-property-ado-md.md) proprietà.  
  
-   Restituisce una stringa significativa che descrive la **livello** con il [descrizione](../../../ado/reference/ado-md-api/description-property-ado-md.md) proprietà.  
  
-   Restituire il [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) degli oggetti che compongono il **a livello** con il [membri](../../../ado/reference/ado-md-api/members-collection-ado-md.md) raccolta.  
  
-   Restituisce il numero di livelli dalla radice del **livello** con il [profondità](../../../ado/reference/ado-md-api/depth-property-ado-md.md) proprietà.  
  
-   Utilizzare ADO standard [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme per ottenere informazioni aggiuntive sul **livello** oggetto.  
  
 Il **proprietà** raccolta contiene le proprietà specifiche del provider. La tabella seguente elenca le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare in base all'implementazione del provider. Vedere la documentazione per il provider per un elenco completo delle proprietà disponibili.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Il nome del catalogo a cui appartiene il cubo.|  
|CubeName|Nome del cubo.|  
|Descrizione|Una descrizione significativa del livello.|  
|DimensionUniqueName|Nome univoco della [dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Nome univoco della gerarchia.|  
|LevelCaption|Etichetta o didascalia associata al livello.|  
|LevelCardinality|Numero di membri nel livello.|  
|LevelGUID|Il GUID del livello.|  
|LevelName|Nome del livello.|  
|LevelNumber|La distanza tra il livello e la radice della gerarchia.|  
|LevelType|Tipo di livello.|  
|LevelUniqueName|Nome univoco del livello.|  
|SchemaName|Il nome dello schema a cui appartiene il cubo.|  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Raccolta Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

---
title: Oggetto Dimension (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d5b475600ef211d8203a64a1a2c6d917bb99914
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764302"
---
# <a name="dimension-object-ado-md"></a>Oggetto Dimension (ADO MD)
Rappresenta una delle dimensioni di un cubo multidimensionale che contiene una o più gerarchie di membri.  
  
## <a name="remarks"></a>Commenti  
 Con le raccolte e le proprietà di un oggetto **dimensione** , è possibile eseguire le operazioni seguenti:  
  
-   Identificare la **dimensione** con le proprietà [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Restituisce una stringa significativa che descrive la **dimensione** con la proprietà [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Restituisce gli oggetti [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) che compongono la **dimensione** con la raccolta [gerarchie](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) .  
  
-   Utilizzare la raccolta di [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) ADO standard per ottenere informazioni aggiuntive sull'oggetto **Dimension** .  
  
 La raccolta **Properties** contiene proprietà fornite dal provider. Nella tabella seguente sono elencate le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare a seconda dell'implementazione del provider. Per un elenco più completo delle proprietà disponibili, vedere la documentazione relativa al provider.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Nome del catalogo a cui appartiene il cubo.|  
|CubeName|Nome del cubo.|  
|DefaultHierarchy|Nome univoco della gerarchia predefinita.|  
|Descrizione|Descrizione significativa del cubo.|  
|DimensionCaption|Etichetta o didascalia associata alla dimensione.|  
|DimensionCardinality|Numero di membri nella dimensione.|  
|DimensionGUID|GUID della dimensione.|  
|DimensionName|Nome della dimensione.|  
|DimensionOrdinal|Numero ordinale della dimensione tra il gruppo di dimensioni che formano il cubo.|  
|DimensionType|Tipo di dimensione.|  
|DimensionUniqueName|Nome non ambiguo della dimensione.|  
|SchemaName|Nome dello schema a cui appartiene il cubo.|  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Raccolta Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Raccolta gerarchie (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

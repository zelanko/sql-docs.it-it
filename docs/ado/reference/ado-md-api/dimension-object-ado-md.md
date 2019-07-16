---
title: Dimensioni oggetto (ADO MD) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7a13ad87d56f5e7855070d8fe577bb408d6ce9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938533"
---
# <a name="dimension-object-ado-md"></a>Oggetto Dimension (ADO MD)
Rappresenta una delle dimensioni di un cubo multidimensionale, contenente una o più gerarchie dei membri.  
  
## <a name="remarks"></a>Note  
 Con le raccolte e le proprietà di un **dimensione** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Identificare le **dimensione** con il [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) proprietà.  
  
-   Restituisce una stringa significativa che descrive la **dimensione** con il [descrizione](../../../ado/reference/ado-md-api/description-property-ado-md.md) proprietà.  
  
-   Restituisce il [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) degli oggetti che compongono il **dimensione** con il [gerarchie](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) raccolta.  
  
-   Usare ADO standard [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme per ottenere informazioni aggiuntive sul **dimensione** oggetto.  
  
 Il **proprietà** raccolta contiene le proprietà specifiche del provider. La tabella seguente elenca le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare in base all'implementazione del provider. Vedere la documentazione per il provider per un elenco completo delle proprietà disponibili.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Il nome del catalogo a cui appartiene il cubo.|  
|CubeName|Nome del cubo.|  
|DefaultHierarchy|Il nome univoco della gerarchia predefinita.|  
|Descrizione|Una descrizione significativa del cubo.|  
|DimensionCaption|Etichetta o didascalia associata alla dimensione.|  
|DimensionCardinality|Il numero di membri nella dimensione.|  
|DimensionGUID|Il GUID della dimensione.|  
|DimensionName|Nome della dimensione.|  
|DimensionOrdinal|Il numero ordinale della dimensione all'interno del gruppo di dimensioni che costituiscono il cubo.|  
|DimensionType|Il tipo di dimensione.|  
|DimensionUniqueName|Nome univoco della dimensione.|  
|SchemaName|Il nome dello schema a cui appartiene il cubo.|  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Raccolta Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Raccolta hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

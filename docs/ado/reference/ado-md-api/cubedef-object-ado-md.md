---
title: Oggetto CubeDef (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3831c78380d8ae34e1dab74e92514c7d84136988
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709382"
---
# <a name="cubedef-object-ado-md"></a>Oggetto CubeDef (ADO MD)
Rappresenta un cubo da uno schema multidimensionale, contenente un set di dimensioni correlate.  
  
## <a name="remarks"></a>Note  
 Con le raccolte e le proprietà di un **CubeDef** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Identificare un **CubeDef** con il [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) proprietà.  
  
-   Restituisce una stringa che descrive il cubo con le [descrizione](../../../ado/reference/ado-md-api/description-property-ado-md.md) proprietà.  
  
-   Restituisce le dimensioni che costituiscono il cubo con le [dimensioni](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) raccolta.  
  
-   Ottenere informazioni aggiuntive sui **CubeDef** con l'oggetto ADO standard [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
 Il **proprietà** raccolta contiene le proprietà specifiche del provider. La tabella seguente elenca le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare in base all'implementazione del provider. Vedere la documentazione per il provider per un elenco completo delle proprietà disponibili.  
  
|nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Il nome del catalogo a cui appartiene il cubo.|  
|CreatedOn|Data e ora della creazione del cubo.|  
|CubeGUID|Cubo di GUID.|  
|CubeName|Nome del cubo.|  
|CubeType|Tipo del cubo.|  
|DataUpdatedBy|ID utente della persona che esegue l'ultimo aggiornamento dei dati.|  
|Descrizione|Una descrizione significativa del cubo.|  
|LastSchemaUpdate|Data e ora dell'ultimo aggiornamento dello schema.|  
|SchemaName|Il nome dello schema a cui appartiene il cubo.|  
|SchemaUpdatedBy|ID utente della persona che esegue l'ultimo aggiornamento dello schema.|  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Oggetto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs Collection (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Dimensions Collection (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

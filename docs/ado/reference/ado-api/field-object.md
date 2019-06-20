---
title: Oggetto Field | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9b57ce165337dc2cef87daf8c2a835bde0c5f85b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697861"
---
# <a name="field-object"></a>Oggetto Field
Rappresenta una colonna di dati con un tipo di dati comune.  
  
## <a name="remarks"></a>Note  
 Ciascuna **campo** corrisponde a una colonna in oggetto il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Si utilizza il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà di **campo** oggetti da impostare o restituire i dati per il record corrente. A seconda della funzionalità espone il provider, alcune raccolte, metodi o proprietà di un **campo** oggetto potrebbe non essere disponibile.  
  
 Con le raccolte, i metodi e proprietà di un **campo** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Restituire il nome di un campo con il [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà.  
  
-   Visualizzare o modificare i dati nel campo con il **valore** proprietà. **Valore** è la proprietà predefinita di **campo** oggetto.  
  
-   Restituisce le caratteristiche di base di un campo con il [tipo](../../../ado/reference/ado-api/type-property-ado.md), [precisione](../../../ado/reference/ado-api/precision-property-ado.md), e [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) proprietà.  
  
-   Restituire la dimensione dichiarata di un campo con il [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) proprietà.  
  
-   Restituisce le dimensioni effettive dei dati in un determinato campo con il [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) proprietà.  
  
-   Determinare i tipi di funzionalità sono supportati per un determinato campo con il [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà e [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
-   Modificare i valori dei campi che contengono dati long carattere o binari long con il [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) metodi.  
  
-   Se il provider supporta aggiornamenti batch, risolvere eventuali discrepanze nei valori dei campi durante l'aggiornamento in batch con il [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) e [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) proprietà.  
  
 Tutte le proprietà dei metadati (**Name**, **tipo**, **DefinedSize**, **precisione**, e **NumericScale**) sono disponibili prima di aprire la **campo** dell'oggetto **Recordset**. Impostarli in quel momento è utile per la creazione dinamica di form.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Campo oggetto proprietà, metodi ed eventi](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Fields Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

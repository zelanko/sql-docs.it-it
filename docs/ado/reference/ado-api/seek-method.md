---
title: Metodo Seek | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e2ee81ac2ede53eb4fdbcfe8d3b5987db96f1ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917010"
---
# <a name="seek-method"></a>Metodo Seek
Esegue una ricerca nell'indice di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per individuare rapidamente la riga che corrisponde ai valori specificati e imposta la posizione della riga corrente su quella riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parametri  
 *KeyValues*  
 Matrice di valori **Variant** . Un indice è costituito da una o più colonne e la matrice contiene un valore da confrontare con ogni colonna corrispondente.  
  
 *SeekOption*  
 Valore [SeekEnum](../../../ado/reference/ado-api/seekenum.md) che specifica il tipo di confronto da eseguire tra le colonne dell'indice e i relativi *valori*di base.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il metodo **Seek** insieme alla proprietà [index](../../../ado/reference/ado-api/index-property.md) se il provider sottostante supporta indici nell'oggetto **Recordset** . Utilizzare il metodo [Supports](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** per determinare se il provider sottostante supporta **Seek**e il metodo **Supports (adIndex)** per determinare se il provider supporta gli indici. Ad esempio, il [provider di OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) supporta la **ricerca** e l' **Indice**.  
  
 Se **Seek** non trova la riga desiderata, non si verifica alcun errore e la riga viene posizionata alla fine del **Recordset**. Impostare la proprietà **index** sull'indice desiderato prima di eseguire questo metodo.  
  
 Questo metodo è supportato solo con i cursori sul lato server. La ricerca non è supportata quando il valore della proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) dell'oggetto **Recordset** è **adUseClient**.  
  
 Questo metodo può essere utilizzato solo quando l'oggetto **Recordset** è stato aperto con un valore [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) di **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Seek e proprietà index (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Esempio di metodo Seek e proprietà index (VC + +)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Metodo Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Proprietà Index](../../../ado/reference/ado-api/index-property.md)

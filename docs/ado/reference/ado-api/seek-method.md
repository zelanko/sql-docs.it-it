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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917010"
---
# <a name="seek-method"></a>Metodo Seek
Cerca l'indice di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per individuare rapidamente la riga che corrisponde ai valori specificati e cambia la posizione della riga corrente di tale riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parametri  
 *KeyValues*  
 Matrice di **Variant** valori. Un indice è costituito da una o più colonne e la matrice contiene un valore da confrontare con ogni colonna corrispondente.  
  
 *SeekOption*  
 Oggetto [SeekEnum](../../../ado/reference/ado-api/seekenum.md) valore che specifica il tipo di confronto da eseguire tra le colonne dell'indice e il corrispondente *KeyValues*.  
  
## <a name="remarks"></a>Note  
 Usare la **Seek** metodo in combinazione con la [indice](../../../ado/reference/ado-api/index-property.md) proprietà se il provider sottostante supporta gli indici per il **Recordset** oggetto. Usare la [supporta](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** metodo per determinare se il provider sottostante supporta **Seek**e il **Supports (adIndex)** metodo per determinare se il provider supporta gli indici. (Ad esempio, il [Provider OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) supporta **Seek** e **indice**.)  
  
 Se **Seek** non trovare la riga desiderata, nessun errore si verifica e la riga è posizionato alla fine delle **Recordset**. Impostare il **indice** proprietà per l'indice desiderato prima di eseguire questo metodo.  
  
 Questo metodo è supportato solo con i cursori sul lato server. Seek non è supportata quando la **Recordset** dell'oggetto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valore della proprietà **adUseClient**.  
  
 Questo metodo può essere utilizzato quando la **Recordset** oggetto è stato aperto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) pari a **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Seek e esempio di proprietà indice (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Metodo Seek e esempio di proprietà Index (VC + +)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Metodo Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Proprietà Index](../../../ado/reference/ado-api/index-property.md)

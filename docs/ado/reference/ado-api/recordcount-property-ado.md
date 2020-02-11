---
title: Proprietà RecordCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7304062298a95406a223ba58026379a3bebf392f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931475"
---
# <a name="recordcount-property-ado"></a>Proprietà RecordCount (ADO)

Indica il numero di record in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .
  
## <a name="return-value"></a>Valore restituito

Restituisce un valore **Long** che indica il numero di record nel **Recordset**.
  
## <a name="remarks"></a>Osservazioni

Utilizzare la proprietà **RecordCount** per determinare il numero di record presenti in un oggetto **Recordset** . La proprietà restituisce-1 quando ADO non è in grado di determinare il numero di record o se il tipo di cursore o il provider non supporta **RecordCount**. La lettura della proprietà **RecordCount** in un **Recordset** chiuso causa un errore.

#### <a name="bookmarks-or-approximate-positioning"></a>Segnalibri o posizionamento approssimativo

Se *l'oggetto recordset supporta* segnalibri o posizionamento approssimativo, questa proprietà restituisce il numero esatto di record nel recordset. Questa proprietà restituisce il numero esatto indipendentemente dal fatto che il recordset sia stato popolato completamente.

Al contrario, se l'oggetto recordset non *supporta* segnalibri o posizionamento approssimativo, l'accesso a questa proprietà potrebbe essere un svuotamento significativo delle risorse. Lo svuotamento si verifica perché tutti i record devono essere recuperati e conteggiati per restituire un valore RecordCount preciso.

- **adBookmark** correlate ai segnalibri.
- **adApproxPosition** è correlato al posizionamento approssimativo.

> [!NOTE]
> Nelle versioni ADO 2,8 e precedenti, il provider SQLOLEDB recupera tutti i record quando viene usato un cursore sul lato server, nonostante il fatto che restituisca **true** per entrambi i **supporti (AdApproxPosition)** e **supporta (adBookmark)**.
  
Il tipo di cursore dell'oggetto **Recordset** influiscono sulla possibilità di determinare il numero di record. La proprietà **RecordCount** restituirà-1 per un cursore di sola trasmissione. conteggio effettivo per un cursore statico o keyset; e-1 o il conteggio effettivo per un cursore dinamico, a seconda dell'origine dati.
  
## <a name="applies-to"></a>Si applica a

[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche

[Esempio di proprietà Filter e RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Esempio di proprietà Filter e RecordCount (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

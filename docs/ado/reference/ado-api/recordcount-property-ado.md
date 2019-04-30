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
manager: craigg
ms.openlocfilehash: fa6f29c480244919de71d06cf3d56e672f00c47f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240064"
---
# <a name="recordcount-property-ado"></a>Proprietà RecordCount (ADO)

Indica il numero di record in una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.
  
## <a name="return-value"></a>Valore restituito

Restituisce un **lungo** valore che indica il numero di record nelle **Recordset**.
  
## <a name="remarks"></a>Note

Usare la **RecordCount** sono di proprietà per scoprire il numero di record in un **Recordset** oggetto. La proprietà restituisce -1 se ADO non è possibile determinare il numero di record oppure se il tipo di cursore o provider non supporta **RecordCount**. Leggere il **RecordCount** proprietà in una classe chiusa **Recordset** provoca un errore.

#### <a name="bookmarks-or-approximate-positioning"></a>Segnalibri o approssimativo di posizionamento

Se l'oggetto Recordset *viene* supporta entrambi i segnalibri o simulare il posizionamento, questa proprietà restituisce il numero esatto di record del recordset. Questa proprietà restituisce il numero esatto indipendentemente dal fatto che il Recordset è stato completamente popolato.

Al contrario, se l'oggetto Recordset *non* supporta segnalibri o approssimativo di posizionamento, accedere a questa proprietà potrebbe essere un numero significativo sulle risorse. Termina lo svuotamento si verifica perché tutti i record devono recuperare e conteggiate per restituire un valore di RecordCount accurato.

- **adBookmark** correlate ai segnalibri.
- **adApproxPosition** è correlato al posizionamento approssimativo.

> [!NOTE]
> In ADO 2.8 e versioni precedenti, il provider SQLOLEDB recupera tutti i record quando viene utilizzato un cursore lato server, nonostante il fatto che restituisce **True** per entrambe **supporta (adApproxPosition)** e**Supporta (adBookmark)**.
  
Il tipo di cursore del **Recordset** oggetto influisce sulla possibilità di determinare il numero di record. Il **RecordCount** proprietà restituirà -1 per un cursore forward-only; il conteggio effettivo per un valore statico o keyset cursor; e -1 o il conteggio effettivo per un cursore dinamico, a seconda dell'origine dati.
  
## <a name="applies-to"></a>Si applica a

[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche

[Esempio di proprietà RecordCount (VB) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Esempio di proprietà RecordCount (VC + +) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

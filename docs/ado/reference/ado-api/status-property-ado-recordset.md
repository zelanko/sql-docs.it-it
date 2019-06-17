---
title: Proprietà Status (Recordset ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57767cb50382f676aec2e11eaef77a8cdab9a87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711006"
---
# <a name="status-property-ado-recordset"></a>Proprietà Status (Recordset - ADO)
Indica lo stato del record corrente per quanto riguarda gli aggiornamenti in batch o altre operazioni bulk.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una somma di uno o più [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) valori.  
  
## <a name="remarks"></a>Note  
 Usare la **stato** proprietà per visualizzare le modifiche in sospeso per i record modificati durante l'aggiornamento in batch. È anche possibile usare il **lo stato** proprietà per visualizzare lo stato del record non corretti durante le operazioni bulk, ad esempio quando chiama il [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oppure [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodi su un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto, o impostare il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà in un **Recordset** oggetto in una matrice dei segnalibri. Questa proprietà, è possibile determinare come un determinato record non è riuscita e risolvere il problema di conseguenza.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Status (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Esempio di proprietà Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   

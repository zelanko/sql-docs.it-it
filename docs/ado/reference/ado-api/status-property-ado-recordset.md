---
title: Proprietà Status (recordset ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d3ba9ad977fe02a712a675b8a9e4bae4b3d038b1
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759737"
---
# <a name="status-property-ado-recordset"></a>Proprietà Status (Recordset - ADO)
Indica lo stato del record corrente rispetto agli aggiornamenti batch o ad altre operazioni bulk.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una somma di uno o più valori [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Usare la proprietà **status** per vedere quali modifiche sono in sospeso per i record modificati durante l'aggiornamento del batch. È inoltre possibile utilizzare la proprietà **status** per visualizzare lo stato dei record che hanno esito negativo durante le operazioni bulk, ad esempio quando si chiamano i metodi [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) su un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oppure si imposta la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) per un oggetto **Recordset** su una matrice di segnalibri. Con questa proprietà è possibile determinare il modo in cui un determinato record ha avuto esito negativo e risolverlo di conseguenza.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Status (recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Esempio della proprietà Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   

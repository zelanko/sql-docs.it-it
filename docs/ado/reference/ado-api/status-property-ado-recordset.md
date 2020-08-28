---
description: Proprietà Status (Recordset - ADO)
title: Proprietà Status (recordset ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 546fc85e2f6fc2753b85a055f597b3d39129dd61
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988712"
---
# <a name="status-property-ado-recordset"></a>Proprietà Status (Recordset - ADO)
Indica lo stato del record corrente rispetto agli aggiornamenti batch o ad altre operazioni bulk.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una somma di uno o più valori [RecordStatusEnum](./recordstatusenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Usare la proprietà **status** per vedere quali modifiche sono in sospeso per i record modificati durante l'aggiornamento del batch. È inoltre possibile utilizzare la proprietà **status** per visualizzare lo stato dei record che hanno esito negativo durante le operazioni bulk, ad esempio quando si chiamano i metodi [Resync](./resync-method.md), [UpdateBatch](./updatebatch-method.md)o [CancelBatch](./cancelbatch-method-ado.md) su un oggetto [Recordset](./recordset-object-ado.md) oppure si imposta la proprietà [Filter](./filter-property.md) per un oggetto **Recordset** su una matrice di segnalibri. Con questa proprietà è possibile determinare il modo in cui un determinato record ha avuto esito negativo e risolverlo di conseguenza.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Status (recordset) (VB)](./status-property-example-recordset-vb.md)   
 [Esempio della proprietà Status (VC++)](./status-property-example-vc.md)
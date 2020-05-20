---
title: Metodo CancelBatch (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: rothja
ms.author: jroth
ms.openlocfilehash: c2e9f3b57137b4c113b9e177e9fecefec4070ac0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763172"
---
# <a name="cancelbatch-method-ado"></a>Metodo CancelBatch (ADO)
Annulla un aggiornamento batch in sospeso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Facoltativa. Valore [AffectEnum](../../../ado/reference/ado-api/affectenum.md) che indica il numero di record su cui avrà effetto il metodo **CancelBatch** .  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **CancelBatch** per annullare gli aggiornamenti in sospeso in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in modalità di aggiornamento batch. Se il **Recordset** è in modalità di aggiornamento immediato, la chiamata a **CancelBatch** senza **adAffectCurrent** genera un errore.  
  
 Se si modifica il record corrente o si aggiunge un nuovo record quando si chiama **CancelBatch**, ADO chiama prima il metodo [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) per annullare le modifiche memorizzate nella cache. Successivamente, tutte le modifiche in sospeso nel **Recordset** vengono annullate.  
  
 Il record corrente può essere determinabile dopo una chiamata **CancelBatch** , soprattutto se si è in corso l'aggiunta di un nuovo record. Per questo motivo, è consigliabile impostare la posizione del record corrente su una posizione nota nel **Recordset** dopo la chiamata a **CancelBatch** . Ad esempio, chiamare il metodo [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
 Se il tentativo di annullare gli aggiornamenti in sospeso ha esito negativo a causa di un conflitto con i dati sottostanti (ad esempio, se un record è stato eliminato da un altro utente), il provider restituisce gli avvisi alla raccolta degli [errori](../../../ado/reference/ado-api/errors-collection-ado.md) , ma non interrompe l'esecuzione del programma. Si verifica un errore di run-time solo se sono presenti conflitti in tutti i record richiesti. Utilizzare la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterAffectedRecords**) e la proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) per individuare i record con conflitti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi UpdateBatch e CancelBatch (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Esempio di metodi UpdateBatch e CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Metodo Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Metodo Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

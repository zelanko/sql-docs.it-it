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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 572738c966651e35f2980ea75c3770ddc4bd029d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696174"
---
# <a name="cancelbatch-method-ado"></a>Metodo CancelBatch (ADO)
Annulla un aggiornamento batch in sospeso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Facoltativo. Un' [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valore che indica il numero di record la **CancelBatch** saranno influenzati dal metodo.  
  
## <a name="remarks"></a>Note  
 Usare la **CancelBatch** metodo annullare eventuali aggiornamenti in sospeso in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in modalità di aggiornamento batch. Se il **Recordset** è in modalità di aggiornamento immediato, chiama **CancelBatch** senza **adAffectCurrent** genera un errore.  
  
 Se si sta modificando il record corrente o si aggiunge un nuovo record quando si chiama **CancelBatch**, ADO prima chiama il [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo per annullare eventuali modifiche memorizzate nella cache. Successivamente, tutte le modifiche in sospeso il **Recordset** vengono annullate.  
  
 Il record corrente potrebbe essere non determinabile dopo una **CancelBatch** chiamare, in particolare se fosse in corso l'aggiunta di un nuovo record. Per questo motivo, è consigliabile impostare la posizione del record corrente in una posizione nota nel **Recordset** dopo le **CancelBatch** chiamare. Ad esempio, chiama il [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) (metodo).  
  
 Se il tentativo di annullare gli aggiornamenti in sospeso non riesce a causa di un conflitto con i dati sottostanti (ad esempio, se un record è stato eliminato da un altro utente), il provider restituisce avvisi per i [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta ma non arrestano esecuzione del programma. Errore di run-time si verifica solo se sono presenti conflitti in tutti i record richiesti. Usare la [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà (**adFilterAffectedRecords**) e il [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà per individuare i record con conflitti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di UpdateBatch e CancelBatch (esempio di metodi (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Esempio UpdateBatch e CancelBatch metodi (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Metodo Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Metodo CancelUpdate (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

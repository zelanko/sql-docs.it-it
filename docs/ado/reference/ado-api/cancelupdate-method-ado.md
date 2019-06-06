---
title: Metodo CancelUpdate (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b53fa2e9d69b39218d846b57070b78ae230d81cf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698820"
---
# <a name="cancelupdate-method-ado"></a>Metodo CancelUpdate (ADO)
Annulla tutte le modifiche apportate alla riga corrente o nuova di un' [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, o il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto, prima di chiamare il [Update ](../../../ado/reference/ado-api/update-method.md) (metodo).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Note  
  
## <a name="recordset"></a>recordset  
 Usare la **CancelUpdate** metodo per annullare le modifiche apportate alla riga corrente oppure per eliminare una riga appena aggiunta. Non è possibile annullare le modifiche apportate alla riga corrente o a una nuova riga dopo la chiamata il **Update** metodo, a meno che le modifiche siano parte di una transazione di cui è possibile eseguire il rollback con la [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) (metodo), o in parte un aggiornamento batch. Nel caso di un aggiornamento batch, è possibile annullare il **aggiornare** con il **CancelUpdate** oppure [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) (metodo).  
  
 Se si aggiunge una nuova riga quando si chiama il **CancelUpdate** metodo, la riga corrente diventa la riga corrente prima di [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) chiamare.  
  
 Se si sono in modalità di modifica e si vuole eseguire la migrazione del record corrente (ad esempio, tramite il [spostare](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), o [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodi), è possibile usare  **Metodo CancelUpdate** per annullare le modifiche in sospeso. Potrebbe essere necessario eseguire questa operazione se l'aggiornamento non è possibile inviare all'origine dati. Ad esempio, un tentativo di eliminazione che ha esito negativo a causa di violazioni di integrità referenziale lascerà il **Recordset** in modalità di modifica dopo una chiamata a [eliminare](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Record  
 Il **CancelUpdate** metodo annulla tutte le operazioni di inserimento o eliminazione di in sospeso [campo](../../../ado/reference/ado-api/field-object.md) oggetti e Annulla gli aggiornamenti dei campi esistenti in sospeso e li Ripristina i valori originali. Il [lo stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà di tutti i campi il **campi** raccolta è impostata su **adFieldOK**.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento metodi e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Aggiornamento metodi e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Metodo AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Metodo Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo CancelUpdate (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)

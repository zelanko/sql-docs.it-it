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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ecc08dde974826846058d4d8927df202367d28d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242408"
---
# <a name="cancelupdate-method-ado"></a>Metodo CancelUpdate (ADO)
Annulla tutte le modifiche apportate alla riga corrente o nuova di un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oppure alla raccolta di [campi](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) , prima di chiamare il metodo [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="recordset"></a>recordset  
 Utilizzare il metodo **CancelUpdate** per annullare tutte le modifiche apportate alla riga corrente o per eliminare una nuova riga aggiunta. Non è possibile annullare le modifiche apportate alla riga corrente o a una nuova riga dopo aver chiamato il metodo **Update** , a meno che le modifiche non facciano parte di una transazione di cui è possibile eseguire il rollback con il metodo [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) o che facciano parte di un aggiornamento batch. Nel caso di un aggiornamento batch, è possibile annullare l' **aggiornamento** con il metodo **CancelUpdate** o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .  
  
 Se si aggiunge una nuova riga quando si chiama il metodo **CancelUpdate** , la riga corrente diventa la riga corrente prima della chiamata a [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) .  
  
 Se si è in modalità di modifica e si vuole spostare il record corrente (ad esempio, usando i metodi [Move](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)o [Close](../../../ado/reference/ado-api/close-method-ado.md) ), è possibile usare **CancelUpdate** per annullare le modifiche in sospeso. Potrebbe essere necessario eseguire questa operazione se l'aggiornamento non può essere pubblicato correttamente nell'origine dati. Ad esempio, un tentativo di eliminazione che ha esito negativo a causa di violazioni di integrità referenziale lascerà il **Recordset** in modalità di modifica dopo una chiamata a [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Record  
 Il metodo **CancelUpdate** Annulla tutti gli inserimenti o le eliminazioni in sospeso degli oggetti [campo](../../../ado/reference/ado-api/field-object.md) e Annulla gli aggiornamenti in sospeso dei campi esistenti e li ripristina nei valori originali. La proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) di tutti i campi nella raccolta **Fields** è impostata su **adFieldOK**.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedi anche  
 [Esempio di metodi Update e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Esempio di metodi Update e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Metodo AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Metodo Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Metodo Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)

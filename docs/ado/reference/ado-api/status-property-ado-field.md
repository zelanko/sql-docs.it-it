---
title: Proprietà Status (campo ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11a39cf6f30e7a4892d6f2df5c8c373ab6847632
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240332"
---
# <a name="status-property-ado-field"></a>Proprietà Status (Field - ADO)
Indica lo stato di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) valore. Il valore predefinito è **adFieldOK**.  
  
## <a name="remarks"></a>Note  
  
## <a name="record-field-status"></a>Stato dei campi di record  
 Modifiche al valore di una **campo** oggetto nella raccolta di campi di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto vengono memorizzati nella cache finché l'oggetto [Update](../../../ado/reference/ado-api/update-method.md) viene chiamato il metodo. Se le modifiche apportate al valore del campo ha causato un errore, a questo punto, viene generato l'errore OLE DB **DB_E_ERRORSOCCURRED** (2147749409). La proprietà di stato di uno qualsiasi del **campo** gli oggetti nel **campi** raccolta che ha causato l'errore conterrà un valore compreso il [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) che descrive la causa di il problema.  
  
 Per migliorare le prestazioni, aggiunte ed eliminazioni per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolte del **Record** oggetto vengono memorizzati nella cache finché il **Update** viene chiamato il metodo e quindi le modifiche vengono eseguite un aggiornamento in blocco ottimistico. Se il **Update** non viene chiamato, il server non vengono aggiornato. Se tutti gli aggiornamenti non riescono, viene restituito un errore del provider OLE DB (DB_E_ERRORSOCCURRED) e il **stato** proprietà indica la somma dei valori del codice di stato operazione e di errore. Ad esempio, **adFieldPendingInsert o eliminato**. Il **lo stato** proprietà per ogni **campo** può essere utilizzato per determinare il motivo il **campo** non aggiunto, modificato o eliminato.  
  
 Molti tipi di problemi riscontrati quando si aggiunge, modifica o eliminazione di un **campo** vengono segnalati tramite il **stato** proprietà. Ad esempio, se l'utente elimina un **campo**, è contrassegnata per l'eliminazione dalle **campi** raccolta. Se il successivo **Update** restituisce un errore perché l'utente ha tentato di eliminare un **campo** per cui non dispongono dell'autorizzazione, il **campo** avranno un  **Lo stato** dei **adFieldPermissionDenied o adFieldPendingDelete**. Chiama il [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo ripristini i valori originale e imposta il **stato** a **adFieldOK**.  
  
 Analogamente, il **Update** metodo può restituire un errore perché un nuovo **campo** è stato aggiunto e assegnargli un valore non appropriato. In tal caso il nuovo **campo** sarà nel **campi** insieme e hanno lo stato **adFieldPendingInsert** ed eventualmente **adFieldCantCreate** (a seconda del provider). È possibile fornire un valore appropriato per il nuovo **campo** e chiamare **Update** nuovamente.  
  
## <a name="recordset-field-status"></a>Stato dei campi di recordset  
 Modifiche al valore di una **campo** oggetto nella raccolta di campi di uno una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) vengono memorizzati nella cache finché l'oggetto [Update](../../../ado/reference/ado-api/update-method.md) viene chiamato il metodo. Se le modifiche apportate al valore del campo ha causato un errore, a questo punto, viene generato l'errore OLE DB **DB_E_ERRORSOCCURRED** (2147749409). La proprietà di stato di uno qualsiasi del **campo** gli oggetti nel **campi** raccolta che ha causato l'errore conterrà un valore compreso il [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) che descrive la causa di il problema.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Status (campo) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Esempio di proprietà Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   

---
title: Metodo (Recordset ADO) Delete | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fab7baf1771ad0600f4c1a0a8cac931f0adcc0a4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695422"
---
# <a name="delete-method-ado-recordset"></a>Metodo Delete (Recordset - ADO)
Elimina il record corrente o un gruppo di record.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Un' [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valore che determina il numero di record la **eliminare** saranno influenzati dal metodo. Il valore predefinito è **adAffectCurrent**.  
  
> [!NOTE]
>  **adAffectAll** e **adAffectAllChapters** non sono argomenti validi **eliminare**.  
  
## <a name="remarks"></a>Note  
 Usando il **eliminare** metodo contrassegna il record corrente o un gruppo di record in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto per l'eliminazione. Se il **Recordset** oggetto non consente l'eliminazione di record, si verifica un errore. Se si è in modalità di aggiornamento immediato, le eliminazioni verranno eseguite immediatamente nel database. Se non è possibile eliminare un record (a causa di violazioni di integrità del database, ad esempio), il record rimarranno nella modalità di modifica dopo la chiamata a [Update](../../../ado/reference/ado-api/update-method.md). Ciò significa che è necessario annullare l'aggiornamento con [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) prima di uscire il record corrente (ad esempio, con [Close](../../../ado/reference/ado-api/close-method-ado.md), [spostare](../../../ado/reference/ado-api/move-method-ado.md), o [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se si è in modalità di aggiornamento batch, i record contrassegnati per l'eliminazione dalla cache e l'eliminazione effettiva si verifica quando si chiama il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (metodo). Usare la [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà per visualizzare i record eliminati.  
  
 Il recupero dei valori di campo del record eliminato genera un errore. Dopo aver eliminato il record corrente, il record eliminato rimane invariato fino a quando non si sposta in un altro record. Una volta si allontanano del record eliminato, non è più accessibile.  
  
 Se le eliminazioni in una transazione vengono nidificate, è possibile ripristinare i record eliminati con il [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) (metodo). Se si è in modalità di aggiornamento batch, è possibile annullare l'eliminazione in sospeso o un gruppo di eliminazioni in sospeso con le [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) (metodo).  
  
 Se il tentativo di eliminare i record non riesce a causa di un conflitto con i dati sottostanti (ad esempio, un record è già stato eliminato da un altro utente), il provider restituisce avvisi per i [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta ma non arrestano programma esecuzione. Errore di run-time si verifica solo se sono presenti conflitti in tutti i record richiesti.  
  
 Se il [tabelle univoche](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) dinamica è impostata e il **Recordset** è il risultato dell'esecuzione di un'operazione di JOIN in più tabelle, il **Elimina** metodo che verrà eliminato solo le righe dalla tabella menzionata nel [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo Delete (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Esempio del metodo Delete (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Esempio del metodo Delete (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Metodo Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (insieme di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Metodo DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

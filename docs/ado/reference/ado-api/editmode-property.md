---
title: Proprietà EditMode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 147528e9400d6befe9d5cb3c5d3cc3f882e48ad0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181131"
---
# <a name="editmode-property"></a>Proprietà EditMode
Indica lo stato di modifica del record corrente.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valore.  
  
## <a name="remarks"></a>Note  
 ADO mantiene un buffer di modifica associato al record corrente. Questa proprietà indica se sono state apportate modifiche a questo buffer, o se è stato creato un nuovo record. Usare la **EditMode** proprietà per determinare lo stato di modifica del record corrente. È possibile verificare le modifiche in sospeso se un processo di modifica è stata interrotta e determinare se è necessario usare il [Update](../../../ado/reference/ado-api/update-method.md) oppure [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) (metodo).  
  
 Nella *modalità di aggiornamento immediato* le **EditMode** viene reimpostata a **adEditNone** dopo una chiamata al **aggiornare** viene chiamato il metodo . Quando una chiamata a [eliminare](../../../ado/reference/ado-api/delete-method-ado-recordset.md) non è stato eliminare i record nell'origine dati (ad esempio, a causa di violazioni di integrità referenziale), il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) rimane in modalità di modifica (**EditMode** = **adEditInProgress**). Pertanto **CancelUpdate** deve essere chiamato prima di uscire il record corrente (ad esempio con [spostare](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), o [chiudere](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 Nella *modalità di aggiornamento batch* (in cui il provider vengono memorizzati nella cache più modifiche e li scrive all'origine dati sottostante solo quando si chiama il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo), il valore del **EditMode**  proprietà viene modificata quando viene eseguita la prima operazione e non viene ripristinato da una chiamata per il **Update** (metodo). Operazioni successive non modificare il valore della **EditMode** proprietà, anche se vengono eseguite diverse operazioni. Ad esempio, se la prima operazione consiste nell'aggiungere un nuovo record e il secondo apporta modifiche a un oggetto esistente di record, la proprietà del **EditMode** saranno ancora **adEditAdd**. Il **EditMode** proprietà non venga reimpostata **adEditNone** fino a quando non dopo la chiamata a **UpdateBatch**. Per determinare quali operazioni sono state eseguite, impostare il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) in modo che solo i record con le modifiche in sospeso verranno visibile ed esaminare il [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà di ogni record per determinare quali modifiche sono state apportate ai dati.  
  
> [!NOTE]
>  **Proprietà EditMode** può restituire un valore valido solo se viene rilevato un record corrente. **Proprietà EditMode** restituirà un errore se [BOF o EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è true, o se il record corrente è stato eliminato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CursorType, LockType ed esempio di proprietà EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType ed EditMode esempio di proprietà (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Metodo AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Elimina metodo (Recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)

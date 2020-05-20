---
title: Metodo Clear (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: rothja
ms.author: jroth
ms.openlocfilehash: 187000a648ca2e5e28ba09f10e3dfe55fea51b1d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763132"
---
# <a name="clear-method-ado"></a>Metodo Clear (ADO)
Rimuove tutti gli oggetti [Error](../../../ado/reference/ado-api/error-object.md) dalla raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il metodo **Clear** sulla raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) per rimuovere tutti gli oggetti [Error](../../../ado/reference/ado-api/error-object.md) esistenti dalla raccolta. Quando si verifica un errore, ADO cancella automaticamente la raccolta degli **errori** e la riempie con gli oggetti **Error** in base al nuovo errore.  
  
 Alcune proprietà e metodi restituiscono avvisi visualizzati come oggetti **Error** nella raccolta **Errors** ma non interrompono l'esecuzione di un programma. Prima di chiamare i metodi [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) su un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ; metodo [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) su un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) . in alternativa, impostare la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) per un oggetto **Recordset** , chiamare il metodo **Clear** sulla raccolta **Errors** . In questo modo, è possibile leggere la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) della raccolta **Errors** per verificare la presenza di avvisi restituiti.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Execute, Requery e Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Esempio di metodi Execute, Requery e Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Esempio di metodi Execute, Requery e Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo Delete (raccolta di campi ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (raccolta Parameters ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Metodo Delete (recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Filter (proprietà)](../../../ado/reference/ado-api/filter-property.md)   
 [Metodo di risincronizzazione](../../../ado/reference/ado-api/resync-method.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e69e7d2d2a66ccb9df0e03f6f77849c502f3bf2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239750"
---
# <a name="clear-method-ado"></a>Metodo Clear (ADO)
Rimuove tutti i [errore](../../../ado/reference/ado-api/error-object.md) oggetti dalle [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Note  
 Usare il **chiaro** metodo sulle [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta da cui rimuovere tutte le [errore](../../../ado/reference/ado-api/error-object.md) oggetti dalla raccolta. Quando si verifica un errore, ADO Cancella automaticamente la **errori** raccolta e la riempie con **errore** gli oggetti in base al nuovo errore.  
  
 Alcune proprietà e metodi restituiscono gli avvisi che vengono visualizzati come **errore** gli oggetti nel **errori** raccolta ma non arrestano l'esecuzione del programma. Prima di chiamare il [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodi su un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ; dell'oggetto di [aprire](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo su un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) ; dell'oggetto o impostare il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà su un **Recordset** dell'oggetto, chiamare il **Clear**metodo su di **errori** raccolta. In questo modo, è possibile leggere il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà delle **errori** insieme per provare gli avvisi restituiti.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di errori (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (insieme di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Elimina metodo (Recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Proprietà filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Metodo Resync](../../../ado/reference/ado-api/resync-method.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

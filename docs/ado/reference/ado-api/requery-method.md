---
title: Metodo Requery | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: rothja
ms.author: jroth
ms.openlocfilehash: 29b2d0cba996e3f41a12df93babe8d9b86a8fbeb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756520"
---
# <a name="requery-method"></a>Metodo Requery
Aggiorna i dati in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) eseguendo nuovamente la query su cui è basato l'oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *Opzioni*  
 Facoltativa. Maschera di maschera che contiene i valori [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) che interessano questa operazione.  
  
> [!NOTE]
>  Se *options* è impostato su **adAsyncExecute**, questa operazione viene eseguita in modo asincrono e viene emesso un evento [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) alla conclusione. I valori **ExecuteOpenEnum** di **adExecuteNoRecords** o **adExecuteStream** non devono essere utilizzati con la **riesecuzione della query**.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare il metodo **Requery** per aggiornare l'intero contenuto di un oggetto **Recordset** dall'origine dati rilasciando il comando originale e recuperando i dati una seconda volta. La chiamata a questo metodo equivale alla chiamata dei metodi [Close](../../../ado/reference/ado-api/close-method-ado.md) e [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) in successione. Se si modifica il record corrente o si aggiunge un nuovo record, si verificherà un errore.  
  
 Mentre l'oggetto **Recordset** è aperto, le proprietà che definiscono la natura del cursore ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [maxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)e così via) sono di sola lettura. Pertanto, il metodo **Requery** può aggiornare solo il cursore corrente. Per modificare le proprietà del cursore e visualizzare i risultati, è necessario utilizzare il metodo [Close](../../../ado/reference/ado-api/close-method-ado.md) in modo che le proprietà diventino di nuovo in lettura/scrittura. È quindi possibile modificare le impostazioni delle proprietà e chiamare il metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) per riaprire il cursore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Execute, Requery e Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Esempio di metodi Execute, Requery e Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Esempio di metodi Execute, Requery e Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
